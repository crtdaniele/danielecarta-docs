---
id: typescript-interface
title: Interface
---

Un interfaccia definisce un modello o specifica e chiunque implementerà quell'interfaccia dovrà poi andare a rispettare quelle determinate specifiche. Vediamo subito come.
In questo esempio andremo a definire un interfaccia Car con due proprietà:

```ts
interface Car {
  modello: string,
  marca: string
}

const car: Car = {modello: 'E-Type', marca: 'Jaguar'};
```

<em>Curiosità:</em> Typescript sfruttra il Duck Typing o Structural Subtyping per controllare se un oggetto rispetta quelle determinate specifiche.

## Proprietà opzionali

All'interno di un Interface possiamo anche definire proprietà opzionali:

```ts
interface Car {
  modello: string,
  marca: string,
  anno?: number
}
```

In questo caso, quando si implementerà l'interaccia Car, solo le prime due proprietà saranno indispensabili per non generare errori.

## Readonly

Un'altra cosa interessante è che possiamo definire delle proprietà in sola lettura:

```ts
interface User {
  email: string
}

const myUser: User = {email: crtdaniele@gmail.com};

// questo genererà un errore in quanto email non può esser valorizzata solo quando l'oggetto viene creato
myUser.email = "nuovaemail@prova.it";
```
