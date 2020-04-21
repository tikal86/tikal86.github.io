---
layout: post
title:  "playing around with SVG"
date:   2020-04-19 11:40:59
categories: svg
---

## This is a page with svgs

To learn how to best show svgs on my blog pages I am playing around with the options that github pages and jekyll provide for displaying code and images

#### One rendered as preformatted text with inlined markdown
```svg
<svg viewBox="0 0 660 340" xmlns="http://www.w3.org/2000/svg"><style>
    /* Note that the color of the text is set with the    *
     * fill property, the color property is for HTML only */
    .red { font: 40px serif; fill: red; }
    .small { font: 20px sans-serif; }
    .large { font: 40px sans-serif; }
    .yellowish {fill: rgb(255,203,70); }
    .blue {fill: rgb(62,161,203);}
    .green {fill: rgb(130,215,54);}
    .red {fill: rgb(255,105,70)};
    .operationbox {fill: white;stroke: black;font: 40px sans-serif;)};</style>
<g>
    <line x1="20" y1="100" x2="600" y2="100" stroke="black"></line>
    <line x1="560" y1="85" x2="560" y2="115" stroke="black"></line>
    <polygon points="600,90 630,100 600,110" fill="black" stroke="black"/>
</g>
<g>
    <circle class="yellowish" cx="100" cy="100" r="20" stroke="black" ></circle>
    <text x="94" y="107" class="small">2</text>
</g>
<g>
    <circle class="blue" cx="150" cy="100" r="20" stroke="black" ></circle>
    <text x="139" y="107" class="small">30</text>
</g>
<g>
    <circle class="green" cx="200" cy="100" r="20" stroke="black" ></circle>
    <text x="189" y="107" class="small">22</text>
</g>
<g>
    <circle class="red" cx="250" cy="100" r="20" stroke="black" ></circle>
    <text x="244" y="107" class="small">5</text>
</g>
<g>
    <line x1="20" y1="300" x2="600" y2="300" stroke="black"></line>
    <line x1="560" y1="285" x2="560" y2="315" stroke="black"></line>
    <polygon points="600,290 630,300 600,310" fill="black" stroke="black"/>
</g>
<rect class="operationbox" fill="white" stroke="black" x="20" y="150" width="580" height="100" />
<text x="150" y="214" class="large">filter (x => x > 10)</text>
<g>
    <circle class="blue" cx="150" cy="300" r="20" stroke="black" ></circle>
    <text x="139" y="307" class="small">30</text>
</g>
<g>
    <circle class="green" cx="200" cy="300" r="20" stroke="black" ></circle>
    <text x="189" y="307" class="small">22</text>
</g>
</svg>
```

#### One rendered  as preformatted text with highlightjs
{% highlight xml %}
<svg viewBox="0 0 660 340" xmlns="http://www.w3.org/2000/svg"><style>
    /* Note that the color of the text is set with the    *
     * fill property, the color property is for HTML only */
    .red { font: 40px serif; fill: red; }
    .small { font: 20px sans-serif; }
    .large { font: 40px sans-serif; }
    .yellowish {fill: rgb(255,203,70); }
    .blue {fill: rgb(62,161,203);}
    .green {fill: rgb(130,215,54);}
    .red {fill: rgb(255,105,70)};
    .operationbox {fill: white;stroke: black;font: 40px sans-serif;)};</style>
<g>
    <line x1="20" y1="100" x2="600" y2="100" stroke="black"></line>
    <line x1="560" y1="85" x2="560" y2="115" stroke="black"></line>
    <polygon points="600,90 630,100 600,110" fill="black" stroke="black"/>
</g>
<g>
    <circle class="yellowish" cx="100" cy="100" r="20" stroke="black" ></circle>
    <text x="94" y="107" class="small">2</text>
</g>
<g>
    <circle class="blue" cx="150" cy="100" r="20" stroke="black" ></circle>
    <text x="139" y="107" class="small">30</text>
</g>
<g>
    <circle class="green" cx="200" cy="100" r="20" stroke="black" ></circle>
    <text x="189" y="107" class="small">22</text>
</g>
<g>
    <circle class="red" cx="250" cy="100" r="20" stroke="black" ></circle>
    <text x="244" y="107" class="small">5</text>
</g>
<g>
    <line x1="20" y1="300" x2="600" y2="300" stroke="black"></line>
    <line x1="560" y1="285" x2="560" y2="315" stroke="black"></line>
    <polygon points="600,290 630,300 600,310" fill="black" stroke="black"/>
</g>
<rect class="operationbox" fill="white" stroke="black" x="20" y="150" width="580" height="100" />
<text x="150" y="214" class="large">filter (x => x > 10)</text>
<g>
    <circle class="blue" cx="150" cy="300" r="20" stroke="black" ></circle>
    <text x="139" y="307" class="small">30</text>
</g>
<g>
    <circle class="green" cx="200" cy="300" r="20" stroke="black" ></circle>
    <text x="189" y="307" class="small">22</text>
</g>
</svg>
{% endhighlight %}

#### And one included
![observable svg](/images/observable.svg)

#### blur
![blur circle](/images/blur.svg)

#### blur different size
![blur circle](/images/blur.svg){:height="600px" width="300px"}
