## States and Props

So far, we have just been dealing with static contents and markup. Most components you will write in Stencil will be useless if they do not handle dynamic contents and markup. States and Props decorators are used to bring life to Stencil components.

## States

A state is a mutable chunk of data defined in a component. After initialization, it can be overwritten, deleted and updated to fit the needs of a component. A state is basically a class property decorated with the **State** decorator:

```
import { Component, State } from '@stencil/core';

@Component({
  tag: 'todo-site',
  styleUrl: 'site.scss'
})
export class Site {

  // todos as a state
  @State() todos: Todo[] = [
    {task: 'Cook', completed: false},
    {task: 'Dance', completed: true},
    {task: 'Eat', completed: false}
  ];

  render() {
    return (
      <div class="wrapper">
        ...
        <div class="container">
          <div class="row">
            <div class="col-md-offset-4 col-md-4 col-sm 12">
              <todo-list todos={this.todos}></todo-list>
            </div>
          </div>
        </div>
      </div>
    );
  }
}

interface Todo {
  task: string;
  completed: boolean;
}
```

The **todos** property is defined as a state and initialized with an array with three Todo objects. The object is typed as a **Todo** interface and has task (string) and completed (boolean) properties.

A state, unlike props, can be updated at runtime, which makes them mutable. In our case, for example, we can add or remove tasks.

The **todos** state is used in the component by passing it down to the **todo-list** component using props.

## Props

Take another look on how we passed the array of todos to the **todo-list** component:

```
<todo-list todos={this.todos}></todo-list>
```

The **todos** property, which is passed the array of todo items is what is referred to as **props**.

Before the **todo-list** component can receive values via **todos** props, it needs to be aware of the incoming values. In that case, we need to create a **todos** property on the component class and decorate the class using **Props**:

```
import { Component, Prop } from '@stencil/core';

@Component({
  tag: 'todo-list',
  styleUrl: 'todo-list.scss'
})
export class TodoList {

  @Prop() todos: Todo[];

  completedClass(todo: Todo) : string {
    return todo.completed ? 'completed' : '';
  }

  render() {
    return (
      <div class="todo-list">
        <ul>
          {this.todos.map(todo => <li class={this.completedClass(todo)} >{todo.task}</li>)}
        </ul>
      </div>
    );
  }
}

interface Todo {
  task: string;
  completed: boolean;
}
```

The property is defined as an array and typed with the Todo interface, as well. When the component receives this value, we iterate over each of the items in the array using **map** and display them in a **li** tag. There is also a **completedClass** method, which returns **completed** or empty string if the **completed** property of the each todo is **true** or **false** respectively.

> **Info** **Note:** States are mutable and can be changed at runtime, while props will always retain the value it received throughout runtime. Props also are received as attributes via the component's tag.
