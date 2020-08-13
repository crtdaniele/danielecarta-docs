---
id: typescript-optional-chaining
title: Optional Chaining
---

Disponibile dalla versione 3.7 di TS.

Se lavori in Javascript, sicuramente ti sarai imbattuto in oggetti con vari livelli di profondità. Spesso (e volentieri) ti sarà capitato di avere oggetti con tutti i vari livelli di profondità e altri con meno livelli di profondità.

Facciamo un esempio pratico:

```js
// versione 1
const bigObject = {
  // ...
  prop1: {
    //...
    prop2: {
      // ...
      value: 'Some value'
    }
  }
};

// versione 2
const bigObject = {
  // ...
  prop1: {
    // Nothing here   
  }
};
```
