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

Il problema ora è che per scrivere del codice stabile, ti ritroverai a scrivere qualcosa tipo questo:

```js
if (bigObject && 
    bigObject.prop1 != null && 
    bigObject.prop1.prop2 != null) {
  let result = bigObject.prop1.prop2.value;
}
```

Con Typescript abbiamo a disposizione l'operatore ? (optional chaining) che ci semplifica la vita in situazioni con oggetti molto profondi:

```js
let ListaAuto = [{
    nome: "Daniele",
    auto: {
        marca: "BMW",
        dati: {
            modello: "Serie 1"
        }
    }
},{
    nome: "Marco",
    auto: {
        marca: "Audi"
    }
}];

ListaAuto.map(auto => {
    console.log(auto.auto.dati?.modello);
});
```

In questo esempio, il secondo oggetto non ha la proprietà <em>dati</em>, quindi accedere direttamente a auto.auto.dati?.modello comporterebbe un errore in quanto non esistono quelle proprietà.
Scrivendo però auto.auto.dati?.modello il compilatore non genererà nessun tipo di errore ma stamperà semplicemente in console:

```js
Serie 1
Undefined
```
