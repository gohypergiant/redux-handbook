# Reducers

First off, please read up on [reducers](http://redux.js.org/docs/basics/Reducers.html). This page in the official Redux documentation is a great resource and covers a lot of conventions and best practices.

### State Shape

It is a good idea to think of the shape of your state before writing any code if possible. To make your state easy to reason about, keep it as flat as possible. Keeping it flat also has the added benefit of making state updates easier since you are not dealing with nested objects.

### Immutable Data

By using libraries like `immutable.js` we can have immutable data baked in to our reducers. This helps `react-redux` know when to re-render components, allows us to know for certain that were getting returned new instances, and many more benefits.
