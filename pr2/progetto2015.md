---
layout: bootstrap
title: Progetto 2015
---

Progetto PR2 (A.A. 2014/2015)
======================================
**Ultimo aggiornamento: 27 Agosto 2015**
<!--
Consegna:

 - rendere *pubblico* il progetto, poi compilare il [Form di consegna](http://goo.gl/forms/O50ibZikwd). Non modificare il progetto dopo la compilazione del form. Non verranno prese in considerazione consegne successive all'2 Settembre alle 15.00. Come dalle regole dell'esame già comunicate, *la consegna e' necessaria per poter partecipare alla prossima prova di teoria/pratica di PR2*. I progetti verranno valutati e non potranno essere riconsegnati successivamente.

<!--
Consegna:

 - rendere *pubblico* il progetto per 3 giorni, poi compilare il [Form di consegna](http://goo.gl/forms/O50ibZikwd). Non modificare il progetto dopo la compilazione del form. Non verranno prese in considerazione consegne successive all'1 Luglio alle 15.00. Come dalle regole dell'esame già comunicate, *la consegna e' necessaria per poter partecipare alla prossima prova di teoria/pratica di PR2*. I progetti verranno valutati e non potranno essere riconsegnati successivamente.
 -->
 
Note e news:

 - *Eccezione InvocationTargetException con Obba.* Qualora venisse lanciata l'eccezione `java.lang.reflect.InvocationTargetException`, è necessario installare il pacchetto libreoffice-java-common col comando (su ubuntu) `sudo apt-get install libreoffice-java-common`


_Change Log_

 - 29 Maggio _assegnazione funzioni a studenti_; interfaccia varargs; _pubblicazione esempio_ 
 - 24 Maggio _aggiunta lista funzioni_
 - 21 Maggio _creato documento_

Motivazione: 
----------
  1. il progetto ha il fine di stimolare lo sviluppo di codice in gruppo, 
  1. utilizzare tecnologie di versionamento (git e bitbucket), 
  1. esercitarsi a comprendere codice scritto da altri, e 
  1. familiarizzare con Java 8 e le sue librerie. Possibilmente divertendosi.

Il progetto consiste nel realizzare 3 funzioni di LibreOffice, implementate nelle seguenti classi: 

```
it.unica.pr2.progetto2015.gXXXXX.Semplice
it.unica.pr2.progetto2015.gXXXXX.Complessa
it.unica.pr2.progetto2015.gXXXXX.Custom
```

dove `XXXXX` è dato dal numero di matricola del componente del gruppo (5 cifre). Se il gruppo ha piu' componenti, si metteranno tutte le matricole dalla piu piccola alla piu grande separate dal simbolo `_`.
Per esempio: `it.unica.pr2.progetto2015.g12345_28957.Custom`

Ognuna ha un costruttore vuoto ed implementa la seguente interfaccia:

```java
package it.unica.pr2.progetto2015.interfacce;

/** Implementa una singola funzione del foglio elettronico */
public interface SheetFunction {

	/** 
	Argomenti in input ed output possono essere solo: String, Integer, Long, Double, Character, Boolean e array di questi tipi.
	Ad esempio a runtime si puo' avere, come elementi di args, un Integer ed un Long[], e restituire un Double[];
	*/
	Object execute(Object... args) ;

	/** 
	Restituisce la categoria LibreOffice;
	Vedere: https://help.libreoffice.org/Calc/Functions_by_Category/it
	ad esempio, si puo' restituire "Data&Orario" oppure "Foglio elettronico"
	*/
	String getCategory();

	/** Informazioni di aiuto */
	String getHelp(); 

	/** 
	Nome della funzione.
	vedere: https://help.libreoffice.org/Calc/Functions_by_Category/it
	ad es. "VAL.DISPARI" 
	*/         
	String getName();
}
```

Semplice
--------
La classe Semplice implementa una funzione LibreOffice (si veda la [lista di Funzioni LibreOffice](https://help.libreoffice.org/Calc/Functions_by_Category/it)) semplice, ovvero che non restituisce un array.

Complessa
--------
La classe Complessa implementa una funzione LibreOffice (si veda la [lista di Funzioni LibreOffice](https://help.libreoffice.org/Calc/Functions_by_Category/it)) piu' complessa, ovvero che restituisce un array o che richiede comunque uno sforzo maggiore nell'implementazione.

Custom
------
La classe Custom implementa una funzione non presente in LibreOffice, a scelta dell'utente, utilizzando almeno una libreria esterna (ad esempio: [HtmlUnit](http://htmlunit.sourceforge.net/gettingStarted.html), [Twitter4J](http://twitter4j.org/en/index.html), [Dropbox Java API](https://www.dropbox.com/developers/core/start/java), o qualsiasi altra libreria esterna Java).

Alcune funzioni interessanti sono implementate in Google Sheet (si veda la [lista di Funzioni di Google Sheet](https://support.google.com/docs/table/25273?hl=it)), ad esempio `IMPORTXML`.


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
  - eventuali file di progetto Netbeans

Maggiori dettagli sulle modalità di consegna verranno pubblicati in questa pagina.

Assegnazione gruppi e funzioni
-------
La divisione in gruppi e le funzioni assegnate sono visibili [in questa tabella](https://docs.google.com/spreadsheets/d/1RjFGGm3GcKEHmfgZHQncrIbszDnhZ8K5qKL-Jnc6mP4/edit?usp=sharing).
Ad ogni studente è associata una funzione semplice ed una complessa che dovrà implementare come richiesto, oltre alla funzione custom.
Per i gruppi formati da più persone, il gruppo potrà scegliere una funzione semplice e una funzione complessa da implementare tra quelle assegnate ai propri componenti del gruppo.
I gruppi vanno comunicati al docente a lezione oppure via email. 

Esempio Repository Progetto (semplificato)
----------------
[Repository di esempio su GitHub](https://github.com/pr2unica/progetto2015)


<!--
Lista Funzioni
----

###Database
Le funzioni di questa categoria sono classificate _complesse_

DB.DEV.ST.POP
DB.DEV.ST
DB.PRODOTTO
DB.MEDIA
DB.MIN
DB.MAX
DB.VALORI
DB.CONTA.VALORI
DB.VAR.POP
DB.VAR
DB.SOMMA
DB.CONTA.NUMERI

###Data&Orario
Le funzioni di questa categoria sono tutte classificate _semplici_

FRAZIONE.ANNO
ANNO
GIORNO.LAVORATIVO
NUM.SETTIMANA_ADD
NUM.SETTIMANA
GIORNO.SETTIMANA
OGGI
ORARIO.VALORE
ORARIO
SECONDO
ADESSO
GIORNI.LAVORATIVI.TOT
MESE
MINUTO
ORA
FINE.MESE
DATA.MESE
DOMENICA.DI.PASQUA
GIORNO360
GIORNI
GIORNO
DATA.VALORE
DATA.DIFF
DATA


###Finanza
Le funzioni di questa categoria sono classificate _complesse_

AMMORT.ANNUO
RICEV.SCAD
VA
INTERESSE.RATA
TIR.COST
EFFETTIVO
EFFETTIVO_ADD
DURATA_ADD
TASSO.SCONTO
AMMORT
AMMORT.FISSO
AMMORT.PER
AMMORT.DEGR
INT.MATURATO.SCAD
INT.MATURATO.PER


###Informazione
Le seguenti funzioni sono _semplici_ tranne quelle che restituiscono degli array.

TIPO
NON.DISP
NUM
VAL.TESTO
VAL.RIF
VAL.DISPARI
ISODD
VAL.NUMERO
VAL.NON.TESTO
VAL.NON.DISP
VAL.LOGICO
VAL.FORMULA
VAL.PARI
ISEVEN
VAL.ERRORE
VAL.ERR
VAL.VUOTO
INFO
FORMULA
ATTUALE
CELLA

###Testo
Le seguenti funzioni sono considerate _semplici_.

VALORE
MAIUSC
UNICODE
CARATT.UNI
ANNULLA.SPAZI
TESTO
T
SOSTITUISCI
RICERCA
ROMANO
DESTRA.B
DESTRA
RIPETI
RIMPIAZZA
MAIUSC.INIZ
STRINGA.ESTRAI.B
STRINGA.ESTRAI
MINUSC
LUNGH.B
LUNGHEZZA
SINISTRA.B
SINISTRA
JIS
FISSO
TROVA
IDENTICO
VALUTA
DECIMALE
CONCATENA
CODICE
LIBERA
CODICE.CARATT
BASE
TESTO.BAHT
ASC
ARABO


###Matematica
Le seguenti sono considerate _semplici_ tranne quelle che restituiscono array.

CONVERTI
ARROTONDA.DIFETTO.PRECISO
ARROTONDA.DIFETTO
SEGNO
ARROTONDA.MULTIPLO
COSECH
SECH
COSEC
SEC
ARCCOS
ARCCOSH
RADQ
ARCCOT
ARCCOTH
ARCSEN
ARCSENH
ARCTAN
ARCTAN.2
ARCTANH
COS
COSH
COT
RADQ.PI.GRECO
COTH
GRADI
EXP
FATTORIALE
INT
PARI
MCD
MCD_ADD
CASUALE.TRA
MCM
LCM_ADD
COMBINAZIONE
COMBINAZIONE.VALORI
TRONCA
LN
LOG
LOG10
ISO.ARROTONDA.ECCESSO
ARROT.ECCESS.PRECISO
ARROTONDA.ECCESSO
PI.GRECO
CASUALE
MULTINOMINALE
POTENZA
SOMMA.SERIE
PRODOTTO
SOMMA.Q
RESTO
QUOZIENTE
RADIANTI
ARROTONDA
ARROTONDA.PER.DIF
ARROTONDA.PER.ECC
SEN
SENH
SOMMA
SOMMA.SE
TAN
TANH
SUBTOTALE
EUROCONVERT
DISPARI
ASS



###Matrice
Le funzioni di questa categoria sono _complesse_

MATR.TRASPOSTA
REGR.LIN
REGR.LOG
MATR.SOMMA.PRODOTTO
SOMMA.DIFF.Q
SOMMA.SOMMA.Q
SOMMA.Q.DIFF
TENDENZA
MATR.UNIT
FREQUENZA
MATR.DETERM
MATR.INVERSA
MATR.PRODOTTO
CRESCITA


###Statistica 
Le funzioni di questa categoria non sono utilizzate nel progetto

###Logica
Le funzioni di questa categoria sono _semplici_.

E
FALSO
SE
NON
O
VERO
XO

###Foglio elettronico
Le funzioni di questa categoria non sono utilizzate nel progetto


-->
