# [BPXL Redux Handbook](http://brandonjpierce.github.io/redux-handbook/)

## Introduction

The Black Pixel way to write applications with Redux.

### Redux - What is it?

[Redux](http://redux.js.org/) is a state management library written by Dan Abramov. It is often used in combination with [React](https://facebook.github.io/react/) to pull state out from the view layer into a single Store. In simple terms, any data which may change ends up living in Redux, which then gets wired up to your React containers to provide the means to **read** from or **write** to your state object.

When using Redux, your implementation typically focuses in one of three areas:

- Actions, which describe both the type and any relevant data that you use to communicate updates to the store
- Reducers, which is the code which actually performs the update to the store based on the Actions
- Containers, which is the 'glue' which binds Redux to your components using [higher order components](https://medium.com/@dan_abramov/mixins-are-dead-long-live-higher-order-components-94a0d2f9e750#.jxumv6uhb). Your containers provide the means to interact with Redux by allowing you to wire up state properties or action creators which your components receive as props.

If you are new to Redux, the [docs](http://redux.js.org/index.html) are an excellent place to start.

### Why we use it

Redux is an evolution of the [Flux](https://facebook.github.io/flux/docs/overview.html) architecture and has similar goals, namely pulling application state out of the view layer and providing the means to interact with it. There are a few key differences between the two, such as:

- Flux often advocates for multiple stores, whereas Redux has a single store and uses "reducer" functions to allow for a separation of concerns.
- Flux is an 'architecture', with several implementations; Redux is a single library
- Flux allows for either mutable or immutable data (although immutability is often encouraged); Redux mandates immutability

The combination of these points lead to several advantages with Redux.

- You don't have to worry about multiple stores and managing any dependencies between them
- Immutability being mandatory means Redux is able to implement [shouldComponentUpdate](https://facebook.github.io/react/docs/advanced-performance.html) optimization for free
- The single store and immutable data allows for easy implementation of features such as simpler state hydration, snapshots, or recording/'time travel'
- Redux's approach allows it to have a smaller, simpler API making it easier to learn and use in practice
- This also allows for easier testing and debugging
- It has become very popular leading to quick adoption and community support through additional modules/middleware

### Are there any downsides to using Redux?

There is an excellent discussion on [github](https://github.com/reactjs/redux/issues/1385) discussing this. An additional thing to consider is that your data should be represented in your state object in a normalized way. This make take some additional considerations depending on your data model/API design. Dan Abramov has provided an additional tool called [normalizr](https://github.com/paularmstrong/normalizr) which attempts to address this.
