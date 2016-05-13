# Usage with React

By utilizing [react-redux](https://github.com/reactjs/react-redux) we can keep a clean separation between smart and dumb components and allow our application to grow more easily.

### Avoid coupling to the state of another module

If, in our `projects` and `todos` example, `projects` needed to grab information from the `todos` state in order to render a component, you should provide an interface from the `todos` state rather than interacting with the `todos` state directly:

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

The `GOOD` example is powerful because you can freely change the structure of the `todos` and `projects` state, without worrying about updating the `ProjectTodosContainer` component. This way, if you need to refactor your state, you can simply update your selectors instead of updating numerous container components.

### Utilize smart and dumb components

All dumb components should be rendered as stateless functional components. A dumb component should always be accompanied with a smart container component e.g. `Todos` and `TodosContainer`. You should be utilizing `react-redux`s `connect` method as much as possible in your container components to eliminate unnecessary re-renders.
