---
layout: post
title:  "Starting functional programming with Elm"
date:   2021-09-12 17:40:59
categories: [elm]
tags: [functional, programming, elm]
---

# Programming with Elm
This is a blog series about functional programming with Elm.

## Why start programming with Elm?
I am a software engineer for a long time and have been programming in an Object Oriented way my whole career, mostly in Java. I like discovering new things and for a time that was mostly Java related. But while there was a lot of development around Java(not much in the language itself), it felt like more of the same. A new librtary here and there but mostly on known concepts. When I learned to program for the frontend, a whole new world opened. It felt like Java in the early days. Lots of frameworks and libraries popping up, great. 

### Functional programming
Lots of these new frameworks and libraries were about functional programming. Even Java received functional programming features. They were easy to use, albeit in a different way. It peaked my interest, what is that, real functional programming? By the way it is not a new concept. it exists for a long time, but somehow it is popping up everywhere. So I wanted to do functional programming. But where and in what language? I could go for the backend (there are multiple candidates, like frege and eta), but I choose the frontend, because I needed a more stable framework/language

## What is Elm?
Elm is a functional programming language for the frontend. Or as they say on the website, 'A delightful language for reliable webapps.' The most important feautures are 'No runtime exceptions', 'Great performance', 'Enforced semantic versioning', 'Small assets', and 'Javascript interop'. It compiles to javascript. 

## The goal
The goal is to make a desktop application that can read json files from the file system and can display it on the screen. That means not only the challenge of learning Elm, but also to create an application with electron and Elm.

### The simple guide
I looked on the web for combinations of electron and elm and found Elm electron webpack. So I forked it and cloned the git repo. It was more a guide than a ready to use template. And that was a good thing. It started simple, using only electron. Then mixing in Elm and finally webpack. 

#### Electron
Getting electron up and working was very simple. In the index.html add or remove some text to see something else. Then fire up electron main.js (or npx electron main.js if you installed it locally) and a window with the text and title should show up. A good start.

#### Without webpack
Running without webpack is not a problem, the only thing is you need to restart the app every time.
{% highlight bash %}
    npm run start
{% endhighlight %}

#### Running only elm
Since it is not running without problems in electron, the latter problem can be fixed by not running it in electron and using the elm reactor.
{% highlight bash %}
    npm run start
{% endhighlight %}

## The conclusion
I am glad that in the end I got it working with Elm 0.19 and electron. The guide helped me a lot to understand all the moving parts.

## References

[Elm](https://elm-lang.org/)

[The Elm guide](https://guide.elm-lang.org/)

[The original Elm electron webpack guide](https://github.com/johnomarkid/elm-electron-webpack)
