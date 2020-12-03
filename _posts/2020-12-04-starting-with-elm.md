---
layout: post
title:  "Starting functional programming with Elm"
date:   2020-11-14 17:40:59
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
Elm is a functional programming language for the frontend. Or as they say on the website, 'A delightful language for reliable webapps.' The most important feautures are 'No runtime exceptions', 'Great performance', 'Enforced semantic versioning', 'Samll assets', and 'Javascript interop'. It compiles to javascript. 

## The goal
The goal is to make a desktop application that can read json files from the file system and can display it on the screen. That means not only the challenge of learning Elm, but also to create an application with electron and Elm.

### Too much moving parts
The first thing I did was searching for existing solutions of frameworks which use both elm and electron. There are quite a few and since I wanted to communicate both from Elm to frontend javascript and from frontend javascript to backend javascript (which uses the ipc part of electron) I chose Elm Electron Starter. It has all the communications needed but uses Typescript and webapck, which I don't have too much knowledge of. But it looked good and after the checkout it worked. The first challenge was, that it was using Elm 0.18 and I wanted to use the laterst versin, which is 0.19. Since the Elm compiler should be pretty helpful, I was up for the challenge. And it was not that difficult. But then it did start, but the Elm part did not show up anymore. After countless attempts of trying to fix this, I gave up. My lack of knowledge of Typescript, electron and webpack made it too difficult. 

### The simple guide
So I went looking for a simpler way and found Elm electron webpack. It was more a guide than a ready to use template. And that was a good thing. It started simple, using only electron. Then mixing in Elm and finally webpack. 

#### Upgrading elm 0.19
It also uses Elm 0.18, but the conversion was again easily done. The hardest part was choosing which function tio use from 'Browser'. The elm guide has a page for it that explaains the differences. For now Browser.element is enough and works.

But as before it did not show the elm part. 
The error was:
[Electron error](electron-error.png)


Since I could now test with only Elm and Javascript, it was easier to find and fix the problem. 
{% highlight java %}
    Observable.just("Hello observable without backpressure")
    .filter(text -> text.startsWith("Hello"))
    .subscribe(System.out::println);
{% endhighlight %}

#### Webpack
Then onto webpack, the first part went without problems, but the devserver did not. The latest version of webpack does not support the old dev server. I tried 'webpack serve' that did start without problems, but electron was never started and the files were not served to localhost. So even if electron was started, no Elm screen was shown.

#### Without webpack
Running without webpack is not a problem, the only thing is you need to restart the app every time.
{% highlight bash %}
    npm run start
{% endhighlight %}

#### Running only elm
Since it is no running without problems in electron, the latter problem can be fixed by not running it in electron and using the elm reactor.
{% highlight bash %}
    npm run start
{% endhighlight %}

## The conclusion
I am glad that in the end I got it working with Elm 0.19 and electron. The guide helped me a lot to understand all the moving parts.

## References

[Elm](https://elm-lang.org/)

[The Elm guide](https://guide.elm-lang.org/)

[Elm Electron Starter](https://github.com/dillonkearns/elm-electron-starter)

[The original Elm electron webpack guide](https://github.com/johnomarkid/elm-electron-webpack)

[My Elm electron webpack fork](https://github.com/tikal86/elm-electron-webpack)
