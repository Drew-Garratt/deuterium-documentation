---
description: React useContextSelector hook in userland
---

# Use Context Selector

## Introduction

Reacts principle method for managing state without the need for [prop drilling](https://kentcdodds.com/blog/prop-drilling) is the [context API](https://kentcdodds.com/blog/how-to-use-react-context-effectively). However, the API is not without its shortcomings. Chiefly that all components connected to a context by the `useContext` hook will be re-rendered if **any** portion of the context state changes, not just the value that individual `useContext` hook uses.

To solve this problem a new `useContextSelector` hook has been proposed. However, due to other priorities, it has yet to make it to general release. This library acts as a polyfill.

## Example Usage

In order to make use of the new hook contexts must be created via the `createContext` function exported from this library.

```tsx
import { createContext } from 'use-context-selector';

const PersonContext = createContext({ firstName: '', familyName: '' })
```

Once this has been done individual components can make use of the new `useContextSelector` hook.&#x20;

As can be seen from the example below (taken from the docs) the new hook returns a selector function for each value. This new value will only be updated, triggering re-render, if the selector's output value changes.

```tsx
import { useState } from 'react';

import { createContext, useContextSelector } from 'use-context-selector';

const context = createContext(null);

const Counter1 = () => {
  const count1 = useContextSelector(context, v => v[0].count1);
  const setState = useContextSelector(context, v => v[1]);
  const increment = () => setState(s => ({
    ...s,
    count1: s.count1 + 1,
  }));
  return (
    <div>
      <span>Count1: {count1}</span>
      <button type="button" onClick={increment}>+1</button>
      {Math.random()}
    </div>
  );
};

const Counter2 = () => {
  const count2 = useContextSelector(context, v => v[0].count2);
  const setState = useContextSelector(context, v => v[1]);
  const increment = () => setState(s => ({
    ...s,
    count2: s.count2 + 1,
  }));
  return (
    <div>
      <span>Count2: {count2}</span>
      <button type="button" onClick={increment}>+1</button>
      {Math.random()}
    </div>
  );
};

const StateProvider = ({ children }) => (
  <context.Provider value={useState({ count1: 0, count2: 0 })}>
    {children}
  </context.Provider>
);

const App = () => (
  <StateProvider>
    <Counter1 />
    <Counter2 />
  </StateProvider>
);
```

## Recomended Reading

{% embed url="https://github.com/dai-shi/use-context-selector" %}
