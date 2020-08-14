---
id: typescript-funzioni
title: Funzioni
---

## Tipizzazione

Anche per le funzioni è possibile tipizzare i vari parametri passati:

```ts
const myFunction = (a: string) => {
    console.log(a);
}
```

In questo esempio stiamo dichirando che myFunction prenderà un solo parametro in input e dovrà essere di tipo string.

## Valore di ritorno

Anche il valore di output però esser tipizzato:

```ts
const myFunction = (a: string): string => {
    return a;
}
```

In questo caso stiamo dicendo che la nostra funzione ritornerà una stringa.

## Parametri opzionali

Anche nelle funzioni è possibile passare dei parametri opzionali sempre con l'operatore ? (ti consiglio di leggere questa pagina sull'<a href="https://danielecarta-docs.netlify.app/docs/typescript-optional-chaining">optional chaining</a>).

```ts
const myFunction = (a: string, b?: string) => {
    console.log(a);
    console.log(b);
}
```

In questo modo il parametro b sarà opzionale quindi potremo chiamare la funzione in questo modo:

```ts
myFunction("parametro 1");
// result: 
   parametro 1
   undefined
   
myFunction("parametro 1", "parametro 2");
// result: 
   parametro 1
   parametro 2
```

Nota bene una cosa, i parametri opzionali NON possono essere dichiarati prima di parametri obbligatori.
