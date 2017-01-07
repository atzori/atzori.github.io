---
layout: bootstrap
title: Documentation
---

Informazioni per Tirocinanti, Tesisti, Dottorandi, Contrattisti
===============================================================

Indice argomenti
----------------
  - Software e Documentazione
  - Timetable (tirocinanti)

Timetable (tirocinanti)
-----------------------
I tirocinanti hanno l'obbligo di compilare il registro delle presenze in forma elettronica, messo a disposizione dal docente.


Software e Documentazione
-------------------------
Tool da utilizzare:

  - Linux Ubuntu
  - Bitbucket and Git
  - [Feature Branch Workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/feature-branch-workflow/)
  - Docker
  
Il software andrà elaborato utilizzando un repository [Bitbucket](https://bitbucket.org/) creato dal docente.
Checklist:

  - *README.md* ([sintassi markdown](https://confluence.atlassian.com/bitbucketserver/markdown-syntax-guide-776639995.html)) chiaro e completo in inglese con:
     - Titolo seguito da descrizione in 1-2 righe del progetto
     - *Install* con istruzioni su come installare ed eventualmente fare il build (compilazione, etc.) del software
     - *Getting Started* con istruzioni su come avviarlo dopo aver eseguito la procedura di Install
     - Eventuali altre sezioni necessarie
  - *[Dockerfile](https://docs.docker.com/engine/reference/builder/)* semplice con EXPOSE opportunamente settato su 8080 se necessita di una porta aperta
 
