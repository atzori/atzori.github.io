---
layout: page
title: Web of Functions - SPARQL call function
---

Web of Functions: Computing Custom Functions Remotely From SPARQL Endpoints
=================================================================

Introducing wfn:call
-------------------------------

We developed a SPARQL function called `wfn:call` that takes as a parameter an URI representing a function and then other arguments for the specified function.
The wfn:call function executes the specified URI function against an appropriate remote endpoint (that implements such a function), passing the arguments and getting the result back.
It allows interoperable remote invocation of functions (including high-order functions) from within a SPARQL query.


Name space 
----------

    wfn: <http://webofcode.org/wfn/>
    
Download
----------
Our open source implementation in Java of the `wfn:call` function is available at [bitbucket](https://bitbucket.org/atzori/callsparql/).
You can use it to enhance your Apache Jena / Fuseki installation, allowing the use of any custom function defined on other remote endpoints.

Further details will be available here.
