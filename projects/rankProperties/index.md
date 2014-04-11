---
layout: page
title: DBpedia Property Ranking
---

DBpedia Property Ranking
========================

Experimental MLR Comparison
---------------------------

We run a number of experiments on different machine learning-to-rank algorithms, comparing them against user data using [Spearman’s rank correlation coefficient](http://en.wikipedia.org/wiki/Spearman's_rank_correlation_coefficient).
For details of our experimental setting, experimental repeatability parameters and the outcome of our research pleas have a look at our [Report on DBpedia Property Ranking Experiments](https://bitbucket.org/atzori/files/downloads/rankprop_experiments_report.pdf).



Computing Ranking Online (tool)
-------------------------------

The tool to compute property ranking is online as a public Web API.
In order to use it, given and entity (e.g., Cagliari) and a property (e.g., populationTotal), you can compute the ranking of the property for that entity by using the following exemplificatory url:

    http://swipe.unica.it/apps/rankProperties/?property=http://dbpedia.org/property/populationTotal&entity=Cagliari

The result is provided in JSON format, such that it can be used within other projects online.
The API also allows to compute the general ranking of properties, without specifying an entity:

    http://swipe.unica.it/apps/rankProperties/?property=http://dbpedia.org/property/populationTotal

In this second case, the ranking is not computed according to a specific entity.
Other details are available in our paper (currently under submission).

