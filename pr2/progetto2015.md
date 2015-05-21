---
layout: page
title: Progetto 2015
---

Progetto PR2 (A.A. 2014/2015)
======================================
**Ultimo aggiornamento: 21 Maggio 2015**

Motivazione: 

  1. il progetto ha il fine di stimolare lo sviluppo di codice in gruppo, 
  1. utilizzare tecnologie di versionamento (git e github), 
  1. esercitarsi a comprendere codice scritto da altri, e 
  1. familiarizzare con Java 8 e le sue librerie. Possibilmente divertendosi.

Il progetto consiste nel realizzare 3 funzioni di LibreOffice, implementate nelle seguenti classi: 
```
it.unica.pr2.progetto2015.gXXXXX.Semplice
it.unica.pr2.progetto2015.gXXXXX.Complessa
it.unica.pr2.progetto2015.gXXXXX.Custom
```
dove `XXX` è dato dal numero di matricola del componente del gruppo (5 cifre). Se il gruppo ha piu' componenti, si metteranno tutte le matricole dalla piu piccola alla piu grande separate dal simbolo `_`.
Per esempio: `it.unica.pr2.progetto2015.g12345_28957.Custom`

Ognuna ha un costruttore vuoto ed implementa la seguente interfaccia:
```
package it.unica.pr2.progetto2015.interface;

public interface SheetFunction {

  /** argomenti in input ed output possono essere solo: String, Integer, Long, Double, Character, Boolean e array di questi tipi.
  
  Ad esempio a runtime si puo' avere, come elementi di args, un Integer ed un Long[], e restituire un Double[];
  
  */
  Object execute(Object[] args) ;
  
  /** restituisce la categoria LibreOffice;
      vedere: https://help.libreoffice.org/Calc/Functions_by_Category/it
      
      ad esempio, si puo' restituire "Data&Orario" oppure "Foglio elettronico"
  */
  final String getCategory();
  
  /** informazioni di aiuto */
  final String getHelp(); 
 
 /** Nome della funzione.
     vedere: https://help.libreoffice.org/Calc/Functions_by_Category/it
     ad es. "VAL.DISPARI" 
  */         
 final String	getName();
}
```

Semplice
--------
La classe Semplice implementa una funzione LibreOffice (si veda la [lista di Funzioni LibreOffice](https://help.libreoffice.org/Calc/Mathematical_Functions/it)) semplice, ovvero che non restituisce un array.

Complessa
--------
La classe Semplice implementa una funzione LibreOffice (si veda la [lista di Funzioni LibreOffice](https://help.libreoffice.org/Calc/Mathematical_Functions/it)) piu' complessa, ovvero che restituisce un array o che richiede comunque uno sforzo maggiore nell'implementazione.

Custom
--------
La classe Custom implementa una funzione non presente in LibreOffice, a scelta dell'utente, utilizzando almeno una libreria esterna (ad esempio: [HtmlUnit](http://htmlunit.sourceforge.net/gettingStarted.html), [Twitter4J](http://twitter4j.org/en/index.html), [Dropbox Java API](https://www.dropbox.com/developers/core/start/java), o qualsiasi altra libreria esterna Java).

Alcune funzioni interessanti sono implementate in Google Sheet (si veda la [lista di Funzioni di Google Sheet](https://support.google.com/docs/table/25273?hl=it))

Note
----

Il progetto andra' testato su: Ubuntu Linux 14.04, jdk 1.7.0_55, LibreOffice 4.4.3, [Obba 4.2.2](http://obba.info/).
Nota: Obba 4.2.2 non supporta jdk 1.8.

Dovrà essere creato un **repository PRIVATO** (utilizzando bitbucket, gratuito) e reso pubblico solo i giorni della consegna.

Il repository conterrà la seguente struttura:

  - README.md   descrizione generale e comandi per funzionamento
  - foglio.ods  foglio elettronico LibreOffice con 3 fogli, ognuna con i test di ciascuna funzione
  - /java/it/unica/pr2/progetto2015/...   sorgenti java
  - /libs/ ...    librerie esterne utilizzate
  - /build/progetto2015.jar   file contentente i compilati, unico file da utilizzare in foglio.ods per i test
  - file di progetto Netbeans


