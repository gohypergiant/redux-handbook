# Actions & Action Creators

## Actions

All actions should follow the [Flux Standard Action](https://github.com/acdlite/flux-standard-action) structure. In short:

> An action **MUST**

> - be a plain JavaScript object.
> - have a `type` property.

> An action **MAY**

> - have a `error` property.
> - have a `payload` property.
> - have a `meta` property.

> An action **MUST NOT** include properties other than `type`, `payload`, and `error`, and `meta`.

This makes it incredibly easy for a developer to know the exact structure of an incoming action when working inside a reducer. It also allows you to utilize destructuring inside your reducers for more terse code:

```javascript
export function todos(state = [], { type, payload }) {
  switch (type) {
    case TODO_ADD:
      return todos.push(payload);

    default: return state;
  }
}
```

## Action creators

Action creators at their basic form are just functions that return an object. Given this flexibility you are able to create them in a number of different ways. We do not have any strict conventions regarding action creators, instead we recommend that you keep them small and focused.

Be careful when adding in middleware libraries as they each add a layer of complexity and abstraction to your code. Action creators should always be small and explicit so that they are predictable and easily testable.

#### Asynchronous actions

For asynchronous actions, utilize [redux-thunk](https://github.com/gaearon/redux-thunk) or [redux-promise](https://github.com/acdlite/redux-promise). If your action requires an HTTP request, use [redux-requests](https://github.com/idolize/redux-requests) or similar so that you are not dispatching multiple HTTP calls and state updates.

#### Dispatching multiple actions

If you need to dispatch multiple actions at once please use [redux-batched-actions](https://github.com/tshelburne/redux-batched-actions)

## Action type naming convention

Since naming things is one of the harder areas in programming, here is a set of guidelines to help you name your action types:

1. Action types **MUST** be namespaced e.g. `TODO_ADD` (`TODO` being the namespace and `ADD` being the type)
2. Action namespace **MUST** come before action type.
3. Asynchronous action types **MUST** use a present tense and past tense to determine HTTP state e.g. `TODO:ADDING` and `TODO:ADDED`
4. Error actions **MUST** append `ERROR` to the action type e.g. `TODO:ADD_ERROR`

Use your best judgement when naming an action so that they are short and descriptive.

## Reducing boilerplate

A standard way of creating an action is like so:

```javascript
export function someAction() {
  return {
    type: SOME_ACTION,
    payload: {
      foo: 'bar'
    },
  };
}
```

with libraries such as [redux-actions](https://github.com/acdlite/redux-actions) this can be shortened to:

```javascript
export const someAction = createAction(SOME_ACTION, () => ({ foo: 'bar' }));
```
