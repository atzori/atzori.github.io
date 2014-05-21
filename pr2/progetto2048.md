---
layout: page
title: Progetto Standard 2014
---

Progetto 2048 (progetto standard 2014)
======================================

Il progetto consiste nel modificare l'implementazione del gioco 2048 (già realizzato, implementato utilizzando JavaFX e Java 8) in modo da permettere, opzionalmente, di giocare autonomamente con un giocatore automatico.

Dovranno essere quindi realizzati 2 file jar. Supponendo di essere il gruppo 9, i file saranno:

 - Game2048_G9.jar (implementa il gioco modificando la versione data)
 - Game2048_player_G9.jar (implementa il giocatore automatico)



Il gioco potra' essere avviato nel seguente modo:

`java -cp Game2048_G9.jar:Game2048_player_G9.jar game2048.Game2048`




Il gioco dovra' funzionare anche con i giocatori automatici realizzati dagli altri gruppi e dal docente, ad esempio:

`java -cp Game2048_G9.jar:Game2048_player_`**G15**`.jar game2048.Game2048`



Per poter permettere che il gioco sia "disaccoppiato" dal giocatore automatico, e che quindi funzioni anche con giocatori automatici di altri gruppi, i giocatori automatici implementeranno la seguente interfaccia:

```java
/* GiocatoreAutomatico.java */
package giocatoreAutomatico;

public interface GiocatoreAutomatico {

    /** restituisce un oggetto GiocatoreAutomatico su cui si potrà chiedere che mosse fare.  */
    public static GiocatoreAutomatico getGiocatoreAutomatico(Griglia g);
    
    /** restituisce 0=ALTO; 1=DX; 2=BASSO; 3=SX , ovvero la mossa che il giocatore automatico intende fare*/
    public int prossimaMossa();
    

}

/* Griglia.java */
package giocatoreAutomatico;

/** le classi che implementano questa interfaccia devono contenere esattamente 16 chiavi.
Alla Location (0,0), dovrà essere associato il numero (2, oppure 4, oppure 8, ...) associato a quella casella.
Qualora nella posizione non ci siano numeri, sarà associato il valore -1
*/
public interface Griglia implements Map<game2048.Location,Integer>  {


}


```
