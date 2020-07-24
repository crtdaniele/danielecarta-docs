---
id: typescript-type
title: Type
---

I Type vengono in genere usati per definire strutture di dati tipo: Primitivi, Union, Object, Tuple.

<!--DOCUSAURUS_CODE_TABS-->
<!--JavaScript-->

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

<!--END_DOCUSAURUS_CODE_TABS-->

## Partial

Serve per creare un Type parziale da un altro Type. Ad esempio posso avere il Type User con 3 prioprietà, da questo Type posso creare un Partial Type per usare una sola proprietà.
Soluzione utile ma non pulitissima, meglio Omit e Pick.

<!--DOCUSAURUS_CODE_TABS-->
<!--JavaScript-->

```js
const user1: Partial<User> = {
    id: 1
}
```

<!--END_DOCUSAURUS_CODE_TABS-->

## Omit

Creare un nuovo Type omettendo alcune proprietà. In questo caso andremo a omettere la proprietà ID ad esempio per creare un nuovo Type di User che arriva da un form (quindi senza la proprietà id).

<!--DOCUSAURUS_CODE_TABS-->
<!--JavaScript-->

```js
type FormDataUser = Omit<User, 'id'>

const user1: FormDataUser = {
    name: "Daniele"
}
```

<!--END_DOCUSAURUS_CODE_TABS-->