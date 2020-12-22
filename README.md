# Run this project
## For local run
### Install dependencies
```
sudo apt-get install ruby ruby-dev make build-essential
sudo gem install -V bundler
bundle
```

### Run jekyll locally
```shell
make
```

## For custome domain
.np domain have no option CNAME so we follow cloudflare
### Steps
#### 1. Go to the https://www.cloudflare.com/en-au/
*  Redirected: Domani name point at ip address(A record)>DNS point ip address to another domain name(CNAME)

```A record : Madanbaduwal.com.np points to  185.199.108.153(githubip)
   A record : Madanbaduwal.com.np points to  185.199.109.153(githubip)
   A record : Madanbaduwal.com.np points to  185.199.110.153(githubip)
   A record : Madanbaduwal.com.np points to  185.199.111.153(githubip)
   
   CNAME record : MadanBaduwal.com.np is an alise of madanbaduwal.github.io
```

  Note : githubip are same  for all users.

* look your Primary name server and Secondary name server from cloudfair
Note : Primary name server and Secondary name server are different for all users so try to copy other , look in your cloudfair account.


#### 2. Go to the egister.com.np
* Pest you Primary name server and Secondary name server from cloudfair

#### 3. After 24 hours you will gate update

#### 4. Check whether my domain is Primary name server and Secondary name server from cloudfair

* https://dnschecker.org/all-dns-records-of-domain.php?query=madanbaduwal.com.np&rtype=ANY

#### 5. CNAME(no any extension) file in github

* You can create CNAME file manually in github project(CNAME align with index.html) with madanbaduwal.com.np.
 or 
* In project setting if we set custome domain it create CNAME file automatically with it body.

#### 6.SSL setup ( For secure)

Unfortunately Github pages does't support SSL on GIithub pages for custome domain , so do that in cloudfair
* Goto the SSL/TLS and make 
``` Full
Encrypts end-to-end, using a self signed certificate on the server
```
and 
* SSL/TLS Recommender ON

* Goto the Page rule  set the following two rules
``` 
madanbaduwal.com.np/*    : Always Use HTTPS

www.madanbaduwal.com.np/*  :Always Use HTTPS

```

#### 7. You can setup many rules in cloudfair for your website.

#### 8.Visiable in google + SEO 

* Go throw : https://mmistakes.github.io/minimal-mistakes/

* Google webmaster + Google search console 
* Verified your website by copy provided text and pest in DNS(cloudfair) as TXT record.

```
TXT record : Madanbaduwal.com.np points to  <text copy from google search console>.
```
* Submite your sitemap : https://madanbaduwal.com.np/sitemap.xml , in google search console.

#### 9.[Reference](https://mmistakes.github.io/minimal-mistakes)

# 10. Writing POST In This project

## 1. Directly write on .md file

## 2. Write on notebook(.ipynb)
### a. First convert .ipynb into .rst (we can't directly convert .ipynb to .md)
#### For this use nbconvert
     ```
     pip install nbconvert
     
     jupyter nbconvert --to <output format> <input notebook>
     
     example : jupyter nbconvert --to rst mynotebook.ipynb
    ```
### b. Second convert .rst to .md using online

 https://cloudconvert.com/rst-to-md

 
