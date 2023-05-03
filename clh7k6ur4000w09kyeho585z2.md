---
title: "useTransition() Hook Explained"
seoTitle: "useTransition Hook Explained"
seoDescription: "React 18 introduced many new hooks and in this article I will be talking about useTransition hook."
datePublished: Wed May 03 2023 10:32:01 GMT+0000 (Coordinated Universal Time)
cuid: clh7k6ur4000w09kyeho585z2
slug: usetransition-hook-explained
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1683109686118/f3090a55-07d5-4403-b5ff-928df93f8ec3.jpeg
tags: javascript, reactjs, typescript, frontend-development, reacthooks

---

With the new launch of React 18, React introduced new hooks along with its unique features. Among them, the `useTransition()` hook is pretty interesting. This hook increases the performance and smoothness of your application and makes it better.

## Why `useTransition()` ?

Suppose we are implementing a typeahead input field, Where two things are happening, Whatever the user enters, gets shown in the UI. Then a

```javascript
import { useEffect, useState } from "react";
import "./App.css";
import List from "./List";
import { MOCKDATA } from "./mockData";

function App() {
  const [keyword, setKeyword] = useState("");
  const [users, setUsers] = useState([]);
  const [result, setResult] = useState([]);

  useEffect(() => {
    setUsers(MOCKDATA);
  }, []);

  const handleChange = async (e) => {
    setKeyword(e.target.value);
    setResult(
      users.length &&
        users.filter((item) => item.name.includes(e.target.value))
    );
  };

  return (
    <>
      <h1>Search Products</h1>
      <div className="card">
        <input value={keyword} onChange={handleChange} />
        <p>Searching for: {keyword}</p>
        {result.length &&
          keyword &&
          result.map((item) => <List key={item?.id} item={item} />)}
      </div>
      <p className="read-the-docs">
        Click on the Vite and React logos to learn more
      </p>
    </>
  );
}

export default App;
```

If the data is too large, this will block the rendering until the filter method is completed. Because on the handleChange event display keyword and filter both happening using useState. Now React is smart enough to understand the state updates are happening together, so it will batch and perform them at the same time, resulting in rendering the component at the end of the total calculations.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683105253939/505c71b0-c07d-4dd4-b0cf-38f2c75d0a3a.gif align="center")

As you can see how much the user types, the onChangeHandler shows the keyword at the end of filtering the list resulting in a cluttered UI experience. That's where the `useTransition` hook comes into play.

## Implement `useTransition`

Depending on the use cases, we have to figure out how to implement `useTransition`. In the above example, we can understand that the keyword display is more important rather than the filter user list. Transitions will be used to figure out which states don't need immediate resources. These states will implement in parallel, but will not block the rendering of the more important state updates.

### Syntax:

`useTransition` hook returns an array with the first value as `isPending` and second as `startTransition` function.

```javascript
const [isPending, startTransition] = useTransition()
```

The `isPending` variable is a boolean type that returns true when the `startTransition` is running. In short, when the state update is occurring this will return true and false if the state update is done.

### In our case, we can wrap the `setResult` inside `startTransition`.

```javascript
startTransition(() => {
      setResult(
        users.length &&
          users.filter((item) => item.name.includes(e.target.value))
      );
    });
```

### Now, render the `List` component conditionally

```javascript
{isPending ? (
          <h1>Loading...</h1>
    ) : (
          result.length &&
          keyword &&
          result.map((item) => <List key={item?.id} item={item} />
        )
)}
```

This will look like this:

```javascript
import { useEffect, useState, useTransition } from "react";
import "./App.css";
import List from "./List";
import { MOCKDATA } from "./mockData";

function App() {
  const [isPending, startTransition] = useTransition();
  const [keyword, setKeyword] = useState("");
  const [users, setUsers] = useState([]);
  const [result, setResult] = useState([]);

  useEffect(() => {
    setUsers(MOCKDATA);
  }, []);

  const handleChange = async (e) => {
    setKeyword(e.target.value);
    startTransition(() => {
      setResult(
        users.length &&
          users.filter((item) => item.name.includes(e.target.value))
      );
    });
  };

  return (
    <>
      <h1>Search Products</h1>
      <div className="card">
        <input value={keyword} onChange={handleChange} />
        <h2>Searching for: {keyword}</h2>
        {isPending ? (
          <h1>Loading...</h1>
        ) : (
          result.length &&
          keyword &&
          result.map((item) => <List key={item?.id} item={item} />)
        )}
      </div>
    </>
  );
}

export default App;
```

Now, if we run the code, we can see that the generated input is getting updated immediately when we type. Resulting in a smoother UI. While the text is updating `Loading...` is getting displayed. Once the state gets finished updating, we can see the final list.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683104750017/458f6c43-f30f-4c14-a11b-32c4cb45bcc1.gif align="center")

## useTransition() vs setTimeout()

* setTimeout has a delay where usetransition's delay depends upon the device.
    
* useTransition() won't freeze the page like setTimeout().
    
* useTransition() executes immediately rather than setTimeout().
    

## Conclusion

Using this hook is simple, and easy. One should only use this hook when there is a computationally intense task in your component that affects the performance. Such that it can inform React to prioritize its tasks.

## Github link:

[https://github.com/Sankalan47/useTransition-Tutorial](https://github.com/Sankalan47/useTransition-Tutorial)

## References:

[https://react.dev/reference/react/useTransition](https://react.dev/reference/react/useTransition)