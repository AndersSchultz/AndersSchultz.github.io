---
layout: post
title: Basic Mithril.js web application 
---

### This tutorial shows how to create a basic web application covering the following asepcts:

- Source control (Git)
- Build system and package management (Node.js, npm, webpack)
- Front end framework (Mithril.js)
- Server side environment - (Hapi.js - one of the multiple web servers running on Node.js)
- Basic parts of a modern, responsive web application

This tutorial will get us up and running with an SPA (single page application) that uses Mithril.js to render HTML in the browser. I am using Mithril.js because it is very fast (currently do not know of anything faster), light-weight, quick and easy to get started with, well documented and very well thought out.

This tutorial is a starting point. In upcoming installments I will expand on the app and show how to make the website absolutely SEO friendly (by utilizing SSR (server side rendering)) and even faster (using pre-rendered files). It will score 100% in Google PageSpeed, a pass in the Mobile-Friendly test and Excellent in Mobile Speed test. Such scores are not difficult to achive but most sites still fail to achieve them (at least what google PageSpeed is concerned). Mostly, I think, this is because of the currently prevailing CMS systems. If I continue long enough with my tutorials I will be adding CMS functionality to the website - without affecting these scores (that is the aim at least).

Besides the website itself I will go through the entire "stack" of tools and technologies involved. So, if you are a relatively new developer or perhaps new to the things I work with I hope very much this and the upcoming tutorials will be of interest.

Let's get started. First of all we need our environment set up.

### Setting up source control for our project

First things first. Let's set up Git so that we can benefit from having a safe external repository of our code as well as revision control, etc. As this will be an Open Source project I am placing my repository for it on Github.

I am using Visual Studio Code as my code editor of choice. I have been using Sublime Text for the last couple of years. I am happy with it but have not failed to notice all the good things being said about Visual Studio Code. So, for now I taking it for a spin. One of the great features is that it comes with in-built ability to work with Git repositories.

For starting up a new project in VS Code follow these steps:

1. Create a repository on Github
2. Copy the repository URL
3. In Command Palette, type: git clone, press Enter and then write the local folder where you want your project to be stored.
4. Enter username and password for Github

After that you will have a local Git "enabled" folder that is synched with your Github project. Now you can work with your project locally from within VS Code and quickly and easily update your Github repository with your latest changes. 

(NB: If you do not want to open source your application or simply would like to keep it private for now, as an alternative to Github you can use [Bitbucket](https://bitbucket.org) where you can create private repositories for free.)

For the above to work you need to have Git installed on your system. You will have no problem finding a tutorial online to follow if you are new to Git. Also, feel free to contact me if you need any help with this.

### Setting up our development infrastructure and building our project 

Now, Let's set up our local development infrstructure so that we can better manage and build our project.

(If you are reading this tutorial, odds are that you are familiar with Node.js and npm and already have them installed. Otherwise, take some time to familiarize yourself with them and get them up and running.) 

To create the scaffold for our application, so our package.json file gets created, use your terminal (navigate to your folder) and type:

```
npm init -y
```

As a package manager I am currently using webpack, so this is the first thing we install:

```
npm install webpack --save-dev --save-exact
```

If interested, look here for more [details about installing webpack](https://webpack.js.org/guides/installation/) from the official documentation

To install Mithril we do:

```
npm install mithril --save --save-exact
```

(I am using the --save-exact flag to ensure that the versions of the modules will be kept consistent across my environments. See [node habits](https://blog.heroku.com/node-habits-2016) for more explanation)

Now, create an index.html and index.js file in your project. Use this structure:

```
- index.html
- src/
    - index.js
```
Add this to your html file:

``` html
<html>
  <head>
    <title>Web app says hello</title>
  </head>
  <body>
    <script src="bundle.js"></script>
  </body>
</html>
```

The key thing here is that we are adding a file called bundle.js to our web page. The bundle.js file will be a single file that will hold all of our application logic. This has the advantage of dimishing the files that will be loaded by the browser and allows us to skip adding all the javascript files manually.

Add this to the index.js file

``` javascript
var m = require("mithril")
m.render(document.body, "hello world")
```

Here we are first requiring the Mithril framework. Then we use the render method to inject a simple "hello world" message into the body of our html page.

Now, let's build our application with webpack.

First add the following code to the package.json file

``` javascript
  "scripts": {
    "build": "webpack"
  }
```

This allows us to build the application using a npm command

Then create a file called webpack.config.js

and enter the following:

var path = require('path');

``` javascript
module.exports = {
  entry: './src/index.js',
  output: {
    filename: 'bundle.js',
    path: path.resolve(__dirname, 'dist')
  }
};
```

The code basically tells webpack to index.js as the entry file and output the result of the build process in a file called bundle.js (in a folder named "dist"). What webpack does as part of its build process is to look in the entry file and take all the javascript from there plus all the script imported from other files through the 'import' or 'require' method.  

With this in place we can now build our project using npm

```
npm run build
```

This should result in an output that lists the assets which have been built. In this case just our bundle.js file (appearing in the 'dist' folder)

To see our website in action we can take advantage of a web-server running in the context of VS Code. To do this you need to install a web server extension. I am currently using this one: vscode-preview-server
```

With a web-server installed, you can now select index.html in VS Code and launch it in the default browser.

At this point we have a full production environment and with our code under source control.




This tutorial is being written as I am creating the application. So, if you happen to read it now I apologize for it not being finalized. You are reading a work in progress :-) 


Other npm modules we will need:

```
npm install lodash --save --save-exact
```

Interesting resources:

[Good habits for working with node](https://blog.heroku.com/node-habits-2016)
[Guidelines for writing Javascript](https://www.gitbook.com/book/duk/airbnb-javascript-guidelines/details)