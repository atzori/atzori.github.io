---
layout: page
title: Computing Recursive SPARQL Queries
---

Computing Recursive SPARQL Queries
==================================

Introducing Recursion in SPARQL
-------------------------------

We developed a SPARQL function called `wfn:runSPARQL` that takes as a parameter a string containing a SPARQL query and executes it.
Such SPARQL query can refer to itself, enabling recursion and the use of any Turing-computable function within SPARQL.

Our work can be found in: 
[Computing Recursive SPARQL Queries](http://ieee-icsc.org/icsc2014/). Atzori M. _8th IEEE International Conference on Semantic Computing_ (2014)


Name space and Public Endpoint
----------
Officially, we plan to use the following namespace:

    wfn: <http://webofcode.org/wfn/>
    
In order to experiment it, we published an endpoint implmenting our `wfn:runSPARQL` function, available at:

    http://swipe.unica.it/ jena/sparql
    
    
An Example: Computing the Factorial
-----------------------------------

The following is an example of recursive SPARQL query that computes the factorial of 3: 

    PREFIX wfn: <http://webofcode.org/wfn/>
    SELECT ?result 
    { 
            # bind variables to parameter values 
            VALUES (?query ?endpoint) { ( 
                    "BIND ( IF(?i0 <= 0, 1, ?i0 * wfn:runSPARQL(?query,?endpoint, ?i0 -1)) AS ?result)" 
                    "http://swipe.unica.it/jena/sparql"
            )}
       
            # actual call of the recursive query 
            BIND( wfn:runSPARQL(?query,?endpoint,3) AS ?result)
    } 

It can be queried against our endpoint above, or using the web interface at:

    http://swipe.unica.it/ jena/sparql.html


