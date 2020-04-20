---
layout: post
title:  "Reactive programming introduction"
date:   2020-04-19 11:40:59
categories: reactive programming
---
<html>
<body>

# Reactive programming

This is a blog series about reactive programming. A solution to programming in an environment with asynchronous data streams.

## What is reactive programming?

Reactive programming is a declarative programming paradigm concerned with data streams and the propagation of change (<a href="https://en.wikipedia.org/wiki/Reactive_programming">wikipedia</a>)

Do not confuse reactive programming with reactive systems. It is possible to use reactive programming to create reactive systems, but they are different things. Reactive systems are about how the system as a whole behaves. They are responsive, resilient, elastic and message driven (<a href="https://www.reactivemanifesto.org/">reactivemanifesto</a>). Reactive programming is about how the code behaves. Reactive programming can be used to build reactive systems, but also to build non reactive systems.

The implementation of reactive programming that is used in this blog is ReactiveX (<a href="http://reactivex.io">reactivex.io</a>). An API for asynchronous programming
with observable streams. It is implemented in several programming languages. The examples in this blog are in Java. 

‘ReactiveX is a combination of the best ideas from the Observer pattern, the Iterator pattern, and functional programming’

 
So it is not functional programming, but uses some ideas from functional programming. 

 

### What are these patterns?

#### The observer pattern

The observer pattern is a software design pattern in which an object, called the observable, notifies its observers automatically of any change in the state of the data the observable is handling. (<a href="https://en.wikipedia.org/wiki/Observer_pattern">wikipedia</a>) 

 

#### The iterator pattern

The iterator pattern is a design pattern in which an iterator is used to traverse a container and access the container's elements. The iterator pattern decouples algorithms from containers <a href="https://en.wikipedia.org/wiki/Iterator_pattern">wikipedia</a>

 

#### Functional programming

Functional programming is a style of building the structure and elements of computer programs, that treats computation as the evaluation of mathematical functions and avoids changing state and mutable data (<a href="https://en.wikipedia.org/wiki/Functional_programming">wikipedia</a>) 

 

### Coupling Observables and Observers

In reactive programming observables are coupled to observers through operations. When an observable sends data, the data is operated on by the operations and then received by the observer. 

### What is an observable?</h3> 

An observable is an object that sends data to it’s observers.  


<svg viewBox="0 0 660 120" width="440" height="80" xmlns="http://www.w3.org/2000/svg"><style>
    /* Note that the color of the text is set with the    *
     * fill property, the color property is for HTML only */
    .red { font: 40px serif; fill: red; }
    .small { font: 20px sans-serif; }
    .large { font: 40px sans-serif; }
    .yellowish {fill: rgb(255,203,70); }
    .blue {fill: rgb(62,161,203);}
    .green {fill: rgb(130,215,54);}
    .red {fill: rgb(255,105,70)};
    .operationbox {fill: white;stroke: black;font: 40px sans-serif;)};</style><g> <line x1="20" y1="30" x2="600" y2="30" stroke="black"></line><line x1="560" y1="15" x2="560" y2="45" stroke="black"></line><polygon points="600,20 630,30 600,40" fill="black" stroke="black"/></g><g> <circle class="yellowish" cx="100" cy="30" r="20" stroke="black" ></circle><text x="94" y="37" class="small">2</text></g><g> <circle class="blue" cx="150" cy="30" r="20" stroke="black" ></circle><text x="139" y="37" class="small">30</text></g><g> <circle class="green" cx="200" cy="30" r="20" stroke="black" ></circle><text x="189" y="37" class="small">22</text></g><g> <circle class="red" cx="250" cy="30" r="20" stroke="black" ></circle><text x="244" y="37" class="small">5</text></g>
</svg>
<br/>

Because it is possible that the observer can’t handle receiving the data as fast as the observable can send it, it is possible for the observer to signal the observable. This is called backpressure. 

Not all observables have the possibility to handle backpressure. To differentiate between observables with and without backpressure, they usually have a different name. E.g. in RxJava an observable without backpressure is called Observable. An observable with backpressure is called Flowable.  

An observable should be subscribed to an observable to recieve data. When a subscription is made, a subscription is returned. A subscriber can use this subscription object to unsubscribe. The object to unsubscribe is different, depending on if it is coming from an observable with or without backpressure.

Creating an observable with and without backpressure in RxJava can be done with factory methods:

<pre language="java">
    Observable.just("Hello observable without backpressure");
    Flowable.just("Hello flowable");
</pre>
 

### What is an observer?

