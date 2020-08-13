---
id: typescript-reactjs
title: Typescript in ReactJS
---

## Props

Esempio molto semplice per definire le Props di un functional component con Type

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

In questa parte { title, paragraph }: CardProps viene utilizzato il destructuring per estrarre le proprietà di CardProps e accedere direttamente alle proprietà senza dover scrivere CardProps.title.

Invece in questo esempio di Type andremo a difinire delle proprietà non obbligatorie

```js
type CardProps = {
  title: string,
  paragraph?: string  // the paragraph is optional
}
```

Quindi in questo caso, utilizzato l'optional chaining andremo a difinire opzionale la proprietà paragraph.

Un altro esempio

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

In questo esempio andremo a definire che Card è un FunctionComponent a cui viene passato il Type CardProps.

I due esempi sono praticamente uguali, con la differenza che nel secondo esempio posso portare in modo opzionale anche la proprietà children in questo modo:

```js
{ title, paragraph, children } 
```

## Children

Come accedere ai componenti children con i FunctionComponent

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

Come detto in precedenza, in questo esempio stiamo utilizzando il destructuring, senza il destructuring dovremmo passare l'oggetto Props in questo modo:

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

## Eventi

Utilizzando Typescript in ReacJS bisogna tipizzare correttamente anche gli eventi. Di seguito un evento base per definire un onClick

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

Altri eventi disponibili: AnimationEvent, ChangeEvent, ClipboardEvent, CompositionEvent, DragEvent, FocusEvent, FormEvent, KeyboardEvent, MouseEvent, PointerEvent, TouchEvent, TransitionEvent, WheelEvent.

Oltre a MouseEvent, è possibile anche andare a specificare il tipo di elemento quindi è possibile limitare ulteriormente la tipizzazione. Vediamo qualche esempio

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

Per quanto riguarda onInput, per il momento bisogna utilizzare SyntheticEvent.

## Hooks

### useState

In questo esempio, useState prende come valore iniziale initial, in questo modo setClicks potrà accettare solo number.

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

### useRef

In questo esempio stiamo definendo che inputEl sarà un HTMLInputElement inizializzato a null.

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

### useReducer

Nel seguente esempio stiamo creando un Type chiamato ActionType che può accettare una stringa con uno di quei 3 valori.

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

## Context

Per utilizzare i Context, la prima cosa da fare è andare a Creare un nuovo Context.
In questo caso abbiamo definito 3 proprietà, la prima boolean e le altre 2 di <a href="https://danielecarta-docs.netlify.app/docs/typescript-tipi#string">tipo string</a>.

```js
import React from 'react';

export const AppContext = React.createContext({ 
  authenticated: true,
  lang: 'en',
  theme: 'dark'
});
```

Fai molta attenzione a una cosa, quando vai a utilizzare il Context, dovrai per forza utilizzare tutte le proprietà, in quanto riceverai un'errore di compilazione facendo questo:

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

Non preoccuparti, c'è anche il modo di andare a utilizzare solo le proprietà di cui hai bisogno utilizzando l'helper <a href="https://danielecarta-docs.netlify.app/docs/typescript-type#partial">Partial</a>:

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

## Style e CSS

Ti consiglio di guardarti questo pacchetto: <a target="_blank" href="https://www.npmjs.com/package/csstype">CSSType</a>.

### Stile in linea

Per definire lo stile in linea, vediamo subito un esempio:

```js
import CSS from 'csstype';

const h1Styles: CSS.Properties = {
  backgroundColor: 'rgba(255, 255, 255, 0.85)',
  position: 'absolute',
  right: 0,
  bottom: '2rem',
  padding: '0.5rem',
  fontFamily: 'sans-serif',
  fontSize: '1.5rem',
  boxShadow: '0 0 10px rgba(0, 0, 0, 0.3)'
};
```

Come avrai notato, abbiamo importato il pacchetto csstype.
Funzionano molto bene anche i suggerimenti.

<img style="margin: 0" src="https://danielecarta-docs.netlify.app/img/autocompletion-on-properties.png" />

Per applicare il tuo stile in linea:

```js
export function Heading({ title } : { title: string} ) {
  return <h1 style={h1Styles}>{title}</h1>;
}
```

### Styled Components

Per utilizzare Styled Components con Typescript, è necessario installare la seguente dipendenza:

```js
npm install @types/styled-components
```

Una volta installata, potremo già iniziare a utilizzarlo:

```js
import styled from "styled-components";

export const Heading = styled.h1`
  font-weight: normal;
  font-style: italic;
`;
```

Se avessimo invece necessità di passare delle props al nostro stile:

```js
type FlexProps = {
  direction?: 'row' | 'column',
}

export const Flex = styled.div<FlexProps>`
    display: flex;
    flex-direction: ${props => props.direction};
`;

// use it like that:
const el = <Flex direction="row"></Flex>
```

Se lavori con VS Code e Styled Components puoi utilizzare quest'estensione: <a target="_blank" href="https://marketplace.visualstudio.com/items?itemName=jpoissonnier.vscode-styled-components">Download</a>
