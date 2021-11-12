---
layout: page
title: Highligh html in MD files
---
[Go to page with below javascript](https://tikal86.github.io/javascript.html)

## Automatic

    html
    <div id="text"></div>
    <script>
        document.getElementById("text").innerHTML = "Text added by JavaScript code";
    </script>

    html

    <div id="text"></div>
    <script>
        document.getElementById("text").innerHTML = "Text added by JavaScript code";
    </script>


## With highlight js
{% highlight html %}
        <div id="text"></div>
        <script>
            document
                .getElementById("text")
                .innerHTML = "Text added by JavaScript code";
        </script>
{% endhighlight %}


## With fenced code blocks (is the same as nothing (first one above))
``` html
<div id="text"></div>
<script>
    document.getElementById("text").innerHTML = "Text added by JavaScript code";
</script>
```

## Trying different higlighting for different languages

### Terminal input/output

#### With bash as language

{% highlight bash %}
elm make src/elm/Main.elm --output src/static/bundle.js

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

npm install html-webpack-plugin --save-dev
npm install mini-css-extract-plugin --save-dev
npm install workbox-webpack-plugin --save-dev
npm install babel-loader --save-dev

[webpack-cli] Error: Compiling RuleSet failed: Query arguments on 'loader' has been removed in favor of the 'options' property (at ruleSet[1].rules[3].loader: elm-webpack?verbose=true&warn=true)
{% endhighlight %}

#### With plaintext

{% highlight plaintext %}
elm make src/elm/Main.elm --output src/static/bundle.js

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

npm install html-webpack-plugin --save-dev
npm install mini-css-extract-plugin --save-dev
npm install workbox-webpack-plugin --save-dev
npm install babel-loader --save-dev

[webpack-cli] Error: Compiling RuleSet failed: Query arguments on 'loader' has been removed in favor of the 'options' property (at ruleSet[1].rules[3].loader: elm-webpack?verbose=true&warn=true)
{% endhighlight %}

#### With nohighlight

{% highlight nohighlight %}
elm make src/elm/Main.elm --output src/static/bundle.js

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

npm install html-webpack-plugin --save-dev
npm install mini-css-extract-plugin --save-dev
npm install workbox-webpack-plugin --save-dev
npm install babel-loader --save-dev

[webpack-cli] Error: Compiling RuleSet failed: Query arguments on 'loader' has been removed in favor of the 'options' property (at ruleSet[1].rules[3].loader: elm-webpack?verbose=true&warn=true)
{% endhighlight %}

#### With json as language

{% highlight json %}
elm make src/elm/Main.elm --output src/static/bundle.js

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

npm install html-webpack-plugin --save-dev
npm install mini-css-extract-plugin --save-dev
npm install workbox-webpack-plugin --save-dev
npm install babel-loader --save-dev

[webpack-cli] Error: Compiling RuleSet failed: Query arguments on 'loader' has been removed in favor of the 'options' property (at ruleSet[1].rules[3].loader: elm-webpack?verbose=true&warn=true)
{% endhighlight %}

#### With javascript as language

{% highlight javascript %}
elm make src/elm/Main.elm --output src/static/bundle.js

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

npm install html-webpack-plugin --save-dev
npm install mini-css-extract-plugin --save-dev
npm install workbox-webpack-plugin --save-dev
npm install babel-loader --save-dev

[webpack-cli] Error: Compiling RuleSet failed: Query arguments on 'loader' has been removed in favor of the 'options' property (at ruleSet[1].rules[3].loader: elm-webpack?verbose=true&warn=true)
{% endhighlight %}

#### With html as language

{% highlight html %}
elm make src/elm/Main.elm --output src/static/bundle.js

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

npm install html-webpack-plugin --save-dev
npm install mini-css-extract-plugin --save-dev
npm install workbox-webpack-plugin --save-dev
npm install babel-loader --save-dev

[webpack-cli] Error: Compiling RuleSet failed: Query arguments on 'loader' has been removed in favor of the 'options' property (at ruleSet[1].rules[3].loader: elm-webpack?verbose=true&warn=true)
{% endhighlight %}

#### Automatic

{% highlight%}
elm make src/elm/Main.elm --output src/static/bundle.js

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

npm install html-webpack-plugin --save-dev
npm install mini-css-extract-plugin --save-dev
npm install workbox-webpack-plugin --save-dev
npm install babel-loader --save-dev

[webpack-cli] Error: Compiling RuleSet failed: Query arguments on 'loader' has been removed in favor of the 'options' property (at ruleSet[1].rules[3].loader: elm-webpack?verbose=true&warn=true)
{% endhighlight %}

