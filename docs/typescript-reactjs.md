---
id: typescript-reactjs
title: Typescript in ReactJS
---

## Definire le Props

Esempio molto semplice per definire le Props di un functional component con Type

<!--DOCUSAURUS_CODE_TABS-->
<!--Typescript-->

```js
import React from 'react'; // we need this to make JSX compile

type CardProps = {
  title: string,
  paragraph: string
}

export const Card = ({ title, paragraph }: CardProps) => <aside>
  <h2>{ title }</h2>
  <p>
    { paragraph }
  </p>
</aside>

const el = <Card title="Welcome!" paragraph="To this example" />
```

<!--END_DOCUSAURUS_CODE_TABS-->

In questa parte { title, paragraph }: CardProps viene utilizzato il destructuring per estrarre le proprietà di CardProps e accedere direttamente alle proprietà senza dover scrivere CardProps.title.

Invece in questo esempio di Type andremo a difinire delle proprietà non obbligatorie

<!--DOCUSAURUS_CODE_TABS-->
<!--Typescript-->

```js
type CardProps = {
  title: string,
  paragraph?: string  // the paragraph is optional
}
```

<!--END_DOCUSAURUS_CODE_TABS-->

Quindi in questo caso, utilizzato l'optional chaining andremo a difinire opzionale la proprietà paragraph.

Un altro esempio

<!--DOCUSAURUS_CODE_TABS-->
<!--Typescript-->

```js
import React, { FunctionComponent } from 'react'; // importing FunctionComponent

type CardProps = {
  title: string,
  paragraph: string
}

export const Card: FunctionComponent<CardProps> = ({ title, paragraph }) => <aside>
  <h2>{ title }</h2>
  <p>
    { paragraph }
  </p>
</aside>

const el = <Card title="Welcome!" paragraph="To this example" />
```

<!--END_DOCUSAURUS_CODE_TABS-->

In questo esempio andremo a definire che Card è un FunctionComponent a cui viene passato il Type CardProps.

I due esempi sono praticamente uguali, con la differenza che nel secondo esempio posso portare in modo opzionale anche la proprietà children in questo modo:

<!--DOCUSAURUS_CODE_TABS-->
<!--Typescript-->

```js
{ title, paragraph, children } 
```

<!--END_DOCUSAURUS_CODE_TABS-->

## Children

Come accedere ai componenti children con i FunctionComponent

<!--DOCUSAURUS_CODE_TABS-->
<!--Typescript-->

```js
import React, { FunctionComponent } from 'react';

type CardProps = {
  title: string,
  paragraph: string
}

// we can use children even though we haven't defined them in our CardProps
export const Card: FunctionComponent<CardProps> = ({ title, paragraph, children }) => <aside>
  <h2>{ title }</h2>
  <p>
    { paragraph }
  </p>
  { children }
</aside>
```

<!--END_DOCUSAURUS_CODE_TABS-->

Come detto in precedenza, in questo esempio stiamo utilizzando il destructuring, senza il destructuring dovremmo passare l'oggetto Props in questo modo:

<!--DOCUSAURUS_CODE_TABS-->
<!--Typescript-->

```js
import React, { FunctionComponent } from 'react';

// no children defined here
type CardProps = {
  title: string,
  paragraph: string
}

// undestructured
export const Card: FunctionComponent<CardProps> = (props) => <aside>
  <h2>{ props.title }</h2>
  <p>
    { props.paragraph }
  </p>
  { /* still in our props */ }
  { props.children }
</aside>
```

<!--END_DOCUSAURUS_CODE_TABS-->

## Eventi

Utilizzando Typescript in ReacJS bisogna tipizzare correttamente anche gli eventi. Di seguito un evento base per definire un onClick

<!--DOCUSAURUS_CODE_TABS-->
<!--Typescript-->

```js
import React, { Component, MouseEvent } from 'react';

export class Button extends Component {
  handleClick(event: MouseEvent) {
    event.preventDefault();
    alert(event.currentTarget.tagName); // alerts BUTTON
  }
  
  render() {
    return <button onClick={this.handleClick}>
      {this.props.children}
    </button>
  }
}
```

<!--END_DOCUSAURUS_CODE_TABS-->

Altri eventi disponibili: AnimationEvent, ChangeEvent, ClipboardEvent, CompositionEvent, DragEvent, FocusEvent, FormEvent, KeyboardEvent, MouseEvent, PointerEvent, TouchEvent, TransitionEvent, WheelEvent.

Oltre a MouseEvent, è possibile anche andare a specificare il tipo di elemento quindi è possibile limitare ulteriormente la tipizzazione. Vediamo qualche esempio

<!--DOCUSAURUS_CODE_TABS-->
<!--Typescript-->

```js
import React, { Component, MouseEvent } from 'react';

export class Button extends Component {
  /*
   Here we restrict all handleClicks to be exclusively on 
   HTMLButton Elements
  */
  handleClick(event: MouseEvent<HTMLButtonElement>) {
    event.preventDefault();
    alert(event.currentTarget.tagName); // alerts BUTTON
  }

  /* 
    Generics support union types. This event handler works on
    HTMLButtonElement and HTMLAnchorElement (links).
  */
  handleAnotherClick(event: MouseEvent<HTMLButtonElement | HTMLAnchorElement>) {
    event.preventDefault();
    alert('Yeah!');
  }

  render() {
    return <button onClick={this.handleClick}>
      {this.props.children}
    </button>
  }
}
```

