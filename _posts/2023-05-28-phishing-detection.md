---
published: true
title: Phishing Detection
layout: single
date: 2023-05-10T00:00-00:00
last_modified_at: 2023--05-10T00:00:00-00:00
author_profile: true
read_time: true
permalink : /phishing-detection/
categories: [Projects]
excerpt : Phishing Detection using deep learning
header :
    og_image : "https://raw.githubusercontent.com/madanbaduwal/phishing-detection-transformer/main/docs/gif.gif"
    teaser: "https://raw.githubusercontent.com/madanbaduwal/phishing-detection-transformer/main/docs/gif.gif"
comments : true
sidebar:
    nav: sidebar-sample
---

Phishing attacks continue to be a major security threat
for individuals and organizations alike. It causes billions
of dollars in losses annually. Machine learning(ML) has
shown great promise in detecting such attacks by identifying patterns and anomalies in large datasets. The tradeoff between feature selection and model selection is a tedious task in ML for phishing detection. Low number
of features are not enough for the generalizability of traditional machine learning algorithms i.e.For Logistic Regression(LR), Support Vector Machine(SVM), Random Forest(RF), XG boost and Naive Bayes(NB). And it’s tough for
deep learning(DL) algorithms to learn features from ambiguities behaviour between phishing and non-phishing websites. This paper presents a comprehensive survey of various ML and ML paradigms that have been employed for
the detection of phishing websites. The survey also discusses various datasets, features, number of parameters in
algorithms, training time-space complexity in phishing detection and compares the accuracies of different ML techniques. The results of this survey provide valuable insight
into the current state of the art in phishing detection and can
serve as a useful resource for researchers and practitioners
working in this field.


<iframe width="700" height="500" src="https://raw.githubusercontent.com/madanbaduwal/phishing-detection-transformer/main/docs/gif.gif" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<br>

# Run Project 

```bash

cd phishing-detection-transformer

cd src

pip3 install -r requirements.txt

streamlit run app.py

```
