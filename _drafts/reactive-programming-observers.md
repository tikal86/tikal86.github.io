# Observables

In the previous installment we talked about the theory and why you should use reactive programming. From now on we get more practical.

We start with the different type of observers.
 Hot-vs-cold
 Unicast vs multicast
 Observer vs Subject

But to show the differences we use a small program in Javascript were we draw charts. Check out the code from https://github.com/tikal86/reactive-programming

## Hot vs Cold

Laten zien met gesynchroniseerde grafieken, bijvoorbeeld grafiek met volume grafiek eronder. Deze moeten gesynchroniseerd zijn. Als je daarvoor een cold observer gebruikt en je subscribed iets later, zijn ze niet in sync. Dus moet je een hot observable gebruiken, dan maakt het niet uit dat je iets later bent, ze lopen in sync

## Unicast vs Multicast

Multicast is dan voor gesynchroniseerde grafieken.

## Observable vs Subject

Subject is zowel een Observable als een Observer. Dus je kunt een Observable anders transformeren. Van cold naar hot bijvoorbeeld.

## Type Subjecten

### Subject

Je krijgt alleen de nieuwe

### BehavioralSubject

Je krijgt de laatste en daarna de nieuwe

### ReplaySubject

Je krijgt de laatste x en daarna de nieuwe
Met moving averages
NB is ReplaySubject(1) hetzelfde als BehavioralSubject?

### AsyncSubject

?
