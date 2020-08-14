---
id: typescript-type-vs-interface
title: Type vs Interface
---

In questo articolo vorrei mostrarvi le differenze principali tra <a href="https://danielecarta-docs.netlify.app/docs/typescript-interface">Interface</a> e <a href="https://danielecarta-docs.netlify.app/docs/typescript-type">Type</a>. Sicuramente ti sarai già imbattuto nella domanda (quando lavoro in ReactJS con Typescript, come definisco le Props di un componente?).

## Oggetto base

Come noterai nell'esempio, la sintassi è molto simile:

```ts
type User = {
  name: string
}

interface User {
  name: string
}
```

## Array

In questo esempio c'è già qualche differenza: 

- La sintassi di Type è più breve
- Definendo in quel modo interface, avremo dei problemi in quanto Typescript non ci farà accedere a metodi come map, filter, ecc.

```ts
type Users = User[]

interface Users {
  [index: number]: User
}
```

A differenza di Type, se provassimo a fare mioArray.map il compilatore di Typescript ci darebbe errore:

```ts
interface User {
  name: string
}

interface Users {
  [index: number]: User
}

const mioArray: Users = [{name: "Daniele"}, {name: "Marco"}];

mioArray.map // error
```

Per avere lo stesso risultato di Type (per ora scritto in una sola riga) dovremmo andare a scrivere qualcosa di questo tipo:

```ts
interface Users extends Array<User> {
  [index: number]: User
}
```

## Funzioni

Sintassi praticamente uguale anche qui:

```ts
type GetUserFn = (name: string) => User
// ...
interface GetUserFn {
  (name: string): User
}
```

## Unione

Anche qui la sintassi per unire due Type o due Interface è molto simile tra di loro:

```ts
type SuperUser = User & { super: true }
// ...
interface SuperUser extends User {
  super: true
}
```

https://dev.to/reyronald/typescript-types-or-interfaces-for-react-component-props-1408
