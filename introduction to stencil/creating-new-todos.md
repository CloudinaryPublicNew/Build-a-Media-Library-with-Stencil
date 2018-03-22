## Creating New Todos

You have learned so much about Stencil and Stencil components. Before we conclude, let's add another component that we can use to add more todo items to the todo list:

```
// components/todo-form/todo-form.tsx
import { Component, Event, EventEmitter, State } from '@stencil/core';

@Component({
  tag: 'todo-form',
  styleUrl: 'todo-form.scss'
})
export class TodoForm {

  @Event() newTodo: EventEmitter;
  @State() todo: string;


  handleChange(e) {
    this.todo = (e.target as HTMLTextAreaElement).value;
  }

  handleNewTodo() {
    this.newTodo.emit(this.todo);
    this.todo = '';
  }

  render() {
    return (
      <div class="todo-form">
        <input type="text" class="form-control" placeholder="New Task" value={this.todo} onChange={this.handleChange.bind(this)} />
        <button onClick={this.handleNewTodo.bind(this)}>Add</button>
      </div>
    );
  }
}
```

Not so much a big difference from what we have dealt with in previous sections. Here are the obvious additions:

* We have an internal state property (todo) that tracks the text being entered in the input field. When the value changes, we set the value of the state property to the new value of the input field.

* There is a button that submits the current value of todo anytime the button is clicked. It does so by triggering a handleNewTodo method which in turn emits a newTodo custom event.

Back to the parent component, we can add a listener to update the list of todo items:

```
import { Component, State, Listen } from '@stencil/core';

export class Site {
  @State() todos: Todo[] = [
    {task: 'Cook', completed: false},
    {task: 'Dance', completed: true},
    {task: 'Eat', completed: false}
  ];

  @Listen('newTodo')
  newTodo(e) {
    const newTodo = {
      task: e.detail,
      completed: false
    };
    this.todos = [...this.todos, newTodo];
  }
 ...
 render() {
    return (
      <div class="wrapper">
        ...
        <div class="container">
          <div class="row">
            <div class="col-md-offset-4 col-md-4 col-sm 12">
              <todo-form></todo-form>
              <todo-list todos={this.todos}></todo-list>
            </div>
          </div>
        </div>
      </div>
    );
  }
}
...
```

* The newTodo method, which handles the custom event, updates the list of todos with the new task we added.

* We also added the form component in the render method: `<todo-form></todo-form>`.

![Creating new Todos](https://cloudinary-res.cloudinary.com/image/upload/w_700,c_fill/dpr_auto/Screen_Shot_2017-09-25_at_6.45.20_AM_lrsizi.png)