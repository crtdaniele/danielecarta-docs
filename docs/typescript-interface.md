---
id: typescript-interface
title: Interface
---

Un interfaccia definisce un modello o specifica e chiunque implementerà quell'interfaccia dovrà poi andare a rispettare quelle determinate specifiche. Vediamo subito come.
In questo esempio andremo a definire un interfaccia Car con due proprietà:

interface Car {
  modello: string,
  marca: string
}

const car: Car = {modello: 'E-Type', marca: 'Jaguar'};

<em>Curiosità:</em> Typescript sfruttra il Duck Typing o Structural Subtyping per controllare se un oggetto rispetta quelle determinate specifiche.
