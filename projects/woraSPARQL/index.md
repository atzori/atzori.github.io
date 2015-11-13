---
layout: page
title: Write-Once Run-Anywhere (WORA) Custom Sparql
keywords: SPARQL, Web of Functions, source code, Java, Custom Functions
---
Write-Once Run-Anywhere (WORA) Sparql
================
This is the official page for the woraSPARQL project. 
In the following we provide technical information about the *bif:callJ()* function, which is the core of the woraSPARQL project.
The project repository will be open for everyone after the ongoing code review process.


The *bif:callJ()* is a custom function implemented on OpenLink Virtuoso. It is written with C programming language. However, thanks to the behavior of callJ inside Virtuoso, we wrote some Java Classes, since the meaning of callJ is that to execute Java methods inside SPARQL. 

## Semantics of bif:callJ##
The *bif:callJ()* is a function that is able to execute a method of a java class. The java class must be written expressly for this purpose and It must have a specific format described afterwards. 
The function takes two arguments that are two strings representing respectively the name of the class and the name of the method that we want to call; the function takes also zero or more arguments, representing the method arguments. 
Therefore, the callJ will have the following syntax:
	
	bif:callJ("className", "methodName", [arg1,...,argN])

## Implementation of bif:callJ##
For the correct behavior of the callJ we used a standard programming interface thanks to which is possible to call java methods inside C language and, vice versa, itâ€™s possible to call C functions inside Java Native Methods. This programming interface is named JNI, an acronym for Java Native Interface.  

### Java Native Interface behavior inside bif:callJ###
The *jni.h* library usable inside a C program contains some functions thanks to whom itâ€™s possible to call java methods and retrieve their result without any trouble. To be able to be executed, the function must have to be compiled first, because the library creates a Java Virtual Machine (JVM) that needs .class (compiled java classes extension) files to execute them. The creation of the JVM is possible thanks to this function:
	
	JNI_CreateJavaVM(JavaVM** jvm, void** p_env, void* vm_args)

This function takes three arguments as input, the first represents a reference to the JVM, the second argument represents the environment and the third argument represents the initialization arguments. After the virtual machine has been initialized, the variable named â€œp_envâ€ consists in a structure that contains a set of useful functions. Now we need to find the class and the method to be executed. Using the previous example of callJ, the function used to find out the class containing the method is the following:
	
	jclass cls = (*penv)->FindClass(â€œclassNameâ€)

The returned value will be a reference of the searched class; it will be useful to find out one of its methods and then call it.
To find the searched method, we need to use the following function:
	
	jmethodID mid = (*penv)->GetStaticMethodID(jclass cls, char* methodName, char* Signature)

The string named Signature must have a particular format, it contains the method signature, that is the input parameters types and the returned value type. We have decided to standardize the methods signatures, they will take one array of strings ad input and they will return a string. The signature in GetStaticMethod function follow the following pattern:

