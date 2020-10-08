---
id: redux-saga
title: Redux Saga
---

## Cos'è Redux Saga?

Redux-Saga è una libreria che serve a produrre side-effects sull’applicazione (ad esempio eseguire codice asincrono come effettuare il fetch di dati) in maniera più facile da gestire, più efficiente, facile da testare e migliore nella gestione degli errori.

Una particolarità di Redux Saga è quella di utilizzare i Generators (puntatori a funzione, utili per la gestione del codice asincrono, function\*).

Quindi, Redux Saga è un middleware che viene installato su Redux Saga è rimane in ascolto e viene utilizzato per effettuare chiamate asincrone e per la modifica dello stato dell'applicazione.

## Come si usa?

### Primo step

Installare Redux Saga all'interno del nostro progetto.
Ovviamente questo passaggio va fatto DOPO aver installato e configurato Redux.

```js
npm i redux-saga
```

### Actions

Come prima cosa, andiamo a creare delle actions (se vuoi approfondire le actions, <a href="https://danielecarta-docs.netlify.app/docs/redux#action">guarda qui</a>) all'interno del nostro progetto che serviranno per le richieste fetch che andremo a fare utilizzando Saga.

```js

```
