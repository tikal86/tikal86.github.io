# Programmeren met Elm

Dit is de eerste blog in een serie over functional programmeren met Elm. In deze serie beschrijf ik mijn leerprocess van de Elm programmeertaal en het schrijven van een applicatie daarmee. Niet alleen probeer ik te beschrijven hoe het gaat als alles werkt, maar juist ook de fouten die gemaakt kunnen worden en de oplossingen daarvoor. Dat gaat me goed af, want fouten maak ik genoeg ;-)

## Inleiding

Als eerste leg ik uit waarom ik Elm gekozen heb, wat Elm is en wat functioneel programmeren is.

### Waarom programmeren met Elm?

Al sinds mijn start als ontwikkelaar heb ik gewerkt met een Object georienteerde taal, namenlijk Java. Omdat ik het leuk vind om nieuwe dingen uit  te cinden en te proberen te begrijpen, heb ik dat vaak gedaan, maar allemaal binnen het concept van Object georienteerd programmeren en Java. Ondanks dat er een boel gebeurde in de Java wereled (een tijd lang niet zozeer met de taal zelf), voelde het als meer van hetzelfde. Een nieuwe bibliotheek hier en daar, maar altijd binnen hetzelfde concept. Toen ik ging programmeren voor het web, ging er een nieuwe wereld voor me open, het voelde als Java in de begin dagen. Heel veel nieuwe ontwikkelingen, frameworks en libraries.

### Functioneel programmeren

Veel van die nieuwe frameworks en libraries werkten met een ander concept, functioneel programmeren. Niet denken in objecten en communicatie tussen die objecten, maar denken in functies en data stromen van en naar die functies. Ze leken makkelijk te gebruiken, ondanks dat ze een ander concept gebruikten. Het interesseerde me enorm, wat is puur funbctioneel programmeren?. Hoe zou je dat kunnen gebruiken? Hoe programmer je daarmee? NB Functioneel programmeren zelf is niet nieuw, het bestaat al een lange tijd, maar de laatste tijd zie je het overal verschijnen. Zelfs Java heeft al taalconstructies gekregen, waarmee je kunt functioneel programmeren.

Dus ik wil functioneel programmeren leren, maar hoe dan? Sowieso moet het een pure functionele taal zijn, niet een taal waarbij het slechts een onderdeel is (zoals Javascript). Het zou kunnen binnen de jvm, bijvoorbeeld met frege of eta of helemaal los daarvan met bijvoorbeeld Haskell. Maar ik heb gekozen voor het web. ook daar zijn er meerdere kandidaten, maar Elm leek me de meest elegante en het sprak me aan wat Elm zou kunnen brengen.

### Wat is Elm?

Elm is a functionele programmeer taal voor het web, of zoals ze zelf zeggen op hun website 'A delightful language for reliable webapps.'. De belangrijkste eigenschappen zijn 'Geen runtime excepties', 'Goede prestaties', 'Gedwongen semantisch versioneren', 'Kleine bestanddelen', and 'Javascript interoperabiliteit'. Het compileert naar javascript en op die manier is het eenvoudig te integreren in bestaande processen.
