---
description: >-
  This component is a light wrapper around focus-trap, tailored to your
  React-specific needs.
---

# Focus Trap React

## Introduction

It is often necessary as we build out more complex UI to trap focus inside a set of elements for the purposes of interaction, for example a modal component.&#x20;

Doing this inside React can be tricky mananaging this in a way that is reactive.

This libary is also an internal dependacy of [reach-ui.md](reach-ui.md "mention")

## Usage

[Check out the demo](http://focus-trap.github.io/focus-trap-react/demo/).

> Please read [the focus-trap documentation](https://github.com/focus-trap/focus-trap) to understand what a focus trap is, what happens when a focus trap is activated, and what happens when one is deactivated.
>
> This module simply provides a React component that creates and manages a focus trap.
>
> * The focus trap automatically activates when mounted (by default, though this can be changed).
> * The focus trap automatically deactivates when unmounted.
> * The focus trap can be activated and deactivated, paused and unpaused via props.

You wrap any element that you want to act as a focus trap with the `<FocusTrap>` component. `<FocusTrap>` expects exactly one child element which can be any HTML element or other React component that contains focusable elements. **It cannot be a Fragment** because `<FocusTrap>` needs to be able to get a reference to the underlying HTML element, and Fragments do not have any representation in the DOM.

For example:

```tsx
const FocusTrap = require('focus-trap-react');

<FocusTrap>
  <div id="modal-dialog" className="modal" >
    <button>Ok</button>
    <button>Cancel</button>
  </div>
</FocusTrap>
```

## Required Reading

{% embed url="https://github.com/focus-trap/focus-trap" %}