An observer listens to an observable. It subscribes to the observable and gets a subscription to it. After subscribing it recieves data from the observable. With the subscription it can unsubscribe from the observable and then no longer recieve data from the observable.  

<svg viewBox="0 0 660 120" width="440" height="80" xmlns="http://www.w3.org/2000/svg"><style>
    /* Note that the color of the text is set with the    *
     * fill property, the color property is for HTML only */
    .red { font: 40px serif; fill: red; }
    .small { font: 20px sans-serif; }
    .large { font: 40px sans-serif; }
    .yellowish {fill: rgb(255,203,70); }
    .blue {fill: rgb(62,161,203);}
    .green {fill: rgb(130,215,54);}
    .red {fill: rgb(255,105,70)};
    .operationbox {fill: white;stroke: black;font: 40px sans-serif;)};</style><g> <line x1="20" y1="30" x2="600" y2="30" stroke="black"></line><line x1="560" y1="15" x2="560" y2="45" stroke="black"></line><polygon points="600,20 630,30 600,40" fill="black" stroke="black"/></g><g> <circle class="blue" cx="150" cy="30" r="20" stroke="black" ></circle><text x="139" y="37" class="small">30</text></g><g> <circle class="green" cx="200" cy="30" r="20" stroke="black" ></circle><text x="189" y="37" class="small">22</text></g>
</svg>


An observer can be as simple as a lambda expression or a method reference.
<pre language="java">
    observable.subscribe(System.out::println);
</pre>
 
 

There is a special case when an object can be both an observer and an observable at the same time. This is called a subject. This will be described in the next installment.

### What are operations?

Operations are the functions that do transformations on the data that is sent from an observable to an observer or on the observable itself. There are many operations and they can be grouped into categories. There are categories creating observables, transforming, filtering or combining operators and lots more. 

<svg viewBox="0 0 660 130" width="440" height="130" xmlns="http://www.w3.org/2000/svg"><style>
    /* Note that the color of the text is set with the    *
     * fill property, the color property is for HTML only */
    .red { font: 40px serif; fill: red; }
    .small { font: 20px sans-serif; }
    .large { font: 40px sans-serif; }
    .yellowish {fill: rgb(255,203,70); }
    .blue {fill: rgb(62,161,203);}
    .green {fill: rgb(130,215,54);}
    .red {fill: rgb(255,105,70)};
    .operationbox {fill: white;stroke: black;font: 40px sans-serif;)};</style><rect class="operationbox" fill="white" stroke="black" x="20" y="10" width="580" height="100" /><text x="150" y="74"      class="large">filter (x => x > 10)</text>
</svg>


An operation can also be a lambda expression or a method reference e.g. like a filter.

<pre language="java">
    observable
    .filter(text -> text.startsWith("Hello"))
    ...
</pre>

A complete example would look like
<pre language="java">
    Observable.just("Hello observable without backpressure")
    .filter(text -> text.startsWith("Hello"))
    .subscribe(System.out::println);
</pre>


### Why would reactive programming be used ?

The advantages of reactive programming are that it avoids stateful programs, uses clean input/output functions over observable streams and allows the programmer to abstract away low-level threading, synchronization, and concurrency issues. 

Another advantage is that it creates programs with less code, making them easier to read and understand. Since error handling is built in, it makes the code easier especially in asynchronous situations. 

 

 

### When would reactive programming be applicable ?

Reactive programming is best used when concurrency and asynchronicity are needed. Reactive programming handles concurrency and asynchronicity really well and makes these complex concepts easy for the developer.  

 

Another good usage is when handling streams of data. Then the reactive programming paradigm suits the flow of the program better. The type of data doesn’t matter 

 

### Next time

The next installment will talk about what types of observables and observers there are. 



### References

<ol>
    <li><a href="https://en.wikipedia.org/wiki/Reactive_programming">Reactive_programming</a></li>
    <li><a href="https://www.reactivemanifesto.org/">reactivemanifesto</a></li>
    <li><a href="http://reactivex.io">reactivex.io</a></li>
    <li><a href="https://en.wikipedia.org/wiki/Observer_pattern">Observer pattern</a></li>
    <li><a href="https://en.wikipedia.org/wiki/Iterator_pattern">Iterator pattern</a></li>
    <li><a href="https://en.wikipedia.org/wiki/Functional_programming">Functional programming</a></li> 
</ol>

PS: the images are created similar to the one from <a href="https://rxmarbles.com/">rxmarbles</a> to prevent having another display language for reactive programming.
</body>
</html>
