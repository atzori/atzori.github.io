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
        SERVICE <http://db.webofcode.org/sparql> {
          ?city a dbpedia-owl:Settlement;
                dbpprop:region dbpedia:Tuscany;
                dbpprop:populationTotal ?p.
          FILTER(?p > 100000)
          ?city geo:lat ?lat;
                geo:long ?lon
        }
      BIND (fn:concat('lang=en&units=metric&lat=',str(?lat),'&lon=',str(?lon) ) as ?params)
      
      SERVICE wfn:gate {
        #BIND( wfn:api-bridge('community-open-weather-map/weather',?params,'main.temp') as ?temperature_in_Celsius)
        _:a wfn:function wfn:api-bridge;
            wfn:output ?temperature_in_Celsius;
            wfn:input1 'community-open-weather-map/weather' ;
            wfn:input2 ?params ;
            wfn:input3 'main.temp' 
      }
      
      }


starting support on Sesame

    PREFIX wfn: <http://webofcode.org/wfn/>
    PREFIX dbpedia: <http://dbpedia.org/resource/>
    PREFIX dbpedia-owl: <http://dbpedia.org/ontology/>
    PREFIX dbpprop: <http://dbpedia.org/property/>
    PREFIX geo: <http://www.w3.org/2003/01/geo/wgs84_pos#>
    PREFIX fn:  <http://www.w3.org/2005/xpath-functions#>
        
    SELECT ?city ?temperature_in_Celsius {
            
      SERVICE wfn:gate {
        #BIND( wfn:api-bridge('community-open-weather-map/weather',?params,'main.temp') as ?temperature_in_Celsius)
        _:a wfn:function wfn:api-bridge;
            wfn:output ?temperature_in_Celsius;
            wfn:input1 'community-open-weather-map/weather' ;
            wfn:input2 ?lon ;
            wfn:input3 'main.temp' 
      } # service
        
    { select ?lon ?city {
        SERVICE <http://db.webofcode.org/sparql> {
          ?city a dbpedia-owl:Settlement;
                dbpprop:region dbpedia:Tuscany;
                dbpprop:populationTotal ?p.
          FILTER(?p > 100000)
          ?city geo:lat ?lat;
                geo:long ?lon
        } # service
    } } # inner select
    } # outher select

the following works both on Sesame and Jena (syntax problems with Virtuoso):

    PREFIX wfn: <http://webofcode.org/wfn/>
    PREFIX dbpedia: <http://dbpedia.org/resource/>
    PREFIX dbpedia-owl: <http://dbpedia.org/ontology/>
    PREFIX dbpprop: <http://dbpedia.org/property/>
    PREFIX geo: <http://www.w3.org/2003/01/geo/wgs84_pos#>
    PREFIX fn:  <http://www.w3.org/2005/xpath-functions#>
    
    SELECT ?city ?temperature_in_Celsius {
    
    
    { select ?lon ?lat ?city {
        SERVICE <http://db.webofcode.org/sparql> {
          ?city a dbpedia-owl:Settlement;
                dbpprop:region dbpedia:Tuscany;
                dbpprop:populationTotal ?p.
          FILTER(?p > 100000)
          ?city geo:lat ?lat;
                geo:long ?lon
        } # service
    } } # inner select
    
      BIND (fn:concat('lang=en&units=metric&lat=',str(?lat),'&lon=',str(?lon) ) as ?params)
    
      SERVICE wfn:gate {
        #BIND( wfn:api-bridge('community-open-weather-map/weather',?params,'main.temp') as ?temperature_in_Celsius)
        _:a wfn:function wfn:api-bridge;
            wfn:output ?temperature_in_Celsius;
            wfn:input1 'community-open-weather-map/weather' ;
            wfn:input2 ?params ;
            wfn:input3 'main.temp' 
      } # service
        
    } # outer select
