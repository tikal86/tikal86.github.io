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

#### Bringing Elm into the fold
The elm part was also no problem, the guide use Elm 0.18 and I had already installed elm 0.19. But that was not a problem, because it does not use very much of Elm. The guide let's you build the elm bundle before changing the elm.json file, so it is possible that when you execute 

{% highlight bash %}
elm make src/elm/Main.elm --output src/static/bundle.js
{% endhighlight %}

nothing is produced and an error is shown:

{% highlight bash %}
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
{% endhighlight %}

So apply the change that is posted later. Update the elm.json file to find your elm files. 

{% highlight json %}
"source-directories": [
    "src/elm"
],
{% endhighlight %}

Then fire up electron main.js and it should work. Except is didn't. The browser gave an error
{% highlight json %}
Uncaught ReferenceError: require is not defined
    at index.html:11
{% endhighlight %}
This is because of a later version of electron.

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

{% highlight bash %}
elm reactor
{% endhighlight %}

to enhance the app and 

{% highlight bash %}
elm make src/elm/Main.elm --output src/static/bundle.js
electron main.js
{% endhighlight %}

to check it in electron

#### Webpack
Then onto webpack, the guide was written with an older version of webpack in mind. The config schema is changed and so the proposed config does not work. So webpack init was run to create a new config file. The follwing answers were given to the questions asked by webpack init:

{% highlight bash %}
? Which of the following JS solutions do you want to use? ES6
? Do you want to use webpack-dev-server? Yes
? Do you want to simplify the creation of HTML files for your bundle? Yes
? Do you want to add PWA support? Yes
? Which of the following CSS solutions do you want to use? CSS only
? Will you be using PostCSS in your project? No
? Do you want to extract CSS for every file? Only for Production
? Do you like to install prettier to format generated configuration? Yes
[webpack-cli] ℹ INFO  Initialising project...
 conflict package.json
? Overwrite package.json? do not overwrite
     skip package.json
   create src/index.js
 conflict README.md
? Overwrite README.md? do not overwrite
     skip README.md
   create index.html
   create webpack.config.js
   create .babelrc
{% endhighlight %}

After that change the entry in the webpack.config.js for entry, because webpack uses './src/index.js' as default.
And add the elm loader to the module/rules/ list. Luckily we can copy that paert from the guide

{% highlight json %}
{
    test:    /\.elm$/,
    exclude: [/elm-stuff/, /node_modules/],
    loader:  'elm-webpack?verbose=true&warn=true',
}
{% endhighlight %}

Now we need to add the plugins that webpack put in the config.
{% highlight bash %}
npm install html-webpack-plugin --save-dev
npm install mini-css-extract-plugin --save-dev
npm install workbox-webpack-plugin --save-dev
npm install babel-loader --save-dev
{% endhighlight %}

BTW if you npx webpack configtest it will show all the errors that there are.

Now there are no validation errors anymore, we can start webpack.
Unfortunately there is still an error when run:

{% highlight bash %}
[webpack-cli] Error: Compiling RuleSet failed: Query arguments on 'loader' has been removed in favor of the 'options' property (at ruleSet[1].rules[3].loader: elm-webpack?verbose=true&warn=true)
{% endhighlight %}

Apparently the loader options should be in a separate object:

{% highlight json %}
    {
        test:    /\.elm$/,
        exclude: [/elm-stuff/, /node_modules/],
        loader:  'elm-webpack',
        options: {
            verbose: true,
            warn: true
        }
    }
{% endhighlight %}

After specifying the filename of the bundle in the output options, webpack created bundle.js 

#### Webpack devserver
Running npx webpack serve, it complained that the devserver was not installed, but it suggested to install it. So that was easy. But then it complained about too many file watchers

{% highlight bash %}
<i> [webpack-dev-server] Project is running at:
<i> [webpack-dev-server] Loopback: http://localhost:8080/, http://127.0.0.1:8080/
<i> [webpack-dev-server] Content not from webpack is served from '/home/andre/git/repo/starting-with-elm/public' directory
node:internal/errors:456
    ErrorCaptureStackTrace(err);
    ^

Error: ENOSPC: System limit for number of file watchers reached, watch '/home/andre/git/repo/starting-with-elm'
{% endhighlight %}

When this was fixed by increasing the number of watchers on my machine with puttin this line in /etc/sysctl.conf:

{% highlight bash %}
fs.inotify.max_user_watches=524288
{% endhighlight %}

and the doing a

{% highlight bash %}
sudo sysctl -p.
{% endhighlight %}

