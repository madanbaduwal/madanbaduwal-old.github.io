---
title: "Image classification in keras"
date: 2020-12-27T00:00-00:00
last_modified_at: 2020-12-27T00:00:00-00:00
categories:
  - AI
permalink: /Image-classification-in-keras/
classes: wide
excerpt: Image classification in keras. 
---

Keras for any image classification task.
=======================================

Introduction
------------

Computer vision task : 
* Recognition 
    * Semantic Segmentation 
    * Image Classification 
    * Object Localization 
    * Object Detection 
    * Instance Segmentation

-   Motion analysis
-   Scene reconstruction
-   Image captioning
-   Image Generation

In this assignment, we will directly classify images without doing
segmentation. That means we didn’t assign a label to every pixel in the
image. We will directly assign a label to the entire image.

Dataset
-------

You can collect data manually or from different sources like imagenet,
kaggle, github… so on. It depends on your project whether you can
collect your data manually or you need to use data from a different
resource.

Note: Data should be genuine. \* Dataset and algorithm accuracy play an
important role while publishing a research paper.

### Train dataset

-   It is the set of data used to train the model.
-   During each epoch a model will be trained over and over again on the
    same data in our training set and we continue to learn about the
    features of this data.

### Validation dataset (also known as Hold out)

-   The validation set is a set of data separate from the training set.
    That is used to validate our model during training.
-   This validation process helps give information that may assist in
    adjusting hyperparameter.
-   In each epoch during training the model will be trained on the data
    in the training set well it also be simultaneously validating on the
    data in the validation set.
-   One of the major reasons we need a validation set is to ensure that
    the model is not overfitting to the one the training set.
-   If training accuracy high and validation accuracy low: Overfitting
-   If model training accuracy high and validation accuracy also high:
    Not overfitting

Note: The weight won’t be updated in the model

### Cross validation dataset(CV)

-   In CV we use the validation set also for the training due to the
    clever manipulation used by us.

Note: The weight updates in the model

### Test dataset

-   The test set is the set of data that is used to test the model after
    the model has already trained.
-   This test set is different from both the training and validation
    set.
-   After a model has been trained and validated using our training and
    validation set we will then use our model to predict the output of
    the test set.

Note: The major difference between the test and other sets we have
discussed is that the test set should not be labeled. The training set
and validation set have to be labeled so that we can see the matrix
given during training like loss and the accuracy in each epoch.

-   When the model is predicting on the unlabeled data in our test set
    this will be the same type of process that we will be used when we
    deploy our model into the field.

Data / image Preprocessing
--------------------------

### With data augmentation

If you have a less number of a dataset then you can do data
augmentation.

#### Image generator

Why image generator?

Here are lots of image datasets so we can’t store this dataset into a
variable. It shows a memory error. First, we create a generator for
training, validation, and test dataset. At the time of model
training(model.fit) , we call generator(trainng\_generator) to generate
batch of image from given directory(training\_data\_dir,
validation\_data\_dir,test\_data\_dir).

#### If you have dataset only(we need to split this data into train and validation)

Folder Organization

    ├── data
    │   
        ├── class A
            ├── image1.jpg
            ├── image2.jpg
            ...
        ├── Class B
              ├── image1.jpg
              ├── image2.jpg
              ...
        ├── Class C
              ├── image1.jpg
              ├── image2.jpg
              ...

``` 
from google.colab import drive
drive.mount('/drive')
```

``` 
data_dir = "/drive/My Drive/covid/data/train" 
```

``` 
import tensorflow as tf
# we usually do augumention with training dataset only because we need to incerase training dataset.
training_data_generator = tf.keras.preprocessing.image.ImageDataGenerator( 
    featurewise_center = False,
    samplewise_center = False,
    featurewise_std_normalization = False,
    samplewise_std_normalization = False,
    zca_whitening = False,
    zca_epsilon = 1e-06,
    rotation_range = 0,
    width_shift_range = 0.0,
    height_shift_range = 0.0,
    brightness_range = None,
    shear_range = 0.1,
    zoom_range = 0.1,
    channel_shift_range = 0.0,
    fill_mode = "nearest",
    cval = 0.0,
    horizontal_flip = True,
    vertical_flip = False,
    rescale = 1./255,
    preprocessing_function = None,
    data_format = None,
    validation_split = 0.2, # If you have dataset (only data folder) then you need to split it into training and validation.
    # Fraction of images reserved for validation (strictly between 0 and 1). 
    # Below training_data_generator.flow_from_directory  subset= "training" give training set and subset="validation" give test/validation set
    dtype = None,
)
```

