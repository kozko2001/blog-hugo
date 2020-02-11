---
title: "Basic webapp — bootstrap"
author: ""
date: 
lastmod: 2020-02-11T21:51:07+01:00
draft: true
description: ""

subtitle: "Each time we have to make a new webapp, the firsts steps are all the same and is really boring to make over and over, more if you are doing…"




aliases:
    - "/"
---

Each time we have to make a new webapp, the firsts steps are all the same and is really boring to make over and over, more if you are doing some side-project like myself and you just don’t want to spend time configuring webpack / babel / eslint etc… 

That’s why the scaffolding of webapps have become so popular lately, you have a **starter-kit** for almost anything imaginable, I have used these starter-kit but always got some problems with them:

*   Some are not well maintained and use old libraries (on a side project, I always want to have cut-edge technology!!)
*   Even when they are update, it’s a bit annoying how opinionated they are, and some time you just want to use some different defaults/libraries/code structure etc…
*   And for me the most important downside of using scaffolding is that you loss touch with the building technology like **babel**, **webpack, different loaders of webpack** etc… and you become a slave of the default stack the starter-kit has chose for you.

So let’s start by making a simple bootstrap of some code#### 1. yarn

Yarn is a tool to manage the project, just like **npm,** but it’s a lot faster at the time of resolving dependencies, also besides of using package.json for install the libraries we need, also uses a **yarn.lock** file which the resolved version of the library. Making the builds between computers much more stables. More info [https://yarnpkg.com/lang/en/](https://yarnpkg.com/lang/en/)
`brew install yarn`

#### 2. Create the project
`mkdir my_project  
yarn init`

Fill in the request values as the project name, version and license.

#### 3. Editor configuration

One of the first things I always do is to add a **.editorconfig** to any project, is just a moment, and will make sure that anybody that edits the project will use the same end of lines, spaces or tabs size etc… 

For more information about editorconfig file [http://editorconfig.org/](http://editorconfig.org/), I normally use sublime-text as my js editor and you just have to install an addon. [https://github.com/sindresorhus/editorconfig-sublime#readme](https://github.com/sindresorhus/editorconfig-sublime#readme)

So basically I always add a .editorconfig file to the root of my project with the following content
`root = true``[*]  
indent_style = space  
indent_size = 2  
charset = utf-8  
trim_trailing_whitespace = true  
insert_final_newline = true  
end_of_line = lf  
# editorconfig-tools is unable to ignore longs strings or urls  
max_line_length = 120`

#### 4. Install a basic webpack configuration

Webpack is one of this tools that you just need to master over time, it’s so huge that is really hard to master. But I feel they are on the right track with webpack 3.0 the configuration files have a lot more sense to me, and seem easier to use.

Webpack at the end is just a bundler, which means that will merge all your code in a single file, so you can develop with multiple files and nice code structure but the performance at the end is as good as possible. And we are not talking only about .js files, also the .css/sass/less files and even images so you don’t have to worry about any asset.
`yarn add webpack --dev`

The most basic configuration of webpack is the next one, where we define an entry js file and an output file.
``const path = require(&#39;path&#39;);  

module.exports = {  
  entry: &#39;./src/index.js&#39;,  
  output: {  
    filename: &#39;bundle.js&#39;,  
    path: path.resolve(__dirname, &#39;dist&#39;)  
  }  
};``
