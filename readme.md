# useEffect

## What is useEffect?

`useEffect` is a hook that allows you to perform side effects in function components. It is a close replacement for `componentDidMount`, `componentDidUpdate`, and `componentWillUnmount` in class components.

## How to use useEffect?

`useEffect` takes a function as its first argument. This function is called after every render. The function can optionally return a cleanup function, which is called before the component is removed from the DOM.

```js
import React, { useEffect } from 'react';

const MyComponent = () => {
  useEffect(() => {
    // This gets called after every render, by default
    // (the first one, and every one after that)
  });

  return <div>Hello, world!</div>;
};
```

## How does useEffect know when to run?

`useEffect` will run after every render by default. If you want to restrict it to only run on mount and unmount, you can pass an empty array as the second argument.

```js
import React, { useEffect } from 'react';

const MyComponent = () => {
  useEffect(() => {
    // This gets called after the first render
  }, []);

  return <div>Hello, world!</div>;
};
```

## How does useEffect know when to re-run?

`useEffect` will re-run if any of the values in the second argument array change. This is useful if you want to perform a side effect when a specific prop changes value.

```js
import React, { useEffect } from 'react';

const MyComponent = ({ name }) => {
  useEffect(() => {
    // This gets called after the first render
    // and after every render where the name prop changes
  }, [name]);

  return <div>Hello, {name}!</div>;
};
```

## How does useEffect compare to componentDidMount and componentDidUpdate?

`useEffect` is a close replacement for `componentDidMount` and `componentDidUpdate`. It is called after every render, and you can optionally return a cleanup function. The cleanup function is called before the component is removed from the DOM.

**Note:** `useEffect` will also be called after the first render, just like `componentDidMount`.

## what is the cleanup function?

The cleanup function is an optional return value from the effect function. It is called before the component is removed from the DOM. It is useful for cleaning up any state or side effects created by the effect, such as event listeners or timers, before the component is removed from the DOM.

```js
import React, { useEffect } from 'react';

const MyComponent = () => {
  useEffect(() => {
    // This gets called after every render

    return () => {
      // This gets called right before React removes the component from the DOM.
      // Cleanup any state or side effects here
    };
  }, []);

  return <div>Hello, world!</div>;
};
```

## example for the cleanup function

```js
import React, { useEffect, useState } from 'react';

const MyComponent = () => {
  const [count, setCount] = useState(0);

  useEffect(() => {
    const interval = setInterval(() => {
      setCount(count + 1);
    }, 1000);

    return () => {
      clearInterval(interval);
    };
  }, [count]);

  return <div>{count}</div>;
};
```

**what is happing here?**

1. The `useEffect` hook is called with an empty array as the second argument. This means that the effect will only run on mount and unmount.
2. The effect function creates an interval that runs every second.
3. The effect function returns a cleanup function that clears the interval.
4. The component is rendered to the DOM.
5. After one second, the `setCount` function is called, causing the component to re-render.
6. The effect function runs again, creating a new interval.
7. The cleanup function from the previous render is called, clearing the old interval.
8. After another second, the `setCount` function is called again, causing the component to re-render.
9. The effect function runs again, creating a new interval.
10. The cleanup function from the previous render is called, clearing the old interval.
11. The component is removed from the DOM.
12. The cleanup function is called, clearing the interval.

## how to fetch data with useEffect?

`useEffect` is a great place to fetch data from an API. You can use `fetch` or a library like `axios` to make the request.

```js
import React, { useEffect, useState } from 'react';

const MyComponent = () => {
  const [data, setData] = useState(null);

  useEffect(() => {
    const fetchData = async () => {
      const response = await fetch('https://example.com/data.json');
      const data = await response.json();
      setData(data);
    };

    fetchData();
  }, []);

  return <div>{JSON.stringify(data)}</div>;
};
```

**what is happing here?**

1. The `useEffect` hook is called with an empty array as the second argument. This means that the effect will only run on mount and unmount.
2. The effect function calls `fetchData`, which makes a request to an API and sets the response data in state.
3. The component is rendered to the DOM.
4. The effect function runs, making the request to the API.
5. The response data is set in state.
6. The component is re-rendered with the response data.
7. The component is removed from the DOM.

## what can I do with useEffect?

`useEffect` is a great place to perform side effects in function components. Some common use cases include:

    * Fetching data from an API
    * Setting up event listeners
    * Setting up timers
    * Logging to the console
    * Updating component state
    * Performing side effects in response to prop or state or context changes

## what i can't do with useEffect?

`useEffect` is not a good place to perform synchronous side effects. Some common use cases that are not a good fit for `useEffect` include:

    * Updating component state synchronously
    * Performing synchronous side effects in response to prop or state or context changes
    * Calling imperative APIs that have side effects like `localStorage.setItem` or `document.title = 'Hello, world!'`

## conclusion

`useEffect` is a great way to perform side effects in function components. It is a close replacement for `componentDidMount`, `componentDidUpdate`, and `componentWillUnmount`. It is called after every render, and you can optionally return a cleanup function. The cleanup function is called before the component is removed from the DOM.

---

Thanks for reading.

if you liked the tutorial please give it a star 🌟

also follow me.

**Yahya EL Ganayni**

- GitHub: [github](https://github.com/yahyaelganyni1)
- Twitter: [@YElganayni](https://twitter.com/YElganayni)
- LinkedIn: [LinkedIn](https://www.linkedin.com/in/yahya-el-ganayni-a456115b/)