``` 
val_data_generator = tf.keras.preprocessing.image.ImageDataGenerator(rescale=1./255)
```

``` 
# prepare iterator
train_generator = training_data_generator.flow_from_directory( 
    data_dir,
    target_size=(224, 224),
    color_mode="rgb",
    classes=None,
    class_mode="categorical",
    batch_size= 32, # 32 images pick from training folder at a time
    shuffle=True,
    seed=None,
    save_to_dir=None, # If you want to save augumented data in directory
    save_prefix="",
    save_format="png",
    follow_links=False,
    subset="training", # Subset of data ("training" or "validation") if validation_split is set in ImageDataGenerator.
    interpolation="nearest",
)
```

``` 
train_generator.class_indices
```

``` 
val_generator = val_data_generator.flow_from_directory( 
    data_dir,
    target_size=(224, 224),
    color_mode="rgb",
    classes=None,
    class_mode="categorical",
    batch_size=32,
    shuffle=True,
    seed=None,
    save_to_dir=None,
    save_prefix="",
    save_format="png",
    follow_links=False,
    subset="validation",
    interpolation="nearest",
)
```

``` 
val_generator.class_indices
```

#### If you have both training and validation dataset

Folder Organization

    ├── data
    │   ├── train    
            ├── class A
                ├── image1.jpg
                ├── image2.jpg
                ...
            ├── Class B
                 ├── image1.jpg
                 ├── image2.jpg
                 ...
            ├── Class C
                 ├── image1.jpg
                 ├── image2.jpg
                 ...
            ... 
    │   ├── test   
            ├── class A
                ├── image1.jpg
                ├── image2.jpg
                ...
            ├── Class B
                ├── image1.jpg
                ├── image2.jpg
                ...
            ├── Class C
                ├── image1.jpg
                ├── image2.jpg
                ...
            ...  

``` 
train_data_dir = "/drive/My Drive/covid/dataset/train"
val_data_dir = "/drive/My Drive/covid/dataset/test" 
```

``` 
import tensorflow as tf
training_data_generator = tf.keras.preprocessing.image.ImageDataGenerator( 
    featurewise_center=False,
    samplewise_center=False,
    featurewise_std_normalization=False,
    samplewise_std_normalization=False,
    zca_whitening=False,
    zca_epsilon=1e-06,
    rotation_range=0,
    width_shift_range=0.0,
    height_shift_range=0.0,
    brightness_range=None,
    shear_range=0.1,
    zoom_range=0.1,
    channel_shift_range=0.0,
    fill_mode="nearest",
    cval=0.0,
    horizontal_flip=True,
    vertical_flip=False,
    rescale=1./255,
    preprocessing_function=None,
    data_format=None,
    validation_split=0.0,
    dtype=None,
)
```

``` 
val_data_generator = tf.keras.preprocessing.image.ImageDataGenerator(rescale=1./255)
```

Here we have a directory so we need to use .flow_from_directory
method.

.flow_from_directory(directory)

``` 
# prepare iterator
train_generator = training_data_generator.flow_from_directory( 
    train_data_dir,
    target_size=(224, 224),
    color_mode="rgb",
    classes=None,
    class_mode="categorical",
    batch_size= 32, 
    shuffle=True,
    seed=None,
    save_to_dir=None, 
    save_prefix="",
    save_format="png",
    follow_links=False,
    subset=None,
    interpolation="nearest",
)
```

``` 
val_generator = val_data_generator.flow_from_directory( 
    val_data_dir,
    target_size=(224, 224),
    color_mode="rgb",
    classes=None,
    class_mode="categorical",
    batch_size=32,
    shuffle=True,
    seed=None,
    save_to_dir=None,
    save_prefix="",
    save_format="png",
    follow_links=False,
    subset=None,
    interpolation="nearest",
)
```

.flow and .flow_from_dataframe mehods

-   .flow is used when we have a dataset in NumPy array of rank 4 or a
    tuple.
-   .flow_from_dataframe is use when pandas data frame. Which
    containing the file paths relative to the directory (or absolute
    paths if the directory is None) of the images in a string column.

### Without data augmentation

If you have enough dataset then you didn’t need to do augmentation. You
can load data directly from the directory.

#### If you have dataset only(we need to split this data into train and validation)

