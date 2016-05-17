```markdown
Possible ideas to talk about still:

- structure of reducer e.g. switch statements vs other methods
- our preferred immutable library
- best practices for keeping state tree size manageable
- cons of nested state
- library suggestions for reducing reducer boilerplate
```

# Reducers & Immutable Data

Reducers are designed to be pure functions, meaning they produce no side effects. They also do not store or mutate state. They are simply passed state and return state. This is the fundamental reason as to why they are so powerful and predictable.

Be sure to read about [reducers](http://redux.js.org/docs/basics/Reducers.html) from the official Redux docs. This page is a great resource and covers a lot of conventions and best practices.

### State Shape

It is a good idea to think of the shape of your state before writing any code if possible. To make your state easy to reason about, keep it as flat as possible. Keeping it flat also has the added benefit of making state updates easier since you are not dealing with nested objects and complex data structures.

### Immutable Data

By using libraries like [Immutable.js](https://facebook.github.io/immutable-js/) we can have immutable data baked into our state. Using immutable libraries is helpful for keeping your reducer updates clean and simple to read.

Using immutable data also helps `react-redux` know when to re-render components more efficiently, which has a direct effect on your applications performance.
