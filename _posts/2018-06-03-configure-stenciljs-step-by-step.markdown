---
layout: post
title:  "Configure StencilJS from scratch step by step"
date:   2018-06-03 01:45:21 +0200
categories: stenciljs
---

[StencilJS][stencil-js] is a latest offering from [ionic][ionic]. It is not another javascript framework but its just a compiler to generate web components. There are many reasons to choose StencilJS as compiler for web components as mentioned below. 

1. Virtual DOM
2. Async Rendering
3. Reactive data-binding
4. Typescript
5. JSX

It generates independent webcomponent which are not bounded with any js framework. You can simply import compiled JS files for a particular component in web app project and can use custom web component just like any native html tags.

For example if i have created a custom web component named as `<my-fancy-name></my-fancy-name>` i can simply import its corresponding JS files in my html file and then i can refer this component in my html file and browser will be able to identify this tag as known tag.

Let's achieve this by example. I will guide you through step by step process on how to setup stenciljs project.

Step 1. Setting up npm
---
* Create directory and navigate to that directory
{% highlight terminal %}
$ mkdir mystencildemo
$ cd mystencildemo
{% endhighlight %}
* Initializing NPM
{% highlight terminal %}
$ npm init
{% endhighlight %}
Run above command and follow on-screen instructions.

* Install @stencil/core as first dependency
{% highlight terminal %}
$ npm install @stencil/core
{% endhighlight %}

This is the only minimal dependency to compile stencil component. Later we will see advanced configuration. 

Now open package.json and add below script in scripts section to package.json.
{% highlight javascript %}
"build":"stencil build",
{% endhighlight%}
After adding above snippet to package.json it will look like below.
{% highlight javascript %}
...
 "scripts": {
    "build":"stencil build",
    "test": "echo \"Error: no test specified\" && exit 1"
  },
...
{% endhighlight%}

Step 2. Building project
---
Now lets try to build our project. Run `npm run build` and see output. You will see below error.
{% highlight terminal%}
> stencil build

[05:09.1]  @stencil/core v0.8.2 🎡
[05:09.1]  build, app, prod mode, started ...
[05:09.1]  compile started ...
[05:09.1]  compile finished in 1 ms

[ ERROR ]  ENOENT: no such file or directory, scandir '/Users/ntilva/Documents/labs/github/blog-stencildemo/src'

[05:09.1]  build failed in 17 ms

npm ERR! code ELIFECYCLE
npm ERR! errno 1
npm ERR! stenciljs-from-scratch-demo@1.0.0 build: `stencil build`
npm ERR! Exit status 1
npm ERR! 
npm ERR! Failed at the stenciljs-from-scratch-demo@1.0.0 build script.
npm ERR! This is probably not a problem with npm. There is likely additional logging output above.

npm ERR! A complete log of this run can be found in:
npm ERR!     /Users/ntilva/.npm/_logs/2018-05-14T10_05_09_135Z-debug.log
{% endhighlight%}

Stencil required src as root folder where it can look for component definitions.

Lets add *src* folder in our project root folder
{% highlight terminal%}
$ mkdir src
{% endhighlight %}

And run `npm run build` and see output again.

Wohoo....This time we have compilation successful 🎉🎉. 

Step 3. Creating first component
---
We dont have anything in our src directory. Let's add our first component to src folder. 

I will create new component in a folder. So insider src folder lets create new folder *my-first-webcomponent*. In this folder create a new file and name it as my-first-webcomponent.tsx. 

You must be wondering why .tsx? Yes its not a typo its a typescript with JSX. Cool huh!!

{% highlight javascript %}
//my-first-webcomponent.tsx
import { Component } from '@stencil/core';
@Component({
    tag: 'my-first-webcomponent'
})
export class StencilComponent {
    render() {
        return (
            <p>My name is Stencil</p>
        );
    }
}
{% endhighlight %}

Run `npm run build` and see output again. Hooray we have our first web component compiled. 

Step 4. Integrate generated component
---
We have our first web component ready but how to validate it? How to integrate it. Its very simple.

Along with build folder create an index.html file as shown below.
{% highlight HTML %}
<!-- index.html -->
<!DOCTYPE html>
<html dir="ltr" lang="en">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, minimum-scale=1.0, maximum-scale=5.0">
  <title>Stenciljs from scratch</title>
  <script src="/build/app.js"></script>
</head>
<body>

    <my-first-webcomponent></my-first-webcomponent>

</body>
</html>
{% endhighlight %}

If `http-server` is installed just run `$ http-server' command where index.html file you have created. if `http-server` not installed just run `npx http-server`. npx allows user to run any node module without downloading it. 

Navigate to browser and you will see our first component in action.

[stencil-js]: https://stenciljs.com
[ionic]: https://ionicframework.com/
