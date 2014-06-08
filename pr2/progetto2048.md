---
layout: page
title: Progetto Standard 2014
---

Progetto 2048 (progetto standard 2014)
======================================
**Ultimo aggiornamento: 8 Giugno 2014**

Motivazione: il progetto ha il fine di stimolare lo sviluppo di codice in gruppo, utilizzare tecnologie di versionamento (git e github), esercitarsi a comprendere codice scritto da altri, e familiarizzare con Java 8 e JavaFX. Possibilmente divertendosi.

Il progetto consiste nel modificare l'implementazione del gioco 2048 ([disponibile qui](https://github.com/atzori/fx2048), realizzata da B. Borges utilizzando JavaFX e Java 8) in modo da permettere, _opzionalmente_, di giocare autonomamente con un giocatore automatico. La modifica dovrà essere fatta utilizzando il fork di github partendo dal [progetto dato](https://github.com/atzori/fx2048).


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


