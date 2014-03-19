---
layout: page
title: DBpedia Property Ranking
---

DBpedia Property Ranking
========================

Experimental MLR Comparison
---------------------------

We are in the process of publishing experiments on different machine learning-to-rank models.
They will be available in this page soon.


Computing Ranking Online (tool)
-------------------------------

The tool to compute property ranking is online as a public Web API.
In order to use it, given and entity (e.g., Cagliari) and a property (e.g., populationTotal), you can compute the ranking of the property for that entity by using the following exemplificatory url:

http://swipe.unica.it/apps/rankProperties/?property=http://dbpedia.org/property/populationTotal&entity=Cagliari

The result is provided in JSON format, such that it can be used within other projects online.

The API also allows to compute the general ranking of properties, without specifying an entity:

http://swipe.unica.it/apps/rankProperties/?property=http://dbpedia.org/property/populationTotal

In this second case, the ranking is not computed according to a specific entity.


