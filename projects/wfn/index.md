---
layout: page
title: Web of Functions
keywords: SPARQL, Web of Functions, Remote function calls
---

Web of Functions
================
The [Web of Functions](http://webofcode.org/wfn/) is a simple, backward-compatible way to computing custom functions remotely from any SPARQL endpoint. It is named after the Web of Data, since every function is associated with a (potentially dereferenciable) URI, thus forming the Web of Functions.

Introducing wfn:call
-------------------------------
In order to access the Web of Functions, we developed a SPARQL function called `wfn:call` that takes as a parameter a URI representing a function, followed by other arguments for the specified function.
The call function executes the specified URI function against an appropriate remote endpoint (that implements such a function), passing the arguments and getting the result back.
It allows interoperable remote invocation of functions (including higher-order functions -- HOF) from within a SPARQL query.


### Name space 
The official namespace is the following:

    wfn: <http://webofcode.org/wfn/>

The call function can be also defined through the following prefix:

    call: <http://webofcode.org/wfn/call>

This way, you can call a function by using the simpler syntax `call:(?functionURI, ?arg1, ?arg2, ...)`

    
### Download
Our open source implementation in Java of the `wfn:call` function is available at [bitbucket](https://bitbucket.org/atzori/callsparql/).
You can deploy it on your Apache Jena / Fuseki installation, allowing the use of `wfn:call` and therefore of any custom function defined on other remote endpoints.
Technical details and how-tos will be available shortly.

###Publications
Details are available in our papers discussed at the [International Semantic Web Conference 2014](http://iswc2014.semanticweb.org/):

 1. [Toward the Web of Functions: Interoperable Higher-Order Functions in SPARQL](https://github.com/lidingpku/iswc2014/raw/master/paper/87970401-toward-the-web-of-functions-interoperable-higher-order-functions-in-sparql.pdf). Atzori M. _ISWC 2014 - Proceedings of the 13th International Semantic Web Conference_, Research Track, [doi](http://dx.doi.org/10.1007/978-3-319-11915-1_26) (2014)
 1. [call: A Nucleus for a Web of Open Functions](http://ceur-ws.org/Vol-1272/paper_13.pdf). Atzori M. _ISWC 2014 - Proceedings of the 13th International Semantic Web Conference_, Demo Track (2014)

Simple Examples: Computing the concatenation of Strings from a Remote Endpoint
----------
Here you can find two simple examples of how to use the `wfn:call` function. It has been registered on our endpoint that you can find at: `http://webofcode.org/wfn/sparql`. The form to input the queries can be found [here](http://webofcode.org/wfn/sparql.html).


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

### Example 3: calling a remote function in the Web of Functions
Another strategy for calling remote functions is based on the *computation of the endpoint address from the function URI*.
This is actually the suggested approach in the paper; it simply consists in transforming a function URI such as `http://somewebaddress.com/whatever/.../functionname` into the endpoint address `http://somewebaddress.com/whatever/.../sparql`. This way the remote endpoint address will not be required when calling a function.

For instance, in order to call the function `http://i-mozart.com/mywfn/answerToAllQuestions`, a function without parameters that computes [the answer to all questions](http://en.wikipedia.org/wiki/Phrases_from_The_Hitchhiker%27s_Guide_to_the_Galaxy#Answer_to_the_Ultimate_Question_of_Life.2C_the_Universe.2C_and_Everything_.2842.29) (as per the novel [The Hitchhiker's Guide to the Galaxy](http://en.wikipedia.org/wiki/The_Hitchhiker's_Guide_to_the_Galaxy), just the constant `42`), we can write:

    PREFIX wfn: <http://webofcode.org/wfn/>
    SELECT *
    {
       BIND( wfn:call(<http://i-mozart.com/mywfn/answerToAllQuestions>) as ?res )
    } 

getting the value `42` for the variable `?res`. The computation is performed by interrogating the server at `http://i-mozart.com/mywfn/sparql`

A Nucleus for the Web of Open Functions
----------
As a boosting factor for the [Web of Functions](http://webofcode.org/wfn/), we need a large enough set of functions forming a nucleus for the Web of Functions, allowing the user to appreciate the new features made available by the call function from within any SPARQL query.

We concentrated on a limited set of _auxiliary functions_ (reduce, compose and memoize) that emphatize the usefulness of the higher-order expressivity, together with hundreds of interesting functions made available through a bridge function that exposes all the [Mashape](http://www.mashape.com/) Web APIs.
The following describes the functions described in our ISWC14 demo paper (more info will be available in the paper).
The function `wfn:compose` is available in our public endpoint.

### Auxiliary HOF functions: reduce, compose, memoize
`wfn:reduce` is taken from the functional languages world (sometimes called [fold or aggregate](http://en.wikipedia.org/wiki/Fold_(higher-order_function)): given a binary function and a set of values, it applies the functions to the first two values, then recursively to the result and the next value in the list. This can perform aggregation by using a function that may not support aggregation (for instance Jena's binary [`afn:max`](https://jena.apache.org/documentation/query/library-function.html).

`wfn:compose` allows [function composition](http://en.wikipedia.org/wiki/Function_composition) in the Web of Functions, showing a powerful example of Higher-order function where functions are used as input and output at the same time.

`wfn:memoize` is a [memoization function](http://en.wikipedia.org/wiki/Memoization), that is, produces a copy of the given functions, with the only difference that computed results are cached, making successive calls faster if same parameter values are used (note: memoize is currently unavailable on our endpoint).

### WebAPIs from within SPARQL queries: api-bridge
`wfn:api-bridge` is a function that allows to use any Web API found at the  [Mashape](http://www.mashape.com/) Hub service. Hundreds of functions will be therefore accessible within SPARQL by using the api-bridge extension function.
The syntax is the following:

    wfn:api-bridge(apiName, getParameters [, json_path])

For instance, if we want to get a json with weather information on the area at a given (latitude, longitude), using the [Mashape API](http://www.mashape.com/community/open-weather-map) made available by the [Open Weather Map initiative](http://openweathermap.org/) as _community-open-weather-map_ (with endpoint _/weather_), we can call the following:

    BIND( wfn:call(wfn:api-bridge, "community-open-weather-map/weather", ?parameters) as ?json).

If we are interested in just the temperature field (that is, "main.temp" in the JSON structure returned), we can specify a third optional parameter:

    BIND( wfn:call(wfn:api-bridge, "community-open-weather-map/weather", ?parameters,
      "main.temp") as ?temperature).
      
or, assuming we have a `wfn:json-field` parsing function, the logically equivalent:

    BIND( wfn:call(wfn:api-bridge, "community-open-weather-map/weather", ?parameters) as ?json).
    BIND( wfn:call(wfn:json-field, ?json, "main.temp") as ?temperature).


A complete query can be found in the [SPARQL examples page](http://atzori.webofcode.org/projects/wfn/examples), where the query gets large cities in Tuscany and their current (at query time) temperature in Celsius.


### Taking Advantage of HOF: Efficiently retrieving weather data

Unfortunately, if we want to get both temperature and, for instance, the humidity, will need two distinct calls to the API service:

    BIND( wfn:call(wfn:api-bridge, "community-open-weather-map/weather", ?parameters,
      "main.temp") as ?temperature).
    BIND( wfn:call(wfn:api-bridge, "community-open-weather-map/weather", ?parameters,
      "main.humidity") as ?humidity).

Memoization wouldn't help, since the last parameter (field) has a different value.
Instead, a more efficient solution that takes advantage of the auxiliary function would be defining first:

    BIND( wfn:compose(wfn:json-field,  wfn:memoize( wfn:api-bridge )) as ?fast_api_bridge).
    
and then, use it:

    BIND( wfn:call( ?fast_api_bridge, "community-open-weather-map/weather", ?parameters,
      "main.temp") as ?temperature).
    BIND( wfn:call( ?fast_api_bridge, "community-open-weather-map/weather", ?parameters,
      "main.humidity") as ?humidity).

The second call would be extremely fast, since it will not involve the open weather API, memoized through the compose function.

More Examples
-------------
Other examples of usage can be found on the [examples page](http://atzori.webofcode.org/projects/wfn/examples)

Contacts
----------
If you are interest in the Web of Functions, want to use it, contribute and/or make your own function available within the Web of Functions, feel free to [email me](mailto:atzori@unica.it).



