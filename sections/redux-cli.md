# Redux CLI

[redux-cli](https://github.com/blackpixel/redux-cli/) is a tool that was created to follow all of the best practices mentioned in this handbook. It has built in commands for creating entire state folders, individual state folder items, and smart container components that use selectors. Refer to the documentation for more information.

## Creating State Folders

Using the `redux-cli make <name>` command you can create entire state tree folders in no time at all. For example, assume our state tree is as follows:

```javascript
{
  todos: {
    active: [],
    complete: [],
    archived: [],
  }
}
```

To create this state tree you would simply `cd` into your state directory and run the following command:

```
redux-cli make todos --reducers=active,complete,archived
```

This will create a folder named `todos` with the following files inside of it:

- `reducer.js`
- `actions.js`
- `selectors.js`

If you notice we passed an additional `--reducers` flag, this populates our `reducer.js` with the passed in reducer values. In the example command above our `reducer.js` file would look like the following:

```javascript
import { combineReducers } from 'redux';
import { handleActions } from 'redux-actions';

import {
  TODO_TEST_ACTION,
} from 'path/to/action-types';

const active = handleActions({
  [TODO_TEST_ACTION]: (state, { payload }) => payload,
});

const completed = handleActions({
  [TODO_TEST_ACTION]: (state, { payload }) => payload,
});

const archived = handleActions({
  [TODO_TEST_ACTION]: (state, { payload }) => payload,
});

export default combineReducers({
  active,
  completed,
  archived,
});
```

Notice that action types are automatically added with a namespace via the `<name>` value (in this case "TODO").

This tool is absolutely invaluable for saving a precious time when developing an application with `redux`. It also makes it incredibly easy to follow all of the rules outlined in this handbook. If you have recommendations or ideas please feel free to [contribute](https://github.com/blackpixel/redux-cli/blob/master/contributing.md) to the project!

## Creating Individual State Files

`redux-cli` also gives you the ability to create individual state files:

- `redux-cli make:reducer`
- `redux-cli make:action`
- `redux-cli make:selector`
- `redux-cli make:container`

This is useful if you already have an existing state structure in place and want to slowly implement a new one. Please refer to the readme of [redux-cli](https://github.com/blackpixel/redux-cli/) for more usage examples.
