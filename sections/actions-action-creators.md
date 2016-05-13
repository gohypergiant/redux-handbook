```markdown
Possible ideas to talk about still:

- thunk or promise debate for async actions
- best practices for keeping action creators small
- best practices for dispatching multiple actions at once
- library suggestions for reducing action creators boilerplate
```

# Actions & Action Creators

### Actions

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

### Action Creators

Action creators can be created in many different ways, so the way you create it is up to you.

For asynchronous actions, utilize [redux-thunk](https://github.com/gaearon/redux-thunk). If your action requires an HTTP request, use [redux-requests](https://github.com/idolize/redux-requests) so that you are not dispatching multiple HTTP calls and state updates.

No middleware outside of the two libraries above should be used unless absolutely needed. Middleware, while nice for reducing boilerplate, hides complexity and introduces a layer of _magic_ to your actions. Actions should always be explicit and clear so that they are predictable and easily testable.

### Action Type Naming Convention

Since naming things is one of the harder areas in programming, here is a set of guidelines to help you name your action types:

1. Action types **MUST** be namespaced e.g. `TODO:ADD` or `TODO_ADD` (`TODO` being the namespace and `ADD` being the type)
2. Action namespace **MUST** come before action type.
3. Asynchronous action types **MUST** use a present tense and past tense to determine HTTP state e.g. `TODO:ADDING` and `TODO:ADDED`
4. Error actions **MUST** append `ERROR` to the action type e.g. `TODO:ADD_ERROR`

Use your best judgement when naming an action so that they are short and descriptive.
