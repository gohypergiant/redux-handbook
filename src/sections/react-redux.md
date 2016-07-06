# Usage With React

By utilizing [react-redux](https://github.com/reactjs/react-redux), we keep a clean separation between container and presentational components and allow our application to grow more naturally. Container components allow you to control all implementation logic and data fetching for a presentational component. A presentational component should only blindly call a function or spit out data, it should not be concerned with anything else. Container components also give you free built in `shouldComponentUpdate` checks so your application will render quickly and not waste unneeded rerenders.

All presentational components should be rendered as stateless functional components. A presentational component should always be accompanied with a container component (e.g., `Todos` and `TodosContainer`). You should be utilizing `react-redux`'s `connect` method as much as possible in your container components to eliminate unnecessary rerenders.

For more information and insight into container and presentational components we recommend giving https://medium.com/@dan_abramov/smart-and-dumb-components-7ca2f9a7c7d0 and http://redux.js.org/docs/basics/UsageWithReact.html a read as they provide excellent descriptions and examples.

## Avoid Coupling to the State of Another Module

If, in our `projects` and `todos` examples, `projects` needed to grab information from the `todos` state in order to render a component, you should provide an interface from the `todos` state rather than interact with the `todos` state directly:

**BAD**
```javascript
const ProjectTodos = ({ todos }) => (
  <div>
    {todos.map(t => <TodoItem todo={t}/>)}
  </div>
);

const ProjectTodosContainer = connect(
  (state, { projectId }) => {
    const project = state.projects[projectId];

    // This couples to the todos state
    const todos = state.todos.filter(
      t => project.todos.includes(t.id)
    );

    return { todos };
  }
)(ProjectTodos);
```

**GOOD**
```javascript
import { createSelector } from 'reselect';
import { activeProject } from 'state/projects/selectors';
import { allTodos } from 'state/todos/selectors';

const ProjectTodos = ({ todos }) => (
  <div>
    {todos.map(t => <TodoItem todo={t}/>)}
  </div>
);

const ProjectTodosContainer = connect(
  createSelector(
    activeProject,
    // here we let the todos selector provide the implementation for us
    allTodos,
    (project, todos) => ({
      todos: todos.filter(t => project.todos.includes(t.id))
    })
  )
)(ProjectTodos);
```

The `GOOD` example is powerful, because you can freely change the structure of the `todos` and `projects` states without worrying about updating the `ProjectTodosContainer` component. This way, if you need to refactor your state, you can simply update your selectors instead of updating numerous container components. 
