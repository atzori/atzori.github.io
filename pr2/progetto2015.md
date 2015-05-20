---
layout: page
title: Progetto 2015
---

Progetto PR2 (A.A. 2014/2015)
======================================
**Ultimo aggiornamento: 20 Maggio 2015**

Motivazione: 

  1. il progetto ha il fine di stimolare lo sviluppo di codice in gruppo, 
  1. utilizzare tecnologie di versionamento (git e github), 
  1. esercitarsi a comprendere codice scritto da altri, e 
  1. familiarizzare con Java 8 e le sue librerie. Possibilmente divertendosi.

Il progetto consiste nel realizzare 3 funzioni di LibreOffice di seguito denominate: _semplice_, _complessa_, e _custom_.

Si tratta di 3 classi diverse, nel package `it.unica.pr2.progetto2015`; ognuna implementa la seguente interfaccia:
```
package it.unica.pr2.progetto2015.interface;

public interface SheetFunction<I,O> {
  public O function(I[]);
}
```



Il progetto andra' testato su: Ubuntu Linux 14.04, jdk 1.7.0_55, LibreOffice 4.4.3, [Obba 4.2.2](http://obba.info/).
Nota: Obba 4.2.2 non supporta jdk 1.8.

Dovrà essere creato un repository PRIVATO (utilizzando bitbucket, gratuito) e reso pubblico solo i giorni della consegna.

Il repository conterrà 


modificare l'implementazione del gioco 2048 ([disponibile qui](https://github.com/atzori/fx2048), realizzata da B. Borges utilizzando JavaFX e Java 8) in modo da permettere, _opzionalmente_, di giocare autonomamente con un giocatore automatico. La modifica dovrà essere fatta utilizzando il fork di github partendo dal [progetto dato](https://github.com/atzori/fx2048).


Dovranno essere quindi realizzati 2 file jar. Supponendo di essere il gruppo 9, i file saranno:

 - Game2048_G9.jar (implementa il gioco modificando la versione data)
 - Game2048_player_G9.jar (implementa il giocatore automatico)



Il gioco potra' essere avviato nel seguente modo:

`java -cp Game2048_G9.jar:Game2048_player_G9.jar game2048.Game2048`




Il gioco dovra' funzionare anche con i giocatori automatici realizzati dagli altri gruppi e dal docente, ad esempio:

`java -cp Game2048_`**G9**`.jar:Game2048_player_`**G15**`.jar game2048.Game2048`



Per poter permettere che il gioco sia "disaccoppiato" dal giocatore automatico, e che quindi funzioni anche con giocatori automatici di altri gruppi, la logica del giocatore automatico deve essere implementata nella classe pubblica `giocatoreAutomatico.player.MyGiocatoreAutomatico` che deve implementare l'interfaccia `giocatoreAutomatico.GiocatoreAutomatico`:

```java
/* GiocatoreAutomatico.java */
package giocatoreAutomatico;


public interface GiocatoreAutomatico {

    /** restituisce un oggetto GiocatoreAutomatico su cui si potrà chiedere che mosse fare.  
     Lancia una eccezione se c'e' un problema nella creazione del giocatore automatico */
    public static GiocatoreAutomatico getGiocatoreAutomatico() throws Exception {
            return (GiocatoreAutomatico) Class.forName("giocatoreAutomatico.player.MyGiocatoreAutomatico").newInstance();
    }
    
    /**   restituisce 0=ALTO; 1=DX; 2=BASSO; 3=SX , ovvero la mossa che il giocatore automatico intende fare.
     * In input prende una griglia di gioco 4x4 che contiene la situazione del gioco corrente.
     * 
     * @see Griglia
     */
    public abstract int prossimaMossa(Griglia g);

}





/* Griglia.java */
package giocatoreAutomatico;

/** le classi che implementano questa interfaccia devono contenere esattamente 16 chiavi.
Alla Location (0,0), dovrà essere associato il numero (2, oppure 4, oppure 8, ...) associato a quella casella.
Qualora nella posizione non ci siano numeri, sarà associato il valore -1
*/
public interface Griglia extends java.util.Map<game2048.Location,Integer> { }


```

