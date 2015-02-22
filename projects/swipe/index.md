---
title: SWiPE Searching Wikipedia by Example, By Example Structured Queries, BESt Query
layout: simple_page
---


# SWiPE: Searching WikiPedia by Example


## Introducing SWiPE
SWiPE is a research prototype interface that implements the _BESt Query_ paradigm ([WWW12 paper](http://www2012.wwwconference.org/proceedings/companion/p309.pdf)). 

It allows to better search Wikipedia, by using different parameters other than simple keyword search.
SWiPE interface looks like Wikipedia but you can click and search using infoboxes as if they were form fields to input constraints.

For instance, to search for all Italian places with more than 2 million people, you can:

1. go to any page similar to the result you are looking for; e.g., go to the [city of Florence](/wiki/Florence) page
2. in the infobox, move the mouse over _Italy_, close to *Country*, click and type `=italy` (or use the set button on the popup); similarly, go over Rome's *Population Total*, click and type `>2000000` (overwriting the existing value)
3. click on the green "SWiPE" button in the bottom Toolbar; now you will be shown [a list of the largest Italian places](/wiki/Special:SwipeSearch?sp=Florence&dbo%3Acountry=Italy&dbo%3ApopulationTotal=%3E2000000), as you asked!

Now, you can refine your search by getting back to the previous example page ([city of Florence](/wiki/Florence)) and, for instance:

1. on the bottom-right search box (there is `Settlement`), overwrite with `cities`: this box allows constraints on the type,   thus allowing cities only, and filtering out provinces and other kind of settlements
2. go over and click on the *Population Total* field, then click on the star symbol appearing in the popup: this will show the population of the cities in the results
3. on the *Population Total* popup, click twice on the sort symbol appearing at the right of the star symbol: this will sort the results by the population size, by clicking twice the sort will be descending.
4. you can hide the infobox with the link _hide this infobox_ on the infobox description.

By clicking on the green button you are faced with the list of [largest cities in italy, sorted by starting from the largest](/wiki/Special:SwipeSearch?sp=Florence&dbo%3Acountry=Italy&dbo%3ApopulationTotal=%3E2000000&rdf%3Atype=cities&dbo%3ApopulationTotal=*&dbo:populationTotal=^desc).

SWiPE dynamically generates a SPARQL query ran against our DBpedia 2014 instance server. Any wrong value in the result is likely to be a wrong value in DBpedia. By clicking on the _[D]_ link close to each result, you can check values in the DBpedia Linked Open Data.
Text constraints are ignore case, and substring search by default: you can specify `ignazio` as *Mayor* in the previous search, finding Rome with mayor `Ignazio Marino`.

To discover active (recognized) fields, press Ctrl+Alt+1 or use the _show fields_ checkbox in the SWiPE Toolbar at the bottom of the screen. The Toolbar will also allow to search for text in the abstracts and to constraint the type of the required results (e.g., _Settlement_).


To simplify the use of SWiPE, drag an drop the following link (a *flipr*) to your browser's bookmarks bar: <a href="javascript:
var l=window.location.href;if(l.indexOf('.wikipedia.org/wiki/')>0){l=l.split('/');l=l[l.length-1];window.location.href='http://swipe.webofcode.org/wiki/'+l;} else if(l.indexOf('.webofcode.org/wiki/')>0){l=l.split('/');l=l[l.length-1];window.location.href='http://en.wikipedia.org/wiki/'+l;}else{window.location.href='http://swipe.webofcode.org/';};">SwipeFlip</a>. Then, whenever you are on a Wikipedia page, just click on the new SWiPE link on the bookmarks bar and the browser will jump to the its corresponding SWiPE page.

Enjoy!

<br/>
*The SWiPE Team*

[Maurizio Atzori](http://atzori.webofcode.org/), University of Cagliari, _atzori@unica.it_

[Carlo Zaniolo](http://www.cs.ucla.edu/~zaniolo/), University of California in Los Angeles, _zaniolo@cs.ucla.edu_

