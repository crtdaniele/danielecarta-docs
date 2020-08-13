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

## Proprietà variabili

Come potrai notare negli esempi precedenti, abbiamo sempre definito di determinato tipo di dato nelle varie proprietà.
Ad esempio la proprietà email era di tipo string, e così via.
Con l'operatore | possiamo andare a definire più di un tipo di dato:

```ts
interface User {
  age: number | string
}
```

Mettiamo caso che il valore di "age" arrivi da una chiamata API e non sappiamo di preciso se il dato arriverà in formato numero o stringa.
In questo modo potremo assegnare entrambi i tipi nella proprietà age.
