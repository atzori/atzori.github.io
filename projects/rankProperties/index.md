---
layout: page
title: DBpedia Property Ranking
---

DBpedia Property Ranking
========================

Experimental MLR Comparison
---------------------------

We run a number of experiments on different machine learning-to-rank algorithms, comparing them against user data using [Spearman’s rank correlation coefficient](http://en.wikipedia.org/wiki/Spearman's_rank_correlation_coefficient).
For details of our experimental setting, experimental repeatability parameters and the outcome of our research please have a look at our [Report on DBpedia Property Ranking Experiments](https://bitbucket.org/atzori/files/downloads/rankprop_experiments_report.pdf).



Computing Ranking Online (tool)
-------------------------------

The tool to compute property ranking is online as a public Web API.
In order to use it, given and entity (e.g., Cagliari) and a property (e.g., populationTotal), you can compute the ranking of the property for that entity by using the following exemplificatory url:

    http://swipe.unica.it/apps/rankProperties/?property=http://dbpedia.org/property/populationTotal&entity=Cagliari

The result is provided in JSON format, such that it can be used within other projects online.
The API also allows to compute the general ranking of properties, without specifying an entity:

    http://swipe.unica.it/apps/rankProperties/?property=http://dbpedia.org/property/populationTotal

In this second case, the ranking is not computed according to a specific entity.

This service also includes in the response all properties ranked based on a given input entity (e.g., Cagliari) and a MLR algorithm number (1-8):

1. RankNet
2. RankBoost
3. AdaRank
4. Coordinate Ascent
5. LambdaMART
6. MART (Multiple Additive Regression Trees, a.k.a. Gradient boosted regression tree)
7. ListNet
8. Random Forests

Here we rank Cagliari's properties using _Random Forest_:

    http://swipe.unica.it/apps/rankProperties/?entity=Cagliari&alg=8



Publications
---------------------------

 1. [Ranking DBpedia Properties](http://web2touch2014.tudor.lu/Accepted.html). Atzori M., Dessi A. _23rd IEEE International Conference on Enabling Technologies: Infrastructure for Collaborative Enterprises, Web2Touch Track_ (2014)
 1. [Computing on-the-fly DBpedia Property Ranking](http://ieee-icsc.org/icsc2014/). Dessi A., Atzori M. _8th IEEE International Conference on Semantic Computing_ (2014)
