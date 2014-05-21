---
layout: page
title: Progetto Standard 2014
---

Progetto 2048 (progetto standard 2014)
======================================

Il progetto consiste nel modificare l'implementazione del gioco 2048 (già realizzato, implementato utilizzando JavaFX e Java 8) in modo da permettere, opzionalmente, di giocare autonomamente con un giocatore automatico.

Dovranno essere quindi realizzati 2 file jar. Supponendo di essere il gruppo 9, i file saranno:

 - Game2048_G9.jar (implementa il gioco modificando la versione data)
 - Game2048\_player\_G9.jar (implementa il giocatore automatico)

Il gioco potra' essere avviato nel seguente modo:

`java -cp Game2048_G9.jar:Game2048\_player\_G9.jar game2048.Game2048`

Il gioco dovra' funzionare anche con i giocatori automatici realizzati dagli altri gruppi e dal docente, ad esempio:

`java -cp Game2048_G9.jar:Game2048\_player\_`*G15*`.jar game2048.Game2048`



 - Fare un fork del progetto [fx2048](https://github.com/atzori/fx2048)
 - modificare il codice in modo da supportare il gioco automatico
 - realizzare un gioca
