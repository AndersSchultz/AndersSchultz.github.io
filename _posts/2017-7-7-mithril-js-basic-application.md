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

This tutorial will get us up and running with an SPA (single page application) that uses Mithril.js to render HTML in the browser. I am using [Mithril.js](https://mithril.js.org) because it is very fast (currently do not know of anything faster), light-weight, quick and easy to get started with, well documented and very well thought out.

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

First create a file called webpack.config.js and enter the following:

``` javascript
var path = require('path');// path module is used which helps us resolve paths properly especially across different operating systems

module.exports = {
  entry: './src/index.js',//The file that is the starting point of all processing
  output: {
    filename: 'bundle.js',//Name of the output file
    path: path.resolve(__dirname, 'dist')//The directory into which the resulting files will be placed
  }
};
```
The code basically tells webpack to index.js as the entry file and output the result of the build process in a file called bundle.js (in a folder named "dist"). What webpack does as part of its build process is to look in the entry file and take all the javascript from there plus all the script imported from other files through the 'import' or 'require' method.  

Then add the following code to the package.json file

``` javascript
  "scripts": {
    "build": "webpack"
  }
```

This allows us to build the application using the `run` npm command. Npm will look up our build command and execute its content which is "webpack". This will in turn cause Node.js to run the `webpac`k command. Webpack will look for a configuration file and find the one you just created - and then build according to its content.

It might seem tedious to do it this way instead of using webpack directly from the command line. However, having a list with build scripts will come in handy as our app gets more complex and more complex build actions will be added. Also, we cannot run webpack straight from the command line without navigating to the folder where it is located. Using npm we are able to have a single command called `build` and npm will take care of finding and executing the webpack executable at the right location.

With this in place we can now build our project using npm

```
npm run build
```

You should soon see some output that lists the assets which have just been built. In this case our bundle.js file (which you will also now find in the 'dist' folder)

To see our website in action we can take advantage of a web-server running in the context of VS Code. To do this you need to install a web server extension. I am currently using this one: vscode-preview-server. So, go ahead and install it unless you already have a dev server in place.

With a web-server installed, you can now select index.html in VS Code and launch it in the default browser.

Using webpacks own build server npm i --save-dev webpack-dev-servers
- runs code from memory not from disc
- changes will be processed on the fly by webpack and the browser page will reload automatically

At this point we have a rudimentary development infrastructure in place and our code under source control.

### Time to bring some style into our website

Let's add a CSS library to our enviromnet. Currently, I am testing [mini.css](http://minicss.org)

To get it added to our project we can once agin rely on npm:

```
npm install mini.css --save-dev --save-exact 
```

Now, it can be imported it like any other module. Add this to your index.js file:

```
import 'mini.css/dist/mini-default.css'
```

Now webpack knows that it should require your css file and add them to your application.

However, webpack does not handle CSS out of the box. If you bild your application now with webpack you will get an error message saying that it is not know how to process the css files. It kind of does not know what it is and what to do with it. 

To make it wiser some configuration, some loaders and a plugin is necessary.

Install the following three modules:

```
npm install --save-dev --save-exact css-loader style-loader extract-text-webpack-plugin
```

The first module `css-loader` handles assets in your CSS (referenced by `@import` and `url()`) and makes them available for further processing.  

The second module `style-loader` adds the CSS to the DOM by injecting a `<style>` tag in the header.  

So, With these loaders webpack is able to take styles referenced by the `import` command and add it to the JavaScript bundle. When running our application, the styles will be inserted into the web page in the header section inside a `<style>` tag.

Though, as we have a rather substatial style sheet (even though mini.css is a small library, it still holds a lot of styling in it) I prefer to have the styles seperated out into a separate file instead of being added into the Javascript file and inserted into the DOM at runtime. The seperate file can be referenced as a regular `<link rel="stylesheet">` tag in the header. This seems like a more clearn approach and has the added benefit of allowing the browser to load the styles in parallel with the JavaScript bundle. Consequently, with a lot of styles the website will load faster. Later we will also make good use of this approach when we will optimize the loading speed of the website further by having the majority of the styles loaded after the intial load of the website (to be done in an upcoming tutorial).

The third module `extract-text-webpack-plugin` on the list enables webpack to take the styles and place them into a separate file.

To instruct webpack to use the modules we must change our configuration file so it now looks like this:

``` javascript
const ExtractTextPlugin = require("extract-text-webpack-plugin");//The plugin is `required` into a variable 

var path = require('path');

module.exports = {
  entry: './src/index.js',
  output: {
    filename: 'bundle.js',
    path: path.resolve(__dirname, 'dist')
  },   
  module: {
    rules: [
      {
        test: /\.css$/,//This is a regular expression that matches all files ending in `.css`
        use: ExtractTextPlugin.extract({//Here the ExtractTextPlugin is used by calling its `extract` method. It takes the result of the css-loader and extracts it into a file.
          fallback: "style-loader"//style-loader is used as a fallback (if ExtractTextPlugin is disabled)
          use: "css-loader"//css-loader is assigned as being responsible for processing the CSS files
        })
      }
    ]
  },
  plugins: [
    new ExtractTextPlugin("styles.css"),//The plugin is initialized with a file name to use when extracting.
  ]
};
```

The new parts of the configuration is explained with comments above. The reason for the fallback assignment is so that the style loader can be used instead of the ExtractTextPlugin. By having this in place we could disable the ExtrctTextPlugin (fx. during development mode) and have styles added to the <header> tag.

## Getting into Mithril.js ##

So far we have just used Mithril.js to render a bit of text to a page. Just so we had something to bundle and build. Now it's time to create the basic infrastrcture for our application.





This tutorial is being written as I am creating the application. So, if you happen to read it now I apologize for it not being finalized. You are reading a work in progress :-) 

notes regarding upcoming things:

Adding image support:

```
npm install --save-dev file-loader
```
+       {
+         test: /\.(png|svg|jpg|gif)$/,
+         use: [
+           'file-loader'
+         ]
+       }

Other npm modules we will need:

```
npm install lodash --save --save-exact
```

Interesting resources:

[Good habits for working with node](https://blog.heroku.com/node-habits-2016)
[Guidelines for writing Javascript](https://www.gitbook.com/book/duk/airbnb-javascript-guidelines/details)