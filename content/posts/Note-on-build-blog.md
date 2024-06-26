---
title: "Note on A Simple Way to Set Up A Website"
date: 2024-06-26T10:20:07-08:00
draft: false
---

## Overview
Hugo: Website Generator.<br>
GitHub Page: to host your website.<br>
GitHub Actions Workflow: to build and deploy your website.

## Prerequisite
- Sign up a GitHub account
- [Install Hugo](https://gohugo.io/installation/)
- [Install Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)

## Step-by-Step Tutorial
Step1: create a new public repository.<br>
Step2: Create a new site with hugo.<br>
```
hugo new site space
```
Step3: Init local git and choose a hugo theme.<br>
There are many themes provided [here](https://themes.gohugo.io/).
Choose one you like.Take [anatole](https://github.com/lxndrblz/anatole) for an example.
hugo new site site-name, 
site name is the blog's name you name it.

```
cd space
git init
git add -A
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/Susy-eng/vspace.git
git push -u origin main
git submodule add https://github.com/lxndrblz/anatole.git themes/anatole
```
Step4: Edit hugo config in file hugo.toml
Change baseURL to your own one.
```
baseURL = "https://<USERNAME>.github.io/<REPOSITORY_NAME>/"
languageCode = "en-us"
title = "My New Hugo Site"
```
An example :
```
baseURL = "https://Susy-eng.github.io/vspace"
languageCode = "en-us"
title = "Blog"
```
For the rest configuration, following [this](https://github.com/lxndrblz/anatole/wiki/1%EF%B8%8F%E2%83%A3-Essential-Steps#setting-up-a-favicon).

Step5: Push local changes to remote repository.
```commandline
git add hugo.toml
git commit -m "Edit configuration file"
git push origin main
```
And them use command `hugo` to check if the website okay.
You will see something similar as the following:
```commandline

                   | EN  
-------------------+-----
  Pages            |  8  
  Paginator pages  |  0  
  Non-page files   |  0  
  Static files     |  6  
  Processed images |  0  
  Aliases          |  1  
  Cleaned          |  0  

Total in 176 ms

```

Step6: Config GitHub Actions Workflow
Refer to [Set Up GitHub Actions Workflow](https://chrisjhart.com/Creating-A-Simple-Free-Blog-Hugo/).
```commandline
mkdir -p .github/workflows
cd .github/workflows
vim deploy_gh_pages.yaml
```
Example yaml file
```commandline
---
name: Deploy Hugo site via GitHub Pages

on:
  push:
    branches:
      - main # Set a branch to deploy
  pull_request:

permissions:
  contents: write

jobs:
  deploy:
    runs-on: ubuntu-22.04
    steps:
      - uses: actions/checkout@v2
        with:
          submodules: true # Fetch Hugo themes (true OR recursive)
          fetch-depth: 0 # Fetch all history for .GitInfo and .Lastmod

      - name: Setup Hugo
        uses: peaceiris/actions-hugo@v2
        with:
          hugo-version: "latest"
          extended: true

      - name: Build
        run: hugo --minify

      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        if: github.ref == 'refs/heads/main'
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./public
```
Then push your changes to remote repository.
```commandline
git add .github/workflows/deploy_gh_pages.yaml
git commit -m "Config GitHub Actions workflow"
git push origin main
```
Step7: Config GitHub Pages to host your website.
Settings->Pages->deploy from branch (choose gh-pages)->Save

After deployment, your blog site is on the top. 
Copy and paste it on the About section of your repository to make you find it easily.

This post is a note for self-learning from [Christopher Hart](https://chrisjhart.com/Creating-A-Simple-Free-Blog-Hugo/).