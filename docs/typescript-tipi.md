---
id: typescript-tipi
title: Tipi di dato
---

Tipi di dato primitivi immutabili:

<ul>
    <li><a href="#boolean">Boolean</a></li>
    <li><a href="#number">Number</a></li>
    <li><a href="#null-e-undefined">Null</a></li>
    <li><a href="#string">String</a></li>
    <li>Symbol</li>
    <li><a href="#null-e-undefined">Undefined</a></li>
</ul>

A questi bisogna poi aggiungere Object.

TypeScript supporta tutti i tipi visti sopra in aggiunta ad alcuni non disponibili in Javascript.

## String

Teniamo presente che Typescript supporta i template string, quindi è possibile usare anche il carattere backtick.

<!--DOCUSAURUS_CODE_TABS-->
<!--Typescript-->

```js
const car: string = "Lamborghini Countach";
```

<!--END_DOCUSAURUS_CODE_TABS-->

## Number

<!--DOCUSAURUS_CODE_TABS-->
<!--Typescript-->

```js
const numeroDecimale: number = 73;
```

<!--END_DOCUSAURUS_CODE_TABS-->

## Boolean

<!--DOCUSAURUS_CODE_TABS-->
<!--Typescript-->

```js
let foo: boolean = false;
```

<!--END_DOCUSAURUS_CODE_TABS-->

## Array

Per dichiarare una variabile di tipo array, sono disponibili due diverse sintassi equivalenti. La prima prevede l'uso del tipo degli elementi seguito da parentesi quadre come mostrato nell'esempio che segue.

Prima versione

<!--DOCUSAURUS_CODE_TABS-->
<!--Typescript-->

```js
const videoGameConsoles: string[] = ['PS4', 'Xbox One S', 'Switch'];
```

<!--END_DOCUSAURUS_CODE_TABS-->

Seconda versione

<!--DOCUSAURUS_CODE_TABS-->
<!--Typescript-->

```js
const consoles2018: Array = ['PS4', 'Xbox One S', 'Switch'];
```

<!--END_DOCUSAURUS_CODE_TABS-->

## Tuple

Tipo di dato non presente in Javascript.

Possono essere usate per rappresentare un array di dimensione fissa i cui elementi sono di tipo diverso.

<!--DOCUSAURUS_CODE_TABS-->
<!--Typescript-->

```js
let driver: [string, number] = ['Ayrton Senna', 3];
```

<!--END_DOCUSAURUS_CODE_TABS-->

Quindi, ricapitolando avremo la certezza che le prime due posizioni dell'Array driver saranno string e number. Abbiamo comunque la possibilità di inserire nuovi elementi all'interno dell'array (solo stringhe e numeri in questo caso).

<!--DOCUSAURUS_CODE_TABS-->
<!--Typescript-->

```js
drive.push('Nuovo elemento');
```

<!--END_DOCUSAURUS_CODE_TABS-->

## Enum

Le enumerazioni costituiscono un altro tipo di dato non presente in Javascript.
Per definirli bisogna utilizzare la parola riservata "enum".

Gli elementi di un oggetto enum consentono di identificare dei valori numerici in maniera semplice e facilmente ricordabile.

<!--DOCUSAURUS_CODE_TABS-->
<!--Typescript-->

```js
enum PuntoCardinale {Nord, Sud, Ovest, Est};
const nord: PuntoCardinale = PuntoCardinale.Nord; // 0
```

<!--END_DOCUSAURUS_CODE_TABS-->

I valori numerici all'interno degli elementi sono sempre progressivi (se non vengono definiti dei valori) e partono sempre dal primo valore.

## Union

Grazie al carattere '|' è possibile combinare più tipi diversi in un nuovo 'tipo composto'. Se, per esempio, consideriamo il frammento di codice riportato sotto, la variabile prezzo può essere di tipo string oppure di tipo number.

<!--DOCUSAURUS_CODE_TABS-->
<!--Typescript-->

```js
let prezzo: string | number;

prezzo = 10.01;
prezzo = '€2.49';
```

<!--END_DOCUSAURUS_CODE_TABS-->

In questo caso la variabile prezzo potrà esser sia stringa che numero.

## Null e Undefined

Con null e undefined dobbiamo stare attenti anche al parametro di configurazione --strictNullChecks (nel nostro ts config).
Vediamo i due casi:

Senza --strictNullChecks

<!--DOCUSAURUS_CODE_TABS-->
<!--Typescript-->

```js
const prova: string | null = undefined;
```

<!--END_DOCUSAURUS_CODE_TABS-->

Il compilatore non ci darà nessun errore, se invece abbiamo --strictNullChecks a true allora il compilatore ci darebbe errore in quanto sarà possibile (per la const prova) dichiarare solo una stringa o appunto un null.
Quindi con --strictNullChecks a true, un tipo null può esser dichiarato solo a null e la stessa cosa è valida per i tipi undefined.

## Void

Il tipo void si utilizza per definire le funzioni che non ritornano un valore definito (funzioni senza return).

<!--DOCUSAURUS_CODE_TABS-->
<!--Typescript-->

```js
function log(message: string): void {
    console.log(message);
}
```

<!--END_DOCUSAURUS_CODE_TABS-->

Se invece avessimo una funzione che ritorna ad esempio una stringa

<!--DOCUSAURUS_CODE_TABS-->
<!--Typescript-->

```js
function log(message: string): string {
    console.log(message);
    return message;
}
```

<!--END_DOCUSAURUS_CODE_TABS-->

## Never

Il tipo never invece viene utilizzato per le funzioni che non restitusciono mai un valore quindi per funzioni che non vengono mai portate a termine (ad esempio una funzione che lancia un ciclio infinito).