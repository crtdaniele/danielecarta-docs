---
id: typescript-type
title: Type
---

I Type vengono in genere usati per definire strutture di dati tipo: Primitivi, Union, Object, Tuple.

```js
// primitive
type Name = string;

// object
type PartialPointX = { x: number; };
type PartialPointY = { y: number; };

type User = {
    id: number;
    name: string;
    city: string;
}

// union
type PartialPoint = PartialPointX | PartialPointY;

// tuple
type Data = [number, string];
```

## Union

In questo esempio andremo a unire due Type. Il Type ChargeableCreditCard è un mix tra il primo e il secondo. Con il Type ChargeableCreditCard potremo andremo a dichiarare un oggetto con le proprietà di CreditCard e quelle di Chargeable che potranno esserci entrambe o solo una delle due (per via dell'operatore |).

```js
type CreditCard = {
  numberCard: string
  expMonth: number
  expYear: number
}

// Type with union operator
type Chargeable = { token: string } | { cvc: number }

type ChargeableCreditCard = CreditCard & Chargeable;
```

## Partial

Serve per creare un Type parziale da un altro Type. Ad esempio posso avere il Type User con 3 prioprietà, da questo Type posso creare un Partial Type per usare una sola proprietà.
Soluzione utile ma non pulitissima, meglio Omit e Pick.

```js
const user1: Partial<User> = {
    id: 1
}
```

## Omit

Creare un nuovo Type omettendo alcune proprietà. In questo caso andremo a omettere la proprietà ID ad esempio per creare un nuovo Type di User che arriva da un form (quindi senza la proprietà id).

```js
type FormDataUser = Omit<User, 'id'>

const user1: FormDataUser = {
    name: "Daniele"
}
```
