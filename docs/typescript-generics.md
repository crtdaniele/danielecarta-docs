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

## Classi Generiche

Possiamo definire anche delle classi generiche, senza definire il tipo di dato dei vari parametri della classe:

````ts
class Pair<T, U> {
  private firstElement: T;
  private secondElement: U;

  constructor(firstElement: T, secondElement: U) {
    this.firstElement = firstElement;
    this.secondElement = secondElement;
  }

  public getFirstElement(): T {
    return this.firstElement;
  }

  public getSecondElement(): U {
    return this.secondElement;
  }

  public getPair(): string {
    return `${this.firstElement} - ${this.secondElement}`;
  }
}

const cars = [
  new Automobile('McLaren', 'P1'),
  new Automobile('Ferrari', 'Portofino'),
  new Automobile('Rolls-Royce', 'Wraith')
];

const firstPair = new Pair<number, string>(3, 'Ayrton Senna');
const secondPair = new Pair<string, Automobile[]>('Lisa', cars);
const thirdPair = new Pair<string, string>('Australia', 'Canberra');
const fourthPair = new Pair<string, string>('ciao', 'hello');
````
