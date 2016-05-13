```markdown
Possible ideas to talk about still:

- code example for store composer
```

# Folder & File Structure

For all of these examples lets assume this is the current state tree:

```javascript
{
  projects: [],
  todos: [],
}
```
---

In many boilerplates and examples for Redux you will see the following folder layout:

<img src="images/folder-layout-bad.png" />

This is reasonable when first starting out with Redux but quickly fails as your project scales. Instead of wasting time scrolling through directories trying to find the correct file you need to modify when adding or updating a feature, it is much easier to have your directories organized and grouped by feature.

The structure of your folders should be an exact 1-1 representation of your current state tree. This makes it incredibly easy to reason about and visualize your state. It also keeps a nice clean separation of concerns between data sources (more about this later).

Our previous layout example from above modified to follow new pattern:

<img src="images/folder-layout-good.png" />

If there are any utility methods that need to be added to selectors, reducers, or actions, you now have the flexibility to put them either in a features folder (if its an isolated method) or, if the method is used in various places, in a `utils.js` file in the root of your state folder.

### Nested State Tree

For nested state trees still follow the rule of matching your folders to your state. For example, if our state changed to this:

```javascript
{
  projects: [],
  todos: {
    active: [],
    archived: [],
  },
}
```

Your folder structure would look like this:

<img src="images/folder-layout-nested.png" />

In your parent reducers you can utilize Redux's `combineReducers` method to group your child reducers together.

### Action Type Definitions

All action type definitions should live inside a `action-types.js` file in the root of your state folder. This keeps all of our actions contained and allows us to add and update new ones with relative ease.

```javascript
export const PROJECT_ADD = 'PROJECT_ADD';
export const PROJECT_REMOVE = 'PROJECT_REMOVE';

// block sections together via a new line

export const TODO_ADD = 'TODO_ADD';
export const TODO_REMOVE = 'TODO_REMOVE';
```

You can read about conventions for actions in the [Actions & Action Creators](actions-action-creators.md) chapter.

### Store Composer

The main store composer should live inside a `index.js` file in the root of your state folder. The store composer should _only_ do the following things:

- Combine all reducers
- Setup middleware
- Create store instance
- Export store instance
