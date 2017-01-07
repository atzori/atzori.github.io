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
I tirocinanti, ai fini del riconoscimento dello svolgimento del tirocinio, hanno l'obbligo di compilare giornalmente il registro delle presenze in forma elettronica, messo a disposizione dal docente.


Software e Documentazione
-------------------------
Tool da utilizzare:

  - Linux Ubuntu
  - Bitbucket and Git
  - [Feature Branch Workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/feature-branch-workflow/)
  - Docker
  
Il software andrà elaborato utilizzando un repository [Bitbucket](https://bitbucket.org/) creato dal docente.
Di seguito una Checklist sintetica del contenuto del repository:

  - *README.md* ([sintassi markdown](https://confluence.atlassian.com/bitbucketserver/markdown-syntax-guide-776639995.html)) chiaro e completo in inglese con:
     - Titolo seguito da descrizione in 1-2 righe del progetto
     - *Install* con istruzioni su come installare ed eventualmente fare il build (compilazione, etc.) del software
     - *Getting Started* con istruzioni su come avviarlo dopo aver eseguito la procedura di Install
     - Eventuali altre sezioni necessarie
  - *[Dockerfile](https://docs.docker.com/engine/reference/builder/)* semplice con EXPOSE opportunamente settato su 8080 se necessita di una porta aperta. Il progetto dovrà funzionare con i comandi 
 ```bash
    docker build -t img/PROGETTO https://bitbucket.org/semanticweb/PROGETTO.git
    docker run --name PROGETTO --rm -p 127.0.0.1:8080:8080 img/PROGETTO
 ```
  - *.gitignore* e *.dockerignore* se opportuni
  - i file sorgente (i compilati e tutto cio' ottenibile dalla procedura di installazione descritta nel README non fanno inseriti nel repository)
 
