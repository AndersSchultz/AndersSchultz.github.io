---
layout: post
title: Getting a basic webb application up and running
---

### This tutorial covers what goes into a basic web application covering all aspects of it.

- Source control (Git)
- Build tools
- Front end framework (Mithril.js)

This tutorial will get us up and running with an SPA (single page application) that uses Mithril.js to render HTML in the browser. I am using Mithril.js because it is very fast (currently do not know of anything faster), light-weight, quick and easy to get started with, well documented and very well thought out.

This tutorial is a starting point. In upcoming installments I will show how to make the website absolutely SEO friendly (by utilizing SSR (server side rendering)) and even faster (using pre-rendered files). It will score 100% in Google PageSpeed, a pass in the Mobile-Friendly test and Excellent in Mobile Speed test. Such scores are not difficult to achive but most sites still fail to achieve them (at least what google PageSpeed is concerned). Mostly, I think, this is because of the currently prevailing CMS systems. If I continue long enough with my tutorials I will be adding CMS functionality to the website - without affecting the scores (that is the aim at least).

Besides the website itself I will go through the entire "stack" of tools and technologies involved. So, if you are a relatively new developer or just new to the things I work I hope this will all be of interest.

Let's get started. First of all we need our environment set up.

First things first. Let's set up Git so that we can benefit from having a safe external repository of our code as well as revision control, etc. As this will be an Open Source project I am placing my repository for it on Github.

I am using Visual Studio Code as my code editor of choice. I have been using Sublime Text for the last couple of years. I am happy with it but have not failed to notice all the good things being said about Visual Studio Code. So, for now I taking it for a spin. One of the great features is that it comes with in-built ability to work with Git repositories.

For starting up a new project I followed these steps:

1. Created repository on Github
2. Copied the repository URL
3. In Command Palette, typed: git clone, pressed Enter and pasted the repository URL.
4. Entered username and password for Github

After that my repository was availabe from within VS Code :-) 

For the above to work you need to have GIT installed on your system. You should have no problem finding a tutorial online to follow if you need help. Also, feel free to contact me if you need any help with this.

Lets initialize our Node application so our package.json file gets created:

```
npm init -y
```

(Note, I am assuming you are familiar with and running Node.js already and know how to use the npm (the Node package manager). If not, you will easily find tutorials covering this.)

As a package manager I am currently using webpack, so this is the first then we install:

```
npm install --save-dev webpack
```

If interested, look here for more [details about installing webpack](https://webpack.js.org/guides/installation/) from the official documentation

To install Mithril we do:

```
npm install mithril --save
```

structure:

```
- index.html
- src/
    - index.js
```

Other npm modules we will need:

```
npm install --save lodash
```

The easiest way to make your first post is to edit this one. Go into /_posts/ and update the Hello World markdown file. For more instructions head over to the [Jekyll Now repository](https://github.com/barryclark/jekyll-now) on GitHub.