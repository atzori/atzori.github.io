---
layout: page
title: Web of Functions - SPARQL call function
---

Web of Functions: Computing Custom Functions Remotely From Any SPARQL Endpoints
=================================================================

Introducing wfn:call
-------------------------------

We developed a SPARQL function called `wfn:call` that takes as a parameter a URI representing a function, followed by other arguments for the specified function.
The call function executes the specified URI function against an appropriate remote endpoint (that implements such a function), passing the arguments and getting the result back.
It allows interoperable remote invocation of functions (including higher-order functions -- HOF) from within a SPARQL query.


###Name space 

    wfn: <http://webofcode.org/wfn/>
    
###Download
Our open source implementation in Java of the `wfn:call` function is available at [bitbucket](https://bitbucket.org/atzori/callsparql/).
You can use it to enhance your Apache Jena / Fuseki installation, allowing the use of any custom function defined on other remote endpoints.

Further details will be available in a forthcoming paper at the Research Track of the [13th International Semantic Web Conference (ISWC14)](http://iswc2014.semanticweb.org/).



Simple Examples: Computing the concatenation of Strings from a Remote Endpoint
----------
Here you can find two simple examples of how to use the `wfn:call` function. It has been registered on our endpoint that you can find at: `http://service.webofcode.org/ jena/sparql`. The form to input the queries can be found at: `http://service.webofcode.org/ jena/sparql.html`


### Example 1: higher-order feature (binding functions to variables) 
Calling a function that is within a variable can be done as it follows:

    PREFIX wfn: <http://webofcode.org/wfn/>
    PREFIX fn: <http://www.w3.org/2005/xpath-functions#>
    SELECT *
    {
       BIND( fn:concat as ?f )
       BIND( wfn:call(?f,"alpha","BETA") as ?res )
    } 


### Example 2: forcing the computation to be run against a given endpoint (DBpedia)
Calling a function that is registered on a remote server can be done easily. In the following we are forcing to use the `fn:concat` (string concatenation) function implemeted in the remote DBpedia server.

    PREFIX wfn: <http://webofcode.org/wfn/>
    PREFIX fn: <http://www.w3.org/2005/xpath-functions#>
    SELECT *
    {
       BIND( wfn:call(CONCAT(STR(fn:concat),"@http://dbpedia.org/sparql"),"alpha","BETA") as ?res )
    } 

Another strategy for calling remote functions is based on the computation of the endpoint address from the function URI.
This is actually the suggested approach in the paper; it simply consists in transforming a function URI such as `http://somewebaddress.com/whatever/.../functionname` into the endpoint address `http://somewebaddress.com/whatever/.../sparql`. This way the remote endpoint address will not be required when calling a function.


A Nucleus for the Web of Open Functions
----------
As a boosting factor for the Web of Functions, we need a large enough set of functions forming a nucleus for the Web of Functions, allowing the user to appreciate the new features made available by the call function from within any SPARQL query.

We concentrated on a limited set of _auxiliary functions_ (reduce, compose and memoize) that emphatize the usefulness of the higher-order expressivity, together with hundreds of interesting functions made available through a bridge function that exposes all the [Mashape](http://www.mashape.com/) Web APIs.

### Auxiliary HOF functions: reduce, compose, memoize
`wfn:reduce` is taken from the functional languages world (sometimes called fold or aggregate): given a binary function and a set of values, it applies the functions to the first two values, then recursively to the result and the next value in the list. This can perform aggregation by using a function that may not support aggregation (for instance [`afn:max`](https://jena.apache.org/documentation/query/library-function.html)


### WebAPIs from within SPARQL queries: api-bridge
`wfn:call` 





