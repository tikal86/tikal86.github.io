---
layout: post
title:  "Failed webpack configuration"
date:   2022-01-07
categories: [elm]
tags: [webpack, elm]
---

## Webpack configuration for elm electron starting guide
This post is a sidelane from the blog [starting with elm](https://tikal86.github.io/elm/starting-with-elm)
That describes the setup for an elm application within electron with the help of a guide from github.
This describes the failed attempt to configure webpack and a dev server for that project. 

#### Webpack
The guide was written with an older version of webpack in mind. The config schema is changed and so the proposed config does not work. So webpack init was run to create a new config file. The follwing answers were given to the questions asked by webpack init:

<figure><pre style="background-color: black;"><code style="background-color: black;color: #66d9ef;border: none;font-size: x-small">
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
</code></pre></figure>

After that change the entry in the webpack.config.js for entry, because webpack uses './src/index.js' as default.
And add the elm loader to the module/rules/ list. Luckily we can copy that paert from the guide

{% highlight javascript %}
{
    test:    /\.elm$/,
    exclude: [/elm-stuff/, /node_modules/],
    loader:  'elm-webpack?verbose=true&warn=true',
}
{% endhighlight %}

Now we need to add the plugins that webpack put in the config.
{% highlight javascript %}
npm install html-webpack-plugin --save-dev
npm install mini-css-extract-plugin --save-dev
npm install workbox-webpack-plugin --save-dev
npm install babel-loader --save-dev
{% endhighlight %}

BTW if you npx webpack configtest it will show all the errors that there are.

Now there are no validation errors anymore, we can start webpack.
Unfortunately there is still an error when run:

{% highlight javascript %}
[webpack-cli] Error: Compiling RuleSet failed: Query arguments 
on 'loader' has been removed in favor of the 'options' property 
(at ruleSet[1].rules[3].loader: elm-webpack?verbose=true&warn=true)
{% endhighlight %}

Apparently the loader options should be in a separate object:

{% highlight javascript %}
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

{% highlight javascript %}
<i> [webpack-dev-server] Project is running at:
<i> [webpack-dev-server] 
    Loopback: http://localhost:8080/, http://127.0.0.1:8080/
<i> [webpack-dev-server] Content not from webpack is served from 
    '/home/andre/git/repo/starting-with-elm/public' directory
node:internal/errors:456
    ErrorCaptureStackTrace(err);
    ^

Error: ENOSPC: System limit for number of file watchers reached, 
watch '/home/andre/git/repo/starting-with-elm'
{% endhighlight %}

When this was fixed by increasing the number of watchers on my machine with puttin this line in /etc/sysctl.conf:

{% highlight javascript %}
fs.inotify.max_user_watches=524288
{% endhighlight %}

and the doing a

{% highlight javascript %}
sudo sysctl -p.
{% endhighlight %}

By now the devserver started and opent a webpage with a friendly "hello world".
While this is friendly and looks good, it is not the message I wanted to see.
Besides this, it also said "Tip: Check your console". And indeed the console had interesting information

<figure><pre style="background-color: black;"><code style="background-color: black;color: #66d9ef;border: none;font-size: xx-small">
andre@HP-ProBook-470-G5:
~/git/repo/starting-with-elm$ npx webpack serve
<i> [webpack-dev-server] Project is running at:
<i> [webpack-dev-server] 
    Loopback: http://localhost:8080/, http://127.0.0.1:8080/
<i> [webpack-dev-server] Content not from webpack is served from 
    '/home/andre/git/repo/starting-with-elm/public' directory
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
</code></pre></figure>

The most important one is
Error: ENOENT: no such file or directory, open '/home/andre/git/repo/starting-with-elm/src/elm/elm.json'

The elm-webpack-loader docs says to point the elSource variable to the elm.json file.
I didn't. After that at least that part worked

The other 9 errors were still there. But devserver staid??? running.

the first part went without problems, but the devserver did not. The latest version of webpack does not support the old dev server. I tried 'webpack serve' that did start without problems, but electron was never started and the files were not served to localhost. So even if electron was started, no Elm screen was shown.