<!--END_DOCUSAURUS_CODE_TABS-->

Per quanto riguarda onInput, per il momento bisogna utilizzare SyntheticEvent.

## Hooks

### useState

In questo esempio, useState prende come valore iniziale initial, in questo modo setClicks potrà accettare solo number.

<!--DOCUSAURUS_CODE_TABS-->
<!--Typescript-->

```js
// import useState next to FunctionComponent
import React, { FunctionComponent, useState } from 'react';

// our components props accept a number for the initial value
const Counter:FunctionComponent<{ initial?: number }> = ({ initial = 0 }) => {
  // since we pass a number here, clicks is going to be a number.
  // setClicks is a function that accepts either a number or a function returning
  // a number
  const [clicks, setClicks] = useState(initial);
  return <>
    <p>Clicks: {clicks}</p>
    <button onClick={() => setClicks(clicks+1)}>+</button>
    <button onClick={() => setClicks(clicks-1)}>-</button>
  </>
}
```

<!--END_DOCUSAURUS_CODE_TABS-->

### useRef

In questo esempio stiamo definendo che inputEl sarà un HTMLInputElement inizializzato a null.

<!--DOCUSAURUS_CODE_TABS-->
<!--Typescript-->

```js
function TextInputWithFocusButton() {
  // initialise with null, but tell TypeScript we are looking for an HTMLInputElement
  const inputEl = useRef<HTMLInputElement>(null);
  const onButtonClick = () => {
    // strict null checks need us to check if inputEl and current exist.
    // but once current exists, it is of type HTMLInputElement, thus it
    // has the method focus! ✅
    if(inputEl && inputEl.current) {
      inputEl.current.focus();
    } 
  };
  return (
    <>
      { /* in addition, inputEl only can be used with input elements. Yay! */ }
      <input ref={inputEl} type="text" />
      <button onClick={onButtonClick}>Focus the input</button>
    </>
  );
}
```

<!--END_DOCUSAURUS_CODE_TABS-->

### useReducer

Nel seguente esempio stiamo creando un Type chiamato ActionType che può accettare una stringa con uno di quei 3 valori.

<!--DOCUSAURUS_CODE_TABS-->
<!--Typescript-->

```js
type ActionType = {
  type: 'reset' | 'decrement' | 'increment'
}

const initialState = { count: 0 };

// We only need to set the type here ...
function reducer(state, action: ActionType) {
  switch (action.type) {
    // ... to make sure that we don't have any other strings here ...
    case 'reset':
      return initialState;
    case 'increment':
      return { count: state.count + 1 };
    case 'decrement':
      return { count: state.count - 1 };
    default:
      return state;
  }
}

function Counter({ initialCount = 0 }) {
  const [state, dispatch] = useReducer(reducer, { count: initialCount });
  return (
    <>
      Count: {state.count}
      { /* and can dispatch certain events here */ }
      <button onClick={() => dispatch({ type: 'reset' })}>
        Reset
      </button>
      <button onClick={() => dispatch({ type: 'increment' })}>+</button>
      <button onClick={() => dispatch({ type: 'decrement' })}>-</button>
    </>
  );
}
```

<!--END_DOCUSAURUS_CODE_TABS-->

## Context

Per utilizzare i Context, la prima cosa da fare è andare a Creare un nuovo Context.
In questo caso abbiamo definito 3 proprietà, la prima boolean e le altre 2 di <a href="https://danielecarta-docs.netlify.app/docs/typescript-tipi#string">tipo string</a>.

<!--DOCUSAURUS_CODE_TABS-->
<!--Typescript-->

```js
import React from 'react';

export const AppContext = React.createContext({ 
  authenticated: true,
  lang: 'en',
  theme: 'dark'
});
```

<!--END_DOCUSAURUS_CODE_TABS-->

Fai molta attenzione a una cosa, quando vai a utilizzare il Context, dovrai per forza utilizzare tutte le proprietà, in quanto riceverai un'errore di compilazione facendo questo:

<!--DOCUSAURUS_CODE_TABS-->
<!--Typescript-->

```js
const App = () => {
  // ⚡️ compile error! Missing properties
  return <AppContext.Provider value={ {
    lang: 'de', 
  } }>
    <Header/>
  </AppContext.Provider>
}
```

<!--END_DOCUSAURUS_CODE_TABS-->

Non preoccuparti, c'è anche il modo di andare a utilizzare solo le proprietà di cui hai bisogno utilizzando l'helper <a href="https://danielecarta-docs.netlify.app/docs/typescript-type#partial">Partial</a>:

<!--DOCUSAURUS_CODE_TABS-->
<!--Typescript-->

```js

import React from 'react';

// We define our type for the context properties right here
type ContextProps = { 
  authenticated: boolean,
  lang: string,
  theme: string
};

// we initialise them without default values, to make that happen, we
// apply the Partial helper type.
export const AppContext = 
  React.createContext<Partial<ContextProps>>({});

const Header = () => {
  return <AppContext.Consumer>
  {
    ({authenticated}) => {
      if(authenticated) {
        return <h1>Logged in!</h1>
      }
      return <h1>You need to sign in</h1>
    }
  }
  </AppContext.Consumer>
}

// Now, we can set only the properties we really need
const App = () => {
  return <AppContext.Provider value={ {
    authenticated: true,
  } }>
    <Header/>
  </AppContext.Provider>
}
```

<!--END_DOCUSAURUS_CODE_TABS-->
