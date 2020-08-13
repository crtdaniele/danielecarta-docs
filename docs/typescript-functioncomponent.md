---
id: typescript-functioncomponent
title: Function Component in Typescript
---

# Usare FunctionComponent oppure no?

Una delle differenze è che FunctionComponent porta di default con se i children.
Cosa vuol dire questo? Vediamo un esempio pratico sulla differenza tra definire un FuncionComponent con e senza.

## Con

In questo esempio, non ho bisogno di andare a definire children all'interno della Props in quanto FunctionComponent porta sempre con se i children:

```js
type Props = {
  title: string
}

const App: FunctionComponent<Props>  = ({title, children}) => {

  return (
    <div className="App">
      {title}
    </div>
  );
}
```

## Senza

In questo esempio abbiamo dichiarato il componente senza FunctionComponent, questo comporta che non è possibile passare dei children:

```js
type Props = {
  title: string
}

const App  = ({title}: Props) => {

  return (
    <div className="App">
      {title}
    </div>
  );
}
```

Per andare a passare dei children, dovrei andare a tipizzare anche children all'interno di Props:

```js
type Props = {
  title: string,
  children: React.ReactNode
}

const App  = ({title, children}: Props) => {

  return (
    <div className="App">
      {title}
    </div>
  );
}
```
