# [BPXL Redux Handbook](http://brandonjpierce.github.io/redux-handbook/)

The Black Pixel way to write applications with Redux.

---

> Everything below is dump of ideas, this will need to be formalized into paragraphs eventually.

### Why we use Redux

- single source of truth
- easy hydration, snapshots, time travel
- can be used standalone or with libraries like react
- easy testing and debugging
- learning curve is very shallow
- rich ecosystem

### What problems does redux solve

- easy to reason about application state
- predictable state changes
- async state changes

### How do I get started?

- Read the docs
- Link to egghead.io tutorial course by Dan Abramov
- Link to Wes Bos tutorial?
- Awesome redux repo

### Should I use Redux to keep track of all application state?

Short answer is no. Redux works best for things such as fetched data and locally modified models. Things such as animation state, inputs, and other frequently updated state items would be better handled in another state abstraction.
