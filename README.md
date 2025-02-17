# zustand-slices

[![CI](https://img.shields.io/github/actions/workflow/status/zustandjs/zustand-slices/ci.yml?branch=main)](https://github.com/zustandjs/zustand-slices/actions?query=workflow%3ACI)
[![npm](https://img.shields.io/npm/v/zustand-slices)](https://www.npmjs.com/package/zustand-slices)
[![size](https://img.shields.io/bundlephobia/minzip/zustand-slices)](https://bundlephobia.com/result?p=zustand-slices)
[![discord](https://img.shields.io/discord/627656437971288081)](https://discord.gg/MrQdmzd)

A slice utility for Zustand

## Install

```bash
npm install zustand zustand-slices
```

## Usage

```jsx
import { create } from 'zustand';
import { createSlice, withSlices } from 'zustand-slices';

const countSlice = createSlice({
  name: 'count',
  value: 0,
  actions: {
    inc: () => (prev) => prev + 1,
    addBy: (n: number) => (prev) => prev + n,
  },
});

const textSlice = createSlice({
  name: 'text',
  value: 'Hello',
  actions: {
    updateText: (newText: string) => () => newText,
  },
});

const useCountStore = create(withSlices(countSlice, textSlice));

const Counter = () => {
  const count = useCountStore((state) => state.count);
  const inc = useCountStore((state) => state.inc);
  const addBy = useCountStore((state) => state.addBy);
  const text = useCountStore((state) => state.text);
  const updateText = useCountStore((state) => state.updateText);
  return (
    <>
      <div>Count: {count}</div>
      <button type="button" onClick={inc}>
        +1
      </button>
      <button type="button" onClick={() => addBy(10)}>
        +10
      </button>
      <input value={text} onChange={(e) => updateText(e.target.value)} />
    </>
  );
};
```

## Examples

The [examples](examples) folder contains working examples.
You can run one of them with

```bash
PORT=8080 yarn run examples:01_counter
```

and open <http://localhost:8080> in your web browser.

You can also try them in codesandbox.io:
[01](https://codesandbox.io/s/github/zustandjs/zustand-slices/tree/main/examples/01_counter)

## Tweets

