---
title: SWiPE Searching Wikipedia by Example, By Example Structured Queries, BESt Query
layout: simple_page
---


# SWiPE: Searching WikiPedia by Example


## Introducing SWiPE
SWiPE is a research prototype interface that implements the _BESt Query_ paradigm ([WWW12 paper](http://www2012.wwwconference.org/proceedings/companion/p309.pdf)). 

It allows to better search Wikipedia, by using different parameters other than simpy keyword search.
SWiPE interface is looks like Wikipedia but you can click and search using infoboxes as if they were form fields to input constraints.

For instance, to search for all Italian places with more than 2 million people, you can:

1. go to any page similar to the result you are looking for, for instance, go to the [city of Florence](/wiki/Florence) page
2. in the infobox, move the mouse over _Italy_, close to country, click and type `=italy`; similarly, go over Rome's _population total_, click and type `>2000000` (overwriting the existing value)
3. click on the green "SWiPE" button in the bottom Toolbar; now you will be shown a list of the largest Italian places, as you asked!

Now, you can try refining your search by getting back to the previous example page ([city of Florence](/wiki/Florence)) and, for instance:

1. on the bottom-right search box (there is `Settlement`), overwrite with `cities`: this will only show cities, filtering out provinces and other kind of settlements
2. go over and click on the _population total_ field, then click on the star symbol appearing in the popup: this will show the population of the cities in the results
3. go over and click on the _population total_ field, then click twice on the sort symbol appearing in the popup (at the right of the star symbol): this will sort the results by the population size, by clicking twice the sort will be descending.
4. you can hide the infobox with the link _hide this infobox_ on the infobox description.

SWiPE dynamically generates a SPARQL query ran against our DBpedia 2014 instance server. Any wrong value in the result is likely to be a wrong value in DBpedia. By clicking on the [D] links you can check values in DBpedia Linked Open Data.

To discover active (recognized) fields, press Ctrl+Alt+1 or use the SWiPE Toolbar commands at the bottom of the screen. The Toolbar will also allow to search for text in the abstracts and to constraint the type of the required results (e.g., _Settlement_).

Enjoy!

<br/>
*The SWiPE Team*

[Maurizio Atzori](http://atzori.webofcode.org/), University of Cagliari, _atzori@unica.it_

[Carlo Zaniolo](http://www.cs.ucla.edu/~zaniolo/), University of California in Los Angeles, _zaniolo@cs.ucla.edu_