Folder Organization

    ├── data
    │   
        ├── class A
            ├── image1.jpg
            ├── image2.jpg
            ...
        ├── Class B
              ├── image1.jpg
              ├── image2.jpg
              ...
        ├── Class C
              ├── image1.jpg
              ├── image2.jpg
              ...

``` 
training_data = tf.keras.preprocessing.image_dataset_from_directory(
    data_dir,
    labels="inferred",
    label_mode="int",
    class_names=None,
    color_mode="rgb",
    batch_size=32,
    image_size=(256, 256),
    shuffle=True,
    seed=None,
    validation_split=0.2,# If you have dataset (only data folder) then you need to split it into training and validation.
    # Fraction of images reserved for validation (strictly between 0 and 1). 
    subset="training", # Only used if validation_split is set
    interpolation="bilinear",
    follow_links=False,
)
```

``` 
validation_data = tf.keras.preprocessing.image_dataset_from_directory(
    data_dir,
    labels="inferred",
    label_mode="int",
    class_names=None,
    color_mode="rgb",
    batch_size=32,
    image_size=(256, 256),
    shuffle=True,
    seed=None,
    validation_split=0.2,
    subset="validation", # Only used if validation_split is set
    interpolation="bilinear",
    follow_links=False,
)
```

#### If you have both training and validation dataset

Folder Organization

    ├── data
    │   ├── train    
            ├── class A
                ├── image1.jpg
                ├── image2.jpg
                ...
            ├── Class B
                 ├── image1.jpg
                 ├── image2.jpg
                 ...
            ├── Class C
                 ├── image1.jpg
                 ├── image2.jpg
                 ...
            ... 
    │   ├── test   
            ├── class A
                ├── image1.jpg
                ├── image2.jpg
                ...
            ├── Class B
                ├── image1.jpg
                ├── image2.jpg
                ...
            ├── Class C
                ├── image1.jpg
                ├── image2.jpg
                ...
            ...  

``` 
training_data = tf.keras.preprocessing.image_dataset_from_directory(
    train_data_dir,
    labels="inferred",
    label_mode="int",
    class_names=None,
    color_mode="rgb",
    batch_size=32,
    image_size=(256, 256),
    shuffle=True,
    seed=None,
    validation_split=None,
    subset=None,
    interpolation="bilinear",
    follow_links=False,
)
```

``` 
validation_data = tf.keras.preprocessing.image_dataset_from_directory(
    val_data_dir,
    labels="inferred",
    label_mode="int",
    class_names=None,
    color_mode="rgb",
    batch_size=32,
    image_size=(256, 256),
    shuffle=True,
    seed=None,
    validation_split=None,
    subset=None,
    interpolation="bilinear",
    follow_links=False,
)
```

### Note (Most important note)

-   In the above we only define generator.

``` 
import sys

print(sys.getsizeof(training_data_generator))
print(sys.getsizeof(train_generator))
print(sys.getsizeof(val_generator))
```

Visualize preprocess data
-------------------------

Here are the sample images in the training dataset.

``` 
next(train_generator) 
```

``` 
from matplotlib import pyplot 
for X_batch, y_batch in training_generator:
    for i in range(0, 2):
        pyplot.imshow(X_batch[i], cmap=pyplot.get_cmap('gray'))
        pyplot.show()
    break
```

Build and compile models
------------------------

You can create your own model from scratch or you can do transfer
learning. We will do transfer learning here.

### Build your model


``` 
from keras.layers import *
from keras.models import *
from tensorflow import keras

model = Sequential()
model.add(Conv2D(32,kernel_size=(3,3),activation='relu',input_shape=(224,224,3)))
model.add(Conv2D(64,(3,3),activation='relu'))
model.add(MaxPooling2D(pool_size=(2,2)))
model.add(Dropout(0.25))

model.add(Conv2D(64,(3,3),activation='relu'))
model.add(MaxPooling2D(pool_size=(2,2)))
model.add(Dropout(0.25))

model.add(Flatten())
model.add(Dense(64,activation='relu'))
model.add(Dropout(0.5))
model.add(Dense(2,activation='sigmoid'))

model.compile(loss=keras.losses.binary_crossentropy,optimizer='adam',metrics = ['accuracy'])

model.summary()
```

### Transfar learning

#### InceptionV3 - Pretrained

