---
title: First Hexo
date: 2021-05-27 23:26:43
tags: hexo_tutorial
---

This is my first time using hexo. I'm trying to record what I did. I will not talk about the details like how to make a template or something. Just talk about installing and deploying on gh-pages.

Here's some websites you may need.
[Hexo's official site](https://hexo.io/docs/writing)

I've already install the [Node.js](https://nodejs.org/en/) and [git](https://git-scm.com/)
I used **yarn** just like npm but faster (using npm is just do the same things)

Just like the official tutorial installing, I use
`npm instal hexo-cli -g`
(I still didn't understand how to yarn global to command line, so just use npm here)
(2021.05.30 I knew how to set global command line, will make a new post to talk about this)
Then open the folder with VScode. It may be an empty folder now.
And enter `yarn install` in your terminal.
Now, there should be something in this folder.
Could check the details of these in the official web if you want.

**We still do not deploy the blog on gh-pages and this is just like creating an app to help you generate the static website.**

## Let's deploy to the gh-pages

Use the [One-Command Deployment](https://hexo.io/docs/one-command-deployment)
I spent a lot of time trying to know the official deployment, but I couldn't understand. So why not use this convenient tool?

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
Now, we build a static website.

And we can deploy the website to gh-pages now
use
`yarn deploy` or `hexo deploy`
There's no difference between these two commands, yarn deploy is just a method to execute the `hexo deploy`, check the 'package.json' file in your folder.

```
"scripts": {
    "build": "hexo generate",
    "clean": "hexo clean",
    "deploy": "hexo deploy",
    "server": "hexo server"
  },
```

This is the script when you use `yarn "scripts_name"` what is going to happen. Don't change the file if you don't need it.(if use npm will be `npm run 'scripts_name'`)

Finally, check your website on your github-pages. Sometimes it may take several sec.
Just use the generate and deploy every time you update the new post or change the template, or more complicated things I still don't know.

---

The first version [site](https://wcc356.github.io/) will no update, but I will not delete it as a experience.

2021.5.29 update
Finally, I know what the official website text means.
I Only have to push my all hexo files to one repo (the official's branch is `source` but this is just a convention, mine is named **main** lol)

check your folder connect to the repo then

#### the step 4 on hexo gh-pages text

setting the CI workflow on the git.
It means when you push to the branch then do these things automatically.
(CI = continuous Integration)

Add .github/workflows/pages.yml file to your repo with the following content:
**Just copy these text to your new file which just made**

```
name: Pages

on:
  push:
    branches:
      - source  # default branch


jobs:
  pages:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Use Node.js 12.x
        uses: actions/setup-node@v1
        with:
          node-version: '12.x'
      - name: Cache NPM dependencies
        uses: actions/cache@v2
        with:
          path: node_modules
          key: ${{ runner.OS }}-npm-cache
          restore-keys: |
            ${{ runner.OS }}-npm-cache
      - name: Install Dependencies
        run: npm install
      - name: Build
        run: npm run build
      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./public
          publish_branch: master  # deploying branch

```

The only two variable you need to change is

1. source should be your own branch name when you pushed
   means when you push then do the following work.

```
on:
  push:
    branches:
      - main
```

2. publish_branch is your deploy branch.
   I changed it to `gh-pages`, just up to you

```
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./public
          publish_branch: gh-pages
```

Long story short, the one command deployed is just for someone who doesn't want to other's read his hexo files(like templates or something).
