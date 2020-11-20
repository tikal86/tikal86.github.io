---
layout: page
title: Javascript in MD files
---
[Go to page with below javascript](https://tikal86.github.io/javascript.html)

Automatic
html
    <div id="text"></div>
    <script>
        document.getElementById("text").innerHTML = "Text added by JavaScript code";
    </script>


With highlight js
{% highlight html %}
        <div id="text"></div>
        <script>
            document
                .getElementById("text")
                .innerHTML = "Text added by JavaScript code";
        </script>
{% endhighlight %}


With fenced code blocks (is the same as nothing (first one above))
``` html
<div id="text"></div>
<script>
    document.getElementById("text").innerHTML = "Text added by JavaScript code";
</script>
```