``` 
from keras.layers import Dense, GlobalAveragePooling2D
from keras.models import Model
from keras.optimizers import Adam

from keras.applications.inception_v3 import InceptionV3

base_model=keras.applications.inception_v3.InceptionV3(weights='imagenet',include_top=False)

x = base_model.output
x = GlobalAveragePooling2D()(x)
x = Dense(1024, activation='relu')(x)
predictions = Dense(2, activation='softmax')(x)

model = Model(inputs=base_model.input, outputs=predictions)
model.compile(optimizer=Adam(lr=learning, beta_1=0.9, beta_2=0.999, amsgrad=False), loss='categorical_crossentropy',metrics=['accuracy'])

model.summary()
```

Train models(ML pipeline)
-------------------------

### Define hyperparameters

``` 
# Hyperparams
IMAGE_SIZE = 224
IMAGE_WIDTH, IMAGE_HEIGHT = IMAGE_SIZE, IMAGE_SIZE
EPOCHS = 5
BATCH_SIZE = 100
TEST_SIZE = 2
learning = 0.00001
input_shape = (IMAGE_WIDTH, IMAGE_HEIGHT, 3)
```

### model.fit

How model.fit work?

Fits the model on data yielded batch-by-batch by a Python generator.

``` 
pip install livelossplot
```

``` 
from livelossplot import PlotLossesKeras
from keras.callbacks import CSVLogger


H = model.fit(
    train_generator,
    steps_per_epoch=len(train_generator.filenames) // BATCH_SIZE,
    epochs=EPOCHS,
    validation_data=val_generator, # Note : validation data is not use in training here so maximum project we found  test data as validation here so validation = test
    validation_steps=len(val_generator.filenames) // BATCH_SIZE,
    callbacks=[PlotLossesKeras(), CSVLogger(TRAINING_LOGS_FILE,
                                            append=False,
                                            separator=";")], 
    verbose=1)
```

Model Evaluation on validation data
-----------------------------------

Here we evaluate the model on validation set because validation is not
used in training so it’s like unknown data for the model.

``` 
from sklearn.metrics import classification_report, confusion_matrix, roc_curve, auc
import seaborn as sns

LABELS = ["covid-19","normal"]

def show_confusion_matrix(validations, predictions):
    matrix = confusion_matrix(validations, predictions)
    plt.figure(figsize=(8, 6))
    sns.heatmap(matrix,
                cmap="coolwarm",
                linecolor='white',
                linewidths=1,
                xticklabels=LABELS,
                yticklabels=LABELS,
                annot=True,
                fmt="d")
    plt.title("Confusion Matrix")
    plt.ylabel("True Label")
    plt.xlabel("Predicted Label")
    plt.show()

filenames = validation_generator.filenames
nb_samples = len(filenames)

Y_pred = model1.predict_generator(validation_generator)
y_pred = np.argmax(Y_pred, axis=1)
print('Confusion Matrix')
show_confusion_matrix(validation_generator.classes, y_pred)
print(confusion_matrix(validation_generator.classes, y_pred))
print('Classification Report')
target_names = ["covid-19","normal"]
print(classification_report(validation_generator.classes, y_pred, target_names=target_names))
# Plot linewidth.
lw = 2
# Compute ROC curve and ROC area for each class
fpr = dict()
tpr = dict()
roc_auc = dict()
for i in range(2):
   fpr[i], tpr[i], _ = roc_curve(validation_generator.classes, y_pred)
   roc_auc[i] = auc(fpr[i], tpr[i])

plt.figure()
lw = 2
plt.plot(fpr[0], tpr[0], color='darkorange',
       lw=lw, label='ROC curve (area = %0.4f)' % roc_auc[1])
plt.plot([0, 1], [0, 1], color='navy', lw=lw, linestyle='--')
plt.xlim([-0.01, 1.0])
plt.ylim([0.0, 1.05])
plt.xlabel('False Positive Rate')
plt.ylabel('True Positive Rate')
plt.title('Receiver operating characteristic example')
plt.legend(loc="lower right")
plt.show()
```

Run inference on test data
--------------------------

``` 
image_path = input("Input the path of image to predict")
  img = keras.preprocessing.image.load_img(
      image_path, target_size=(128,128)
  )
  img_array = keras.preprocessing.image.img_to_array(img)
  img_array = tf.expand_dims(img_array,0 )  # Create batch axis
  predictions = model.predict(img_array)
  score = predictions[0]
  print("Covid % is:",score[1])
  print("Normal % is:",score[0])
```


