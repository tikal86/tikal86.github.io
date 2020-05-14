# Testing reactive programming
A TestSubscriber only works with a Flowable, not with an Observable
otherwise you get an error:
```Java
        Error:(78, 17) java: no suitable method found for subscribe(io.reactivex.subscribers.TestSubscriber<java.lang.String>)
        method io.reactivex.Observable.subscribe(io.reactivex.functions.Consumer<? super java.lang.String>) is not applicable
                (argument mismatch; io.reactivex.subscribers.TestSubscriber<java.lang.String> cannot be converted to io.reactivex.functions.Consumer<? super java.lang.String>)
        method io.reactivex.Observable.subscribe(io.reactivex.Observer<? super java.lang.String>) is not applicable
                (argument mismatch; io.reactivex.subscribers.TestSubscriber<java.lang.String> cannot be converted to io.reactivex.Observer<? super java.lang.String>)
```
