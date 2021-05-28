---
title: first_hexo
tags: hexo_tutorial
---

## First Hexo

This is my first time to use hexo. I'm trying to record what I did. I will not talk the detail like how to make a template or something. Just talk about install and deploy on gh-pages.

Here's some website you may need.
[Hexo's official site](https://hexo.io/docs/writing)

I've already install the [Node.js](https://nodejs.org/en/) and [git](https://git-scm.com/)
I used **yarn** just like npm but faster (using npm is just do the same things)

Just like the official tutorial installing, I use
`npm instal hexo-cli -g`
(I still didn't understand how to yarn global to command line, so just use npm here)
Then open the folder with VScode. It may an empty folder now.
And enter `yarn install` in you termainal.
Now, there should be something in this folder.
Could check the detail of these in the official web if you want.

**We still not deploy the blog on gh-pages and this is just like create an app to help you generate the static website.**

## Let's deploy to the gh-pages

Use the [One-Command Deployment](https://hexo.io/docs/one-command-deployment)
I spent much time to try to know the official deployment, but I couldn't understand. So why not use this convenient tool.

First install the [hexo-deployer-git](https://classic.yarnpkg.com/en/package/hexo-deployer-git).
`npm install hexo-deployer-git`

I forgot to say the git repository name should be
**_username_.github.io**

Edit **\_config.yml** in your folder. It's empty on the **deploy** config now.

```
deploy:
        type:
```

change to

```
deploy:
  type: git
  repo: https://github.com/wcc356/wcc356.github.io
  branch: gh-pages
  message: "Site updated: {{ now('YYYY-MM-DD HH:mm:ss') }}"
```

The repo is the repository you built.

`yarn build` or `hexo generate`
now, we build the static website.

And we can deploy the website to gh-pages now
use
`yarn deploy` or `hexo deploy`
There's no differnt on these two commends, yarn deploy just a method to execute the `hexo deploy`, check the 'package.json' file in your folder.

```
"scripts": {
    "build": "hexo generate",
    "clean": "hexo clean",
    "deploy": "hexo deploy",
    "server": "hexo server"
  },
```

these are the script when you use `yarn "scripts_name"` what is going to happen. Dont change the file if you don't need.(if use npm will be `npm run 'scripts_name'`)

Finall, check your website on you github-pages. Sometimes it may need serveral minutes.
Just use the generate and deploy every time you update the new post or change the template, or more complicated things I still don't know.

---