| Type Signature 			| 			Java Type		|
|      :--    	 			|    			--:			|
|  		Z		 			|  			boolean 		|
|		B					|  			byte			|
|		C					|  			char			|
|		S					|  			short			|
|		I					|  			int				|
|		J					|  			long			|
|		F					|  			float			|
|		D					|  			double			|
|Lfully-qualified-class;	|  	Fully qualified class	|
|		[type				|  		Array of 'type'		|
|(arg-types)ret-type		|  		Method signature	|

Therefore, the value of Signature string will be the following: â€œ([Ljava/lang/String;)Ljava/lang/String;â€ that matches to a java method: String methodName (String[]).
Now, since we have a class and a method reference, we need to call this method passing the remain arguments, if there are. The function to use is the following:

	jobject CallStaticObjectMethod(jclass cls, jMethodID mid, jtype args)

The variable named â€œargsâ€ can have several types but, as we said, it will be a vector of strings. Since, except for the first two arguments, we donâ€™t know the input argument types, we need to check the type of each argument and insert it into a string. To preserve it, the original type information is put at the beginning of the string, separating it from the type with a â€˜@â€™ character. For example, if callJ takes three arguments (Class name, method name, method argument), and the third argument is an integer, the argument passed to the method will be a vector of string containing only one element, that is â€œint@valueâ€. To be able to pass the vector to the method with the CallStaticObjectMethod, we need to insert it into a variable with the type jobjectArray. To create a vector with the Java Native Interface we need to use the following function:

	jobjectArray NewObjectArray(JNIEnv *env, jsize length, jclass elementClass, jobject initialElement);


The first argument is the environment, the second argument represents the vector length, the third argument represents the vector type (in our case is String), the fourth argument is the vectorâ€™s first element; The fourth argument can also be a null argument, if we donâ€™t need to put now the first argument into the vector. 
If we need to put an element into the vector we need to use this function:

	void SetObjectArrayElement(JNIEnv *env, jobjectArray array, jsize index, jobject value)

through which the object named value is added into the vector named array at the position with index index. 
After that, we have the vector with all the arguments in it, and we are ready to call the method with the CallStaticObjectMethod function. 
The CallStaticObjectMethod function will return a string that contains the returned value and type, in the same format as the input. The value retrieved from this string is exactly the value that the callJ will return. 

### Java classes format###
As we said previously, to be able to be executed by the callJ, the java classes must have a specific format. The method restrictions are the following:

+ Methods must be public (through the public keyword before the method name) and static (through the static keyword before the method name and after public);
+ The input argument must be just one and it must be a vector of objects of type String;
+ The vector strings must have the following form: â€œtype@dataâ€; since the callJ is only a prototype, the supported type attributes are String, int (integer) and float (floating point);
+ The output value must be a string having the same format as input strings;

To be able to handle data, we need to extrapolate it from strings. The Java programming language provides several functions to make it easy. For example, the following code extrapolate a String type data, supposing that s is an element of the input vector. 

	if(s.contains("String@")){
	String data = new String();
	int indexData = s.indexOf("@");
	data = s.substring(indexData+1, s.length());
	}

In this way the string named â€œdataâ€ will contain exactly the data, excluding all the rest.

## Experiments using Web OF Functions implementations##

We tested the framework by implementing two functions that realize the **Web of Functions** in Virtuoso. 
One is written in C, and it is a pure Virtuoso custom function. The second one is written in Java and itâ€™s used thanks to *bif:callJ* 
We start with a simple query, the version using callF is the following:

	PREFIX fn: <http://www.w3.org/2005/xpath-functions#>
	SELECT ?res{
	VALUES (?a) {("")}
	BIND ( bif:callF( CONCAT(STR(fn:concat),
	"@http://dbpedia.org/sparql"), 
	"alpha", "BETA") as ?res )
	}

This query computes the string concatenation between the string "alpha" and the string "BETA". The computation is performed by forcing it to be run against the endpoint at the URI \url{http://dbpedia.org/sparql}.
The execution times for both *bif:callF* and *bif:callJ* implementations are the following:

| **Function**	 			| **Execution time (in milliseconds)**	|
|      :--    	 			|    			--:						|
| 	*bif:callF()* 			|  				397 					|
|	*bif:callJ()* 			|  				540						|

Now we define a more complex query, that uses more than one calls to either callF or callJ. The query using the callJ version is the following. Note that the Java class written to implement the Web of Functions is "Call_Java", while the method that we need to executed is "call":

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
		?city geo:long ?lon}
	BIND(bif:callJ("Call_Java", "call", fn:concat,"lang=en&units=metric&lat=",
	str(?lat),"&lon=",str(?lon) ) as ?params)
	BIND(bif:callJ("Call_Java", "call",wfn:api-bridge,
	"community-open-weather-map/weather",
	?params,"main.temp") as ?temperature_in_Celsius)
	}

This query computes the temperature of the Tuscany cities with more than 100.000 inhabitants (the *?p* variable). In this case the *callF* (or *callJ*) is called six times (three times the first one and three time the second one). These are the execution times:

| **Function**	 			| **Execution time (in milliseconds)**	|
|      :--    	 			|    			--:						|
| 	*bif:callF()* 			|  		1550 (258 ms per call)			|
|	*bif:callJ()* 			|  		2303 (384 ms per call)			|

If we change the *?p* variable to 60.000, the *callF* (or *callJ*) is called 20 times (10 times the first one and ten times the second one). These are the execution times in this case:

| **Function**	 			| **Execution time (in milliseconds)**	|
|      :--    	 			|    			--:						|
| 	*bif:callF()* 			|  		4481 (224 ms per call) 			|
|	*bif:callJ()* 			|  		8039 (401 ms per call)			|

The execution times show that the native implementation (*bif:callF*), as expected, has faster running times than the *bif:callJ*. 
Anyway, they are both fast and require the same order of magnitude in terms of millisecond, proving that the bif:callJ is effective and can be used for real case loads.

We recall that the callF is written in pure C code, with the utilization of system libraries, like TCP socket creation for HTTP requests, which make the code harder to maintain, also reducing the portability with other operating systems that use different libraries.
Therefore, at the cost of a slower but acceptable running time, we have that callJ, written in Java, offers high portability, with Java libraries that are usable in all operative system having the Java runtime. The code also is easier to maintain and the same implementation can be used on other SPARQL engines that use Java, such as Apache Jena/Fuseki and Sesame. 

## Deployment##

**You need to install OpenLink Virtuoso before this installation process**

You need to put these files in the corresponding paths:

+ bif_call.c ---> virtuoso-opensource/libsrc/Wi/
+ bif_call_JNI.c ---> virtuoso-opensource/libsrc/Wi/
+ sqlbif.c   ---> virtuoso-opensource/libsrc/Wi/ (sovrascriverlo)
+ Makefile   ---> virtuoso-opensource/libsrc/Wi/ (sovrascriverlo)
+ libwi_la-bif_call.Plo ---> virtuoso-opensource/libsrc/Wi/.deps/
+ libwi_odbc_la-bif_call.Plo ---> virtuoso-opensource/libsrc/Wi/.deps/
+ invoke 	   ---> usr/local/virtuoso-opensource/var/lib/virtuoso/db *Occorre avere i permessi di root per poter svolgere questa operazione*

The "Java_classes" folder must be put in the following path:
*usr/local/virtuoso-opensource/var/lib/virtuoso/db*

**The java classes written for callJ must be put in this folder**

To complete the installation process, you need to open the terminal and change directory to the main virtuoso-opensource folder and execute the following commands:

1. *sudo make*
2. *sudo make install*

The process will take a few minutes.
