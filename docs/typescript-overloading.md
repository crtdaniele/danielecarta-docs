---
id: typescript-overloading
title: Function Overloading
---

Molto linguaggi prevedono la possibilità di avere definizioni multiple di una determinata funzione.
Anche in Typescript esiste questa possibilità e si chiama Function Overloading.

````ts
function add(a:string, b:string):string;

function add(a:number, b:number): number;

function add(a: any, b:any): any {
    return a + b;
}

add("Hello ", "Steve"); // returns "Hello Steve" 
add(10, 20); // returns 30 
````

In questo esempio, abbiamo definito due volte la funzione add, nella prima avremo la possibilità di passare due parametri string. Nella seconda possibilità invece potremo passare due parametri number.

Vi faccio notare, che quando si hanno molti casi, è possibile usare i <a href="">Generics di Typescript</a>.
Ovvero la possibilità di definire il tipo di dato solo quando si andrà a usare effettivamente la funzione.