By now the devserver started and opent a webpage with a friendly "hello world".
While this is friendly and looks good, it is not the message I wanted to see.
Besides this, it also said "Tip: Check your console". And indeed the console had interesting information
{% highlight bash %}
andre@HP-ProBook-470-G5:~/git/repo/starting-with-elm$ npx webpack serve
<i> [webpack-dev-server] Project is running at:
<i> [webpack-dev-server] Loopback: http://localhost:8080/, http://127.0.0.1:8080/
<i> [webpack-dev-server] Content not from webpack is served from '/home/andre/git/repo/starting-with-elm/public' directory
<i> [webpack-dev-middleware] wait until bundle finished: /
asset bundle.js 121 KiB [emitted] (name: main)
asset index.html 825 bytes [emitted]
runtime modules 27 KiB 12 modules
cacheable modules 59.8 KiB
  modules by path ./node_modules/webpack-dev-server/client/ 58 KiB
    modules by path ./node_modules/webpack-dev-server/client/utils/*.js 7.69 KiB 6 modules
    modules by path ./node_modules/webpack-dev-server/client/*.js 12.9 KiB 3 modules
    modules by path ./node_modules/webpack-dev-server/client/modules/ 35.9 KiB
      ./node_modules/webpack-dev-server/client/modules/strip-ansi/index.js 6.09 KiB [built] [code generated]
      ./node_modules/webpack-dev-server/client/modules/logger/index.js 29.8 KiB [built] [code generated]
    ./node_modules/webpack-dev-server/client/clients/WebSocketClient.js 1.48 KiB [built] [code generated]
  modules by path ./src/ 189 bytes
    ./src/static/index.js 150 bytes [built] [code generated]
    ./src/elm/Main.elm 39 bytes [built] [code generated] [1 error]
  ./node_modules/webpack/hot/dev-server.js 1.63 KiB [built] [code generated]

ERROR in ./node_modules/webpack-dev-server/client/index.js?protocol=ws%3A&hostname=localhost&port=8080&pathname=%2Fws&logging=info&reconnect=10 2:0-47
Module not found: Error: Can't resolve 'webpack/hot/log.js' in '/home/andre/git/repo/starting-with-elm/node_modules/webpack-dev-server/client'

ERROR in ./node_modules/webpack-dev-server/client/overlay.js 3:0-43
Module not found: Error: Can't resolve 'ansi-html-community' in '/home/andre/git/repo/starting-with-elm/node_modules/webpack-dev-server/client'
 @ ./node_modules/webpack-dev-server/client/index.js?protocol=ws%3A&hostname=localhost&port=8080&pathname=%2Fws&logging=info&reconnect=10 6:0-57 77:6-10 115:6-10 124:6-10 142:27-40 158:6-10 167:28-41 183:6-10 193:6-10

ERROR in ./node_modules/webpack-dev-server/client/overlay.js 4:0-39
Module not found: Error: Can't resolve 'html-entities' in '/home/andre/git/repo/starting-with-elm/node_modules/webpack-dev-server/client'
 @ ./node_modules/webpack-dev-server/client/index.js?protocol=ws%3A&hostname=localhost&port=8080&pathname=%2Fws&logging=info&reconnect=10 6:0-57 77:6-10 115:6-10 124:6-10 142:27-40 158:6-10 167:28-41 183:6-10 193:6-10

ERROR in ./node_modules/webpack-dev-server/client/utils/createSocketURL.js 1:0-22
Module not found: Error: Can't resolve 'url' in '/home/andre/git/repo/starting-with-elm/node_modules/webpack-dev-server/client/utils'

BREAKING CHANGE: webpack < 5 used to include polyfills for node.js core modules by default.
This is no longer the case. Verify if you need this module and configure a polyfill for it.

If you want to include a polyfill, you need to:
        - add a fallback 'resolve.fallback: { "url": require.resolve("url/") }'
        - install 'url'
If you don't want to include a polyfill, you can use an empty module like this:
        resolve.fallback: { "url": false }
 @ ./node_modules/webpack-dev-server/client/index.js?protocol=ws%3A&hostname=localhost&port=8080&pathname=%2Fws&logging=info&reconnect=10 10:0-57 199:16-31

ERROR in ./node_modules/webpack-dev-server/client/utils/parseURL.js 1:0-22
Module not found: Error: Can't resolve 'url' in '/home/andre/git/repo/starting-with-elm/node_modules/webpack-dev-server/client/utils'

BREAKING CHANGE: webpack < 5 used to include polyfills for node.js core modules by default.
This is no longer the case. Verify if you need this module and configure a polyfill for it.

If you want to include a polyfill, you need to:
        - add a fallback 'resolve.fallback: { "url": require.resolve("url/") }'
        - install 'url'
If you don't want to include a polyfill, you can use an empty module like this:
        resolve.fallback: { "url": false }
 @ ./node_modules/webpack-dev-server/client/index.js?protocol=ws%3A&hostname=localhost&port=8080&pathname=%2Fws&logging=info&reconnect=10 4:0-43 23:26-34

ERROR in ./node_modules/webpack-dev-server/client/utils/reloadApp.js 2:0-48
Module not found: Error: Can't resolve 'webpack/hot/emitter.js' in '/home/andre/git/repo/starting-with-elm/node_modules/webpack-dev-server/client/utils'
 @ ./node_modules/webpack-dev-server/client/index.js?protocol=ws%3A&hostname=localhost&port=8080&pathname=%2Fws&logging=info&reconnect=10 9:0-45 127:4-13 161:4-13

ERROR in ./node_modules/webpack/hot/dev-server.js 14:12-28
Module not found: Error: Can't resolve './log' in '/home/andre/git/repo/starting-with-elm/node_modules/webpack/hot'

ERROR in ./node_modules/webpack/hot/dev-server.js 29:6-35
Module not found: Error: Can't resolve './log-apply-result' in '/home/andre/git/repo/starting-with-elm/node_modules/webpack/hot'

ERROR in ./node_modules/webpack/hot/dev-server.js 47:19-39
Module not found: Error: Can't resolve './emitter' in '/home/andre/git/repo/starting-with-elm/node_modules/webpack/hot'

ERROR in ./src/elm/Main.elm
Module build failed (from ./node_modules/elm-webpack-loader/index.js):
Error: ENOENT: no such file or directory, open '/home/andre/git/repo/starting-with-elm/src/elm/elm.json'
    at Object.openSync (node:fs:583:3)
    at Object.readFileSync (node:fs:451:35)
    at filesToWatch (/home/andre/git/repo/starting-with-elm/node_modules/elm-webpack-loader/index.js:56:23)
    at Object.module.exports (/home/andre/git/repo/starting-with-elm/node_modules/elm-webpack-loader/index.js:108:24)
 @ ./src/static/index.js 2:10-32

9 errors have detailed information that is not shown.
Use 'stats.errorDetails: true' resp. '--stats-error-details' to show it.

webpack 5.59.1 compiled with 10 errors in 1361 ms
assets by path *.js 122 KiB
  asset bundle.js 121 KiB [emitted] (name: main)
  asset main.d0d158cf8f40426e8705.hot-update.js 860 bytes [emitted] [immutable] [hmr] (name: main)
asset index.html 825 bytes [emitted]
asset main.d0d158cf8f40426e8705.hot-update.json 28 bytes [emitted] [immutable] [hmr]
Entrypoint main 122 KiB = bundle.js 121 KiB main.d0d158cf8f40426e8705.hot-update.js 860 bytes
cached modules 59.8 KiB [cached] 14 modules
runtime modules 27 KiB 12 modules
./src/elm/Main.elm 39 bytes [built] [1 error]

ERROR in ./node_modules/webpack-dev-server/client/index.js?protocol=ws%3A&hostname=localhost&port=8080&pathname=%2Fws&logging=info&reconnect=10 2:0-47
Module not found: Error: Can't resolve 'webpack/hot/log.js' in '/home/andre/git/repo/starting-with-elm/node_modules/webpack-dev-server/client'

ERROR in ./node_modules/webpack-dev-server/client/overlay.js 3:0-43
Module not found: Error: Can't resolve 'ansi-html-community' in '/home/andre/git/repo/starting-with-elm/node_modules/webpack-dev-server/client'
 @ ./node_modules/webpack-dev-server/client/index.js?protocol=ws%3A&hostname=localhost&port=8080&pathname=%2Fws&logging=info&reconnect=10 6:0-57 77:6-10 115:6-10 124:6-10 142:27-40 158:6-10 167:28-41 183:6-10 193:6-10

ERROR in ./node_modules/webpack-dev-server/client/overlay.js 4:0-39
Module not found: Error: Can't resolve 'html-entities' in '/home/andre/git/repo/starting-with-elm/node_modules/webpack-dev-server/client'
 @ ./node_modules/webpack-dev-server/client/index.js?protocol=ws%3A&hostname=localhost&port=8080&pathname=%2Fws&logging=info&reconnect=10 6:0-57 77:6-10 115:6-10 124:6-10 142:27-40 158:6-10 167:28-41 183:6-10 193:6-10

ERROR in ./node_modules/webpack-dev-server/client/utils/createSocketURL.js 1:0-22
Module not found: Error: Can't resolve 'url' in '/home/andre/git/repo/starting-with-elm/node_modules/webpack-dev-server/client/utils'

BREAKING CHANGE: webpack < 5 used to include polyfills for node.js core modules by default.
This is no longer the case. Verify if you need this module and configure a polyfill for it.

If you want to include a polyfill, you need to:
        - add a fallback 'resolve.fallback: { "url": require.resolve("url/") }'
        - install 'url'
If you don't want to include a polyfill, you can use an empty module like this:
        resolve.fallback: { "url": false }
 @ ./node_modules/webpack-dev-server/client/index.js?protocol=ws%3A&hostname=localhost&port=8080&pathname=%2Fws&logging=info&reconnect=10 10:0-57 199:16-31

ERROR in ./node_modules/webpack-dev-server/client/utils/parseURL.js 1:0-22
Module not found: Error: Can't resolve 'url' in '/home/andre/git/repo/starting-with-elm/node_modules/webpack-dev-server/client/utils'

BREAKING CHANGE: webpack < 5 used to include polyfills for node.js core modules by default.
This is no longer the case. Verify if you need this module and configure a polyfill for it.

If you want to include a polyfill, you need to:
        - add a fallback 'resolve.fallback: { "url": require.resolve("url/") }'
        - install 'url'
If you don't want to include a polyfill, you can use an empty module like this:
        resolve.fallback: { "url": false }
 @ ./node_modules/webpack-dev-server/client/index.js?protocol=ws%3A&hostname=localhost&port=8080&pathname=%2Fws&logging=info&reconnect=10 4:0-43 23:26-34

ERROR in ./node_modules/webpack-dev-server/client/utils/reloadApp.js 2:0-48
Module not found: Error: Can't resolve 'webpack/hot/emitter.js' in '/home/andre/git/repo/starting-with-elm/node_modules/webpack-dev-server/client/utils'
 @ ./node_modules/webpack-dev-server/client/index.js?protocol=ws%3A&hostname=localhost&port=8080&pathname=%2Fws&logging=info&reconnect=10 9:0-45 127:4-13 161:4-13

ERROR in ./node_modules/webpack/hot/dev-server.js 14:12-28
Module not found: Error: Can't resolve './log' in '/home/andre/git/repo/starting-with-elm/node_modules/webpack/hot'

ERROR in ./node_modules/webpack/hot/dev-server.js 29:6-35
Module not found: Error: Can't resolve './log-apply-result' in '/home/andre/git/repo/starting-with-elm/node_modules/webpack/hot'

ERROR in ./node_modules/webpack/hot/dev-server.js 47:19-39
Module not found: Error: Can't resolve './emitter' in '/home/andre/git/repo/starting-with-elm/node_modules/webpack/hot'

ERROR in ./src/elm/Main.elm
Module build failed (from ./node_modules/elm-webpack-loader/index.js):
Error: ENOENT: no such file or directory, open '/home/andre/git/repo/starting-with-elm/src/elm/elm.json'
    at Object.openSync (node:fs:583:3)
    at Object.readFileSync (node:fs:451:35)
    at filesToWatch (/home/andre/git/repo/starting-with-elm/node_modules/elm-webpack-loader/index.js:56:23)
    at Object.module.exports (/home/andre/git/repo/starting-with-elm/node_modules/elm-webpack-loader/index.js:108:24)
 @ ./src/static/index.js 2:10-32

9 errors have detailed information that is not shown.
Use 'stats.errorDetails: true' resp. '--stats-error-details' to show it.

webpack 5.59.1 compiled with 10 errors in 211 ms
{% endhighlight %}

The most important one is
Error: ENOENT: no such file or directory, open '/home/andre/git/repo/starting-with-elm/src/elm/elm.json'

The elm-webpack-loader docs says to point the elSource variable to the elm.json file.
I didn't. After that at least that part worked

The other 9 errors were still there. But devserver staid??? running.

the first part went without problems, but the devserver did not. The latest version of webpack does not support the old dev server. I tried 'webpack serve' that did start without problems, but electron was never started and the files were not served to localhost. So even if electron was started, no Elm screen was shown.

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

[Elm Electron Starter](https://github.com/dillonkearns/elm-electron-starter)

[The original Elm electron webpack guide](https://github.com/johnomarkid/elm-electron-webpack)

[My Elm electron webpack fork](https://github.com/tikal86/elm-electron-webpack)
