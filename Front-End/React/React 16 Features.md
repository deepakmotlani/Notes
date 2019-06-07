## React 16 Features

* Now you can return list of elements or string from component's render method. 

```
render() {
  return [
    <li>One</li>
    <li>Two</li>
    <li>Three</li>
  ]
}

render() {
  return 'Hello World!';
}
```

* Better Error Handling, previously when there were some error it would React page in broken state. They came up with a solution for this, that if there is a problem in a component render or lifecycle method, whole component tree is unmounted or you can set error boundaries. Error boundaries are special components that capture error inside a subtree & display fallback UI.

* [More Features](https://reactjs.org/blog/2017/09/26/react-v16.0.html)
