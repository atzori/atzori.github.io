---
title: A Gate for the Web of Functions
layout: page
keywords: SPARQL, query rewriting
---
A Gate for the Web of Functions
===============================
Ongoing work


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
      SERVICE wfn:gate {
        #BIND( wfn:api-bridge('community-open-weather-map/weather',?params,'main.temp') as ?temperature_in_Celsius)
        _:a wfn:function wfn:api-bridge.
        _:a wfn:output ?temperature_in_Celsius.
        _:a wfn:input1 'community-open-weather-map/weather' .
        _:a wfn:input2 ?params .
        _:a wfn:input3 'main.temp'
      }
      
      }
