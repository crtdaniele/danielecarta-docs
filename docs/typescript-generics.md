---
id: typescript-generics
title: Generics
---

In Typescript, con i generici è possibile creare una funzione in cui il tipo dei parametri e del valore di ritorno non viene specificato fino al momento in cui la funzione viene invocata.

In questo esempio, il parametro T definirà il tipo di dato in input e in output.

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

Possiamo quindi creare anche un interfaccia da riutilizzare più volte:

````ts
interface GenericPrintFn {
  <T>(arg: T[]): T[];
}

function printType<T>(arg: T[]): T[] {
  console.log(typeof arg);
  return arg;
}

const printFunc: GenericPrintFn = printType;

printFunc<number>([0, 1, 2]); // object
````

In alternativa, possiamo definire il tipo T all'intera interfaccia:

````ts
interface GenericPrintFn<T> {
  (arg: T): T;
}

function printType<T>(arg: T): T {
  console.log(typeof arg);
  return arg;
}

const printFunc: GenericPrintFn<string> = printType;

printFunc('ciao'); // string
````
