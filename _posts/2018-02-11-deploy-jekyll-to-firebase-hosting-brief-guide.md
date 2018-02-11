---
title: Deploy Jekyll to Firebase Hosting - Brief Guide
layout: post
tags:
- tutorial
- jekyll
- firebase
- firebase-hosting
categories:
- tutorial
- jekyll
- firebase
description: The short and simple guide to deploy Jekyll to Firebase Hosting
og_image: firebase_jekyll-01.png
---

![](/firebase_jekyll-01.png)

<br />
In this article, we will deploy **Jekyll site to the Firebase Hosting**.
<br /><br />

<h2>Why Jekyll with Firebase Hosting?</h2>
<br />
Because I just published this website blog. Jekyll is good and simple way to start with and it will compile to static files. So, it will good for SEO!
<br /> <br />
**And you may think why don't I use github pages??**
<br />
Because github pages cannot serve custom domain site with secure verification (use SSL certificate). 
<br /> <br />
That's why I chose **Firebase Hosting**, it also serve our site over https protocol with free SSL certificate.
<br /> <br />

<h2>Let's Start!</h2>
<br />
<h4>Local Setup</h4>
Install Firebase tools CLI tools by running:
<br />
```bash
npm install -g firebase-tools
```
Then login to firebase by below command and follow the step:
<br />
```bash
firebase login
```
<br />
<h4>Project Config</h4>
Running init command:
<br />
```bash
firebase init
```
Follow step to select `Hosting` and `your firebase project`. Then you will get 2 new files: `firebase.json` and `.firebaserc`.
<br /> <br />
You don't have to care about `.firebaserc` file. But, let config `firebase.json` with following code:
```json
{
  "hosting": {
    "public": "_site",
    "ignore": [
      "**/.*",
      "firebase.json"
    ],
  }
}
```
In Jekyll, built project files will be in `_site` directory. So, the public directory to deploy will be `_site` directory.
<br /> <br />
<h4>Done! now let's deploy to Firebase Hosting</h4>
Running:
```bash
firebase deploy
```
When command finished, you now can access to site from browser!