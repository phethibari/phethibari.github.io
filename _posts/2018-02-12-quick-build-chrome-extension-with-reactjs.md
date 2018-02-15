---
title: Quick build Chrome Extension with ReactJS
layout: post
tags:
- reactjs
- chrome-extension
- tips
categories:
- tips
- reactjs
description: Quick build Chrome Extension with ReactJS
og_image: chr-ext-6.png
---

![](/chr-ext-6.png)

<br />
Few days ago, I just read [Getting Started: Building a Chrome Extension](https://developer.chrome.com/extensions/getstarted) and then I found out first paragraph:
<br /> <br />

> Extensions allow you to add functionality to Chrome without diving deeply into native code. **You can create new extensions for Chrome with those core technologies that you're already familiar with from web development: HTML, CSS, and JavaScript**. If you've ever built a web page, you should feel right at home with extensions pretty quickly; we'll put that to the test right now by walking through the construction of a simple extension that will allow the user to change the background color of the current webpage.

<br />
Now we know that with **HTML, CSS and Javascript** we can create chrome extension. But..... why not **Reactjs**? So, let's try with react.
<br /><br />

<h3>Create new project</h3>
Create new project and go to project directory:
<br />
```bash
create-react-app react-chrome-extension && cd react-chrome-extension
```
<br />
Then, there will be something that we must have to make chrome browser recognise our created extension. That is `manifest.json`. Actually, our react default project already included in `public/` directory like this:
<br />
```javascript
// public/manifest.json

{
  "short_name": "React App",
  "name": "Create React App Sample",
  "icons": [
    {
      "src": "favicon.ico",
      "sizes": "64x64 32x32 24x24 16x16",
      "type": "image/x-icon"
    }
  ],
  "start_url": "./index.html",
  "display": "standalone",
  "theme_color": "#000000",
  "background_color": "#ffffff"
}
```
<br />

But for chrome extension, it needs different config for `manifest.json`.
<br /> 

![](/chr-ext-1.png)
<br /> <br />

Delete old config and replace with new simple config as:
<br />
```javascript
// public/manifest.json

{
    "short_name": "Kphetdev.me",
    "name": "Kphetdev.me Extension",
    "manifest_version": 2,
    "browser_action": {
        "default_popup": "index.html",
        "default_title": "Kphetdev Extension"
    },
    "permissions": [
        "activeTab",
        "storage"
    ],
    "version": "1.0"
}
```
<br />

By the way, you can found more manifest attributes at [https://developer.chrome.com/extensions/manifest](https://developer.chrome.com/extensions/manifest).
<br /><br />

<h3>Build and Enjoy!</h3>
Running `yarn build` to build project and built will be in `build/` directory.
<br />

In Chrome, open extension:
<br />

![](/chr-ext-2.png)
<br /> <br />

Don't forget to check Developer Mode on top right page. Then, Click `Load Unpacked extension` to install our react app.
<br />

![](/chr-ext-3.png)
<br /> <br />

Go to our project and choose `build/` directory.
<br />

![](/chr-ext-4.png)
<br /> <br />

Finally, if you look at Toolbar you will see new extension there. And surprisingly, it's working!
<br />

![](/chr-ext-5.png)
<br /> <br />

Now we know, and for further guide to publish you can look at [Publish in the Chrome Web Store](https://developer.chrome.com/webstore/publish).