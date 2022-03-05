# Creating an app

For the real programming in Elm we want to develop a little app.
A charting app, The goal is to develop a charting app that will display values on a timeline.
When hovering over a value, other properties of that event are displayed.

## Selecting a charting framework

Criteria
- must be compatible with Elm 0.19
- has to have a timeline chart or similar
- has to be updated recently
- documentation and examples
- preferably tooltips

### Candidates
Only the candidats that were updated in 2021 or later and could display a line chart or something similar were considered.

#### Elm visualization
https://package.elm-lang.org/packages/gampleman/elm-visualization/latest/

It creates SVG charts and displays them.
It is fairly low level

It has a linechart to display timeseries.
The lastest release is from may 2021, so fairly recent
Has many examples and extensive documentation.
Does not have tooltips

#### Elm charts
https://elm-charts.org/
https://github.com/terezka/elm-charts

It creates SVG charts and displays them.
It is high level, mirrors the element and attribute pattern from HTML.

It has a linechart to display timeseries.
The lastest release is from octobre 2021, so fairly recent
Has many examples and extensive documentation.
Does have tooltips

#### Vectual
https://vectual.org/
It has a linechart to display timeseries.
The lastest release is from february 2021, so fairly recent
Has Some examples and no documentation.
Does not have tooltips

### The choice
The choice is 'Elm charts'.
It looks easy to setup and use.
While 'Elm visualization' looks great and has lots of potential, for now it is to low level.
The attempt is to focus on  displaying the data, rather than the chart library.

## The data
The data used is static for now. It is from a gps logger and contains the gps position and ...
The data is served from a json server.

## The linechart
