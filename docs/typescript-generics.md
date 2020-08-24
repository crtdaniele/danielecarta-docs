---
id: typescript-generics
title: Generics
---

In Typescript, con i generici è possibile creare una funzione in cui il tipo dei parametri e del valore di ritorno non viene specificato fino al momento in cui la funzione viene invocata.

````ts
function printType<T>(arg: T): T {
  console.log(typeof arg);
  return arg;
}

printType<string>('ciao'); // string

printType<number>(17); // number

printType<object>({a: 1})

// oppure

printType<{a: number}>({a: 1})
printType({a: 1}); // object
````
