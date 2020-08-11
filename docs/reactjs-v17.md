---
id: reactjs-v17
title: ReactJS v17.0
---

10 Agosto 2020 - Esce la <b>versione 17 di React</b>, una release un po particolare in quanto chiamata (<b>No new feature</b>). Ebbene sì, una release senza grosse feature.

Questo rilascio è stato fatto per supportare e aiutare i vari aggiornamenti di versione.
Il team di React vuole semplificare sempre di più il passaggio da una versione all'altra.

<a href="https://reactjs.org/blog/2020/08/10/react-v17-rc.html"><b>Documentazione</b></a>

## Event Delegation

Un'altra importante novità di questo rilascio è l'<b>event delegation</b>, spiegato molto bene in questo schema.

<img src="https://reactjs.org/static/bb4b10114882a50090b8ff61b3c4d0fd/1e088/react_17_delegation.png">

Dalla versione 17 React si baserà sul nodo "root" e non più sul nodo html del document. Questa modifica permetterà di render sempre più isolata l'applicazione React per facilitare sempre di più ad esempio l'embed di un'applicazione React all'interno di un progetto già esiste scritto in altri linguaggi.