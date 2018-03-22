## Composing Hierarchical Components

Just like every other scenario in which you used components, Stencil components can be composed with each other. This is the beauty of web components. A component can have multiple children and grandchildren, as well as siblings. This enables you to write small, self-contained components that can work with other smaller components and carry out a single task.

As an example, let's create another component called **TodoList** and compose with the **Site** component. The former will be a child component to the latter.

```
// components/todo-list/todo-list.tsx
import { Component } from '@stencil/core';

@Component({
  tag: 'todo-list',
  styleUrl: 'todo-list.scss'
})
export class TodoList {

  render() {
    return (
      <div class="todo-list">
        <ul>
          <li>Write some code</li>
        </ul>
      </div>
    );
  }
}
```

Same syntax with the **Site** component, with different names and visuals. Let's now add the component to the parent **Site** component:

```
export class Site {
  render() {
    return (
      <div class="wrapper">
        <nav>
          ...
        </nav>
        <div class="container">
          <div class="row">
            <div class="col-md-offset-4 col-md-4 col-sm 12">
              {/* Child component, TodoList */}
              <todo-list></todo-list>

            </div>
          </div>
        </div>
      </div>
    );
  }
}
```

We don't have to import the component child class to the parent class. We only need to include the **todo-list** tag and then Stencil looks up the component in the **components** folder and loads it accordingly.

