---
layout: page
title: Web of Functions - SPARQL examples 
keywords: SPARQL, Web of Functions, Remote function calls
---

Examples of SPARQL queries using the Web of Functions
=====================================================
In this page we provide a set of SPARQL queries that document how take advantage of the [Web of Functions](http://webofcode.org/wfn/).
The [Web of Functions](http://webofcode.org/wfn/) is a simple, backward-compatible way to computing custom functions remotely from any SPARQL endpoint. It is named after the Web of Data, since every function is associated with a (potentially dereferenciable) URI, thus forming the Web of Functions.
Go to the [project page](http://webofcode.org/wfn/) to get info about the Web of Functions.

Endpoint
--------
We made available a public SPARQL endpoint at `http://webofcode.org/wfn/sparql` where you can access the Web of Functions.
SPARQL Queries can be posed by using [this form](http://webofcode.org/wfn/sparql.html). 

Composing functions (higher-order expressivity)
----------------------------------------------
In the following we show how simply define a function `?f` which is the the composition of two function (one extracting the localname out of a URI, another making a string uppercase).
The second `BIND` contain the actual `call:` that will execute the two functions.

    PREFIX call: <http://webofcode.org/wfn/call>
    PREFIX wfn: <http://webofcode.org/wfn/>
    PREFIX afn: <http://jena.hpl.hp.com/ARQ/function#>
    PREFIX fn:  <http://www.w3.org/2005/xpath-functions#>
    PREFIX myserver: <http://i-mozart.com/mywfn/>
        
    SELECT ?res {
      BIND(wfn:compose(afn:localname, fn:upper-case) as ?f)
      BIND(call:(?f, <http://addr.com/my#entity>) as ?res)
    }

In the following another similar example:

      PREFIX call: <http://webofcode.org/wfn/call>
      PREFIX wfn: <http://webofcode.org/wfn/>
      PREFIX afn: <http://jena.hpl.hp.com/ARQ/function#>
      PREFIX myserver: <http://i-mozart.com/mywfn/>
      
      SELECT ?res {
        BIND(wfn:compose(myserver:answerToAllQuestions,
                         afn:sqrt) as ?f)
        BIND(call:(?f) as ?res)
      }
  
  
Accessing +10k functions with `api-bridge`
---------------------------
What is the weather like in Verona right now?

      PREFIX wfn: <http://webofcode.org/wfn/>
      SELECT *
      {
         BIND(   
           wfn:api-bridge('community-open-weather-map/weather',
                  'lang=en&q=Verona&units=metric','main.temp') 
           as ?results
         )
      }

Or, what's the weather like in large Tuscany cities?

      PREFIX wfn: <http://webofcode.org/wfn/>
      PREFIX dbpedia: <http://dbpedia.org/resource/>
      PREFIX dbpedia-owl: <http://dbpedia.org/ontology/>
      PREFIX dbpprop: <http://dbpedia.org/property/>
      PREFIX geo: <http://www.w3.org/2003/01/geo/wgs84_pos#>
      PREFIX fn:  <http://www.w3.org/2005/xpath-functions#>
      
      SELECT ?city ?temperature_in_Celsius {
        SERVICE <http://dbpedia.org/sparql> {
          ?city a dbpedia-owl:Settlement.
          ?city dbpprop:region dbpedia:Tuscany.
          ?city dbpprop:populationTotal ?p.
          FILTER(?p > 100000)
          ?city geo:lat ?lat.
          ?city geo:long ?lon
        }
      BIND (fn:concat('lang=en&units=metric&lat=',str(?lat),'&lon=',str(?lon) ) as ?params)
      BIND( wfn:api-bridge('community-open-weather-map/weather',?params,'main.temp') as ?temperature_in_Celsius)
      }
  
This will show a list of largest tuscany cities with their current temperature in Celsius.
  
