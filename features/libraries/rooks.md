---
description: Collection of React hooks ⚓ for everyone.
---

# Rooks

## Introduction

The hook pattern in React is a great way to re-use common logic. Rooks offers a collection of frequently useful functions that we can pick and choose from to suit our needs.

The library is tree shakable allowing us to import each hook as necessary without an ever expanding bundle size.

## Example Usage

An example of usage taken from our MenuDraw component.

```tsx
import { useUndoState } from 'rooks';

export const MenuDraw = () => {
  // Undo state mimicsk Reacts own Usestate hook but has history
  // allowing for the state to be 'undone'
  const [activeMenu, setActiveMenu, undoActiveMenu] = useUndoState('menuRoot');
```

## Recomended Reading

Before you try to solve a 'hooks' problem take a look at the Rooks list of hooks. Battle tested and robust they are an excellent time saving resouces.

{% embed url="https://react-hooks.org/docs" %}

{% embed url="https://react-hooks.org/docs/hooks-list" %}
