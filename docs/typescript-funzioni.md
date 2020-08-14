---
id: typescript-funzioni
title: Funzioni
---

## Tipizzazione

Anche per le funzioni è possibile tipizzare i vari parametri passati:

const myFunction = (a: string) => {
    console.log(a);
}

In questo esempio stiamo dichirando che myFunction prenderà un solo parametro in input e dovrà essere di tipo string.

## Valore di ritorno

Anche il valore di output però esser tipizzato:

const myFunction = (a: string): string => {
    return a;
}

In questo caso stiamo dicendo che la nostra funzione ritornerà una stringa.

## Parametri opzionali

Anche nelle funzioni è possibile passare dei parametri opzionali sempre con l'operatore ? (ti consiglio di leggere questa pagina sull'optional chaining).
