---
layout: post
title:  "Starting functional programming with Elm"
date:   2022-01-07
categories: [elm]
tags: [functional, programming, elm]
---

## Programming with Elm
This is a blog series about functional programming with Elm.

### Why start programming with Elm?
I am a software engineer for a long time and have been programming in an Object Oriented way my whole career, mostly in Java. I like discovering new things and for a time that was mostly Java related. But while there was a lot of development around Java(not much in the language itself), it felt like more of the same. A new library here and there but mostly on known concepts. When I learned to program for the frontend, a whole new world opened. It felt like Java in the early days. Lots of frameworks and libraries popping up, great. 

#### Functional programming
Lots of these new frameworks and libraries were about functional programming. Even Java received functional programming features. They were easy to use, albeit in a different way. It peaked my interest, what is that, real functional programming? By the way it is not a new concept. it exists for a long time, but somehow it is popping up everywhere. So I wanted to do functional programming. But where and in what language? I could go for the backend (there are multiple candidates, like frege and eta), but I choose the frontend, because I needed a more stable framework/language

### What is Elm?
Elm is a functional programming language for the frontend. Or as they say on the website, 'A delightful language for reliable webapps.' The most important features are 'No runtime exceptions', 'Great performance', 'Enforced semantic versioning', 'Small assets', and 'Javascript interop'. It compiles to javascript. 

### The goal
The goal is to make a desktop application that can read json files from the file system and can display it on the screen. That means not only the challenge of learning Elm, but also to create an application with electron and Elm.

#### The simple guide
I looked on the web for combinations of electron and elm and found Elm electron webpack. So I forked it and cloned the git repository. It was more a guide than a ready to use template. And that was a good thing. It started simple, using only electron. Then mixing in Elm and finally webpack. 

##### Electron
Getting electron up and working was very simple. In the index.html add or remove some text to see something else. Then fire up electron main.js (or npx electron main.js if you installed it locally) and a window with the text and title should show up. A good start.

##### Bringing Elm into the fold
The elm part was also no problem, the guide use Elm 0.18 and I had already installed elm 0.19. But that was not a problem, because it does not use very much of Elm. The guide let's you build the elm bundle before changing the elm.json file, so it is possible that when you execute 

{% highlight javascript%}
elm make src/elm/Main.elm --output src/static/bundle.js
{% endhighlight %}

nothing is produced and an error is shown:

<figure><pre style="background-color: black;"><code style="background-color: black;color: #66d9ef;border: none;font-size: x-small">
Detected a problem.
-- UNEXPECTED FILE NAME --------------------------------------------------------

I am having trouble with this file name:

    src/elm/Main.elm

I found it in your /home/andre/git/repo/starting-with-elm/src/ directory which
is good, but I expect all of the files in there to use the following module
naming convention:

    +--------------+-------------------------------------------------------------+
    | Module Name  | File Path                                                   |
    +--------------+-------------------------------------------------------------+
    | Main         | /home/andre/git/repo/starting-with-elm/src/Main.elm         |
    | HomePage     | /home/andre/git/repo/starting-with-elm/src/HomePage.elm     |
    | Http.Helpers | /home/andre/git/repo/starting-with-elm/src/Http/Helpers.elm |
    +--------------+-------------------------------------------------------------+

Notice that the names always start with capital letters! Can you make your file
use this naming convention?

Note: Having a strict naming convention like this makes it a lot easier to find
things in large projects. If you see a module imported, you know where to look
for the corresponding file every time!
</code></pre></figure>

So apply the change that is posted later in the guide, update the elm.json file to find your elm files. 

{% highlight json %}
"source-directories": [
    "src/elm"
],
{% endhighlight %}

Then fire up 'electron main.js' and it should work. Except it didn't. There was a browser error
<figure><pre style="background-color: black;"><code style="background-color: black;color: #66d9ef;border: none;font-size: x-small">Uncaught ReferenceError: require is not defined
    at index.html:11
</code></pre></figure>
This is because of a later version of electron is used compared to the guide. The new version separates the browser process from the node process.

A fix is to use the config option 'contextIsolation: false' in the 'webPreferences' part of 'new BrowserWindow' options.
It does make electron less safe, because the client and server part are in the same context now.
{% highlight javascript %}
function createWindow () {
  mainWindow = new BrowserWindow({
    width: 1024,
    height: 768,
    webPreferences: {
        nodeIntegration: true, 
        contextIsolation: false
    }
  })
{% endhighlight %}

Now we can develop an application with elm and electron.
Use 

{% highlight javascript %}
elm reactor
{% endhighlight %}

to enhance the app and 

{% highlight javascript %}
elm make src/elm/Main.elm --output src/static/bundle.js
electron main.js
{% endhighlight %}

to check it in electron

To make life easier there are scripts for npm in the package.json file

To start the elm reactor and launch a webbrowser (firefox) on http://localhost:8000
{% highlight javascript %}
npm run elm
{% endhighlight %}
PS: This might not work on Windows, because of the chaining of commands

To build elm and start electron
{% highlight javascript %}
npm run electron
{% endhighlight %}
PS: This might not work on Windows

To start elm reactor without opening a browser window
{% highlight javascript %}
npm run reactor
{% endhighlight %}

To build elm
{% highlight javascript %}
npm run build
{% endhighlight %}

To start electron without building elm
{% highlight javascript %}
npm run start
{% endhighlight %}


### The conclusion
I am glad that in the end I got it working with Elm 0.19 and electron. The guide helped me a lot to understand all the moving parts. In the next parts we can start building an application. 

### What about webpack?
The original guide included webpack. The version of webpack used was version 1. The elm-loader for webpack version 1 does not support Elm 0.19. Since I wanted to use the latest version of Elm this was not an option.

I tried to make it work with the latest version of webpack, but this was not a simple task.
(If you want to see the [attempt](https://tikal86.github.io/elm/failed-webpack-configuration)), but not a successful one.
But since this is about Elm and not webpack, this is not a big problem.

### References

[Elm](https://elm-lang.org/)

[The Elm guide](https://guide.elm-lang.org/)

[The original Elm electron webpack guide](https://github.com/johnomarkid/elm-electron-webpack)

[The code](https://github.com/tikal86/starting-with-elm.git)
