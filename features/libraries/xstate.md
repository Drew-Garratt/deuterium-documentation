---
description: >-
  XState is a library for creating, interpreting, and executing finite state
  machines and statecharts
---

# XState

## Introduction

XState provides us with a predictable, visual and extensible way to build complex logic into the state of our application. It does this by utilising three fundamental computing concepts; finite state machines, statecharts and the actor model.

### Finite state machines

A finite state machine is a mathematical model of computation that describes the behaviour of a system that can be in only one state at any given time. For example, let's say you can be represented by a state machine with a finite number (2) of states: `asleep` or `awake`. At any given time, you're either `asleep` or `awake`. It is impossible for you to be both `asleep` and `awake` at the same time, and it is impossible for you to be neither `asleep` nor `awake`.

<details>

<summary>More resources:</summary>

* [Finite-state machine (opens new window)](https://en.wikipedia.org/wiki/Finite-state\_machine)article on Wikipedia
* [Understanding State Machines (opens new window)](https://www.freecodecamp.org/news/state-machines-basics-of-computer-science-d42855debc66/)by Mark Shead
* [▶️ A-Level Comp Sci: Finite State Machine(opens new window)](https://www.youtube.com/watch?v=4rNYAvsSkwk)

</details>

### Statecharts

Statecharts are a formalism for modeling stateful, reactive systems. Computer scientist David Harel presented this formalism as an extension to state machines in his 1987 paper [Statecharts: A Visual Formalism for Complex Systems (opens new window)](https://www.sciencedirect.com/science/article/pii/0167642387900359/pdf).&#x20;

<details>

<summary>More resources:</summary>

* [Statecharts: A Visual Formalism for Complex Systems (opens new window)](https://www.sciencedirect.com/science/article/pii/0167642387900359/pdf)by David Harel
* [The World of Statecharts (opens new window)](https://statecharts.github.io)by Erik Mogensen

</details>

### Actor Model

The actor model is another very old mathematical model of computation that goes well with state machines. It states that everything is an "actor" that can do three things:

* **Receive** messages
* **Send** messages to other actors
* Do something with the messages it received (its **behavior**), such as:
  * change its local state
  * send messages to other actors
  * _spawn_ new actors

An actor's behavior can be described by a state machine (or a statechart).

<details>

<summary>More resources:</summary>

* [Actor model (opens new window)](https://en.wikipedia.org/wiki/Actor\_model)article on Wikipedia
* [The actor model in 10 minutes (opens new window)](https://www.brianstorti.com/the-actor-model/)by Brian Storti

</details>

## Usage in storefront-app

To help developers take advantage of XState's features while not necessarily having to learn XState's intricacy. This is achieved by seperating interaction with XStates state and actions with React's Context API.\
\
For example.

```tsx
// Selector constants allow us to target values from our StoreState XState
const selectCartId = (state: StoreState) => state.context.cartId;
const selectCart = (state: StoreState) => state.context.cart;

export const CartProvider = ({ children }: { children: ReactNode }) => {
  // The entire XState Service can be accesed via useContext
  const { storeService } = useContext(StoreContext);

  // Individual state values can then be exposed by selectors
  // Here we access the current cart ID and Cart objects
  const cartId = useSelector(storeService, selectCartId);
  const cart = useSelector(storeService, selectCart);

  // To send messages back to the machine we can call .send against the service
  // These messages are fully typed allowing for hinting and completion
  // In this example we create a function for submitting a new cart line item
  const cartLineAdd = ({ id, quantity }: { id: string; quantity: number }) => {
    storeService.send('CART_LINE_ADD', { id, quantity });
  })

  // We can return these values and functions to our context.
  // Developers working with these contexts will only ever have to interact
  // with these values and functions.
  return (
    <CartContext.Provider
      value={{
        cart,
        cartId,
        cartLineAdd,
      }}
    >
      {children}
    </CartContext.Provider>
  );

```

Standard contexts included in the Storefront-app utilise this model to help developers work with state in a manageable.

## The storeMachine

In order to manage the connected states of customer and cart the Storefront-app utilises a top level XState machine called, storeMachine.

### Splitting logic from execution

XState's machine is responsible for defining the logic of our application. What state is the application in? From that state what actions can be taken? This is the nature of finite state machines. That definition does not include the execution of those choices.

For instance, while our cart is in the 'idle' state it accepts a message of `CART_LINE_ADD`. The target of that message is the `cartLineAdd` state this state invokes a [service](https://xstate.js.org/docs/guides/communication.html#invoking-callbacks), performing a callback as soon as the state is entered. What that callback function looks like, is not defined in the machine but instead passed to the machine on invocation. This allows us to swap out services and actions or expand them as needed without altering the underlining logic of the application.

### Defining the machine

The machine itself is defined in `apps/storefront-app/src/components/storeContext/storeMachine.ts`\
\
It is defined using XStates [`createModel` function](https://xstate.js.org/docs/guides/models.html#createmodel). This allows us to create a type-safe model of our state and events.&#x20;

### Interpreting the machine

The machine and model are then interpreted and loaded into React context by `apps/storefront-app/src/components/storeContext/storeMachine.ts`. This file utilises XState React hook [`useInterpret`](https://xstate.js.org/docs/packages/xstate-react/#api). This hook provides a service which can be consued by components to expose state values via selectors using the [`useSelector`](https://xstate.js.org/docs/packages/xstate-react/#api) hook.

In our `storeMachine` the `useInterpret` hook is passed 2 arguments. The first is the machine the second is the options for the machine, which included definitions for its [services](https://xstate.js.org/docs/guides/communication.html#the-invoke-property) and [actions](https://xstate.js.org/docs/guides/actions.html).

```tsx
// Actions are imported from the /actions folder and split by customer/cart
import {
  assignCustomer,
  assignCustomerBlank,
  assignCustomerError,
  assignCustomerRestored,
  assignCustomerToken,
  setCustomerId,
  setCustomerClear,
  setCustomerToken,
} from '@/components/storeContext/actions/customerActions';

// The same is true for services
import {
  cartById,
  cartCreate,
  cartIdentityUpdate,
  cartInit,
  cartLineAdd,
} from '@/components/storeContext/services/cartServices';

const storeService: StoreServiceType = useInterpret(storeMachine, {
    devTools: process.env.NODE_ENV === 'development',
    
    //Services are imported into the service object
    services: {
      cartInit,
      cartCreate,
      cartLineAdd,
      cartById,
      cartIdentityUpdate,
      customerCreate,
      customerInit,
      customerSignIn,
      customerTokenRenew,
      customerFetch,
    },
    //Actions into the actions object
    actions: {
      assignCustomerBlank,
      assignCart,
      assignCartId,
      assignCustomer,
      assignCustomerError,
      assignCustomerToken,
      assignCustomerRestored,t
```

## Recomended Reading

{% embed url="https://xstate.js.org/docs/guides/start.html#our-first-machine" %}

{% embed url="https://xstate.js.org/docs/tutorials/reddit.html#modeling-the-app" %}

{% embed url="https://xstate-catalogue.com" %}
Great resourse for XState examples
{% endembed %}
