## Events and Listeners

Now we got the problem of dynamic content of the table, we need to worry about interaction. How do we create new tasks? What happens when each todo item is clicked? Let's answer those questions now.

An event is raised when a user interacts with your component. We can create and emit custom events for such interactions. Events are raised with Event Emitters and are decorated with the **Event** decorator.

Let's see some event logic by clicking on each item in the todo list:

```
import { Component, Event, EventEmitter, Prop } from '@stencil/core';
export class TodoList {

  @Prop() todos: Todo[];
  @Event() toggleTodo: EventEmitter;

  ...

  // Event handler. Triggered by onClick
  // DOM event on the template in render()
  handleToggleTodo(todo) {
    this.toggleTodo.emit(todo)
  }

  render() {
    return (
      <div class="todo-list">
        <ul>
          {this.todos.map(todo => <li class={this.completedClass(todo)} onClick={this.handleToggleTodo.bind(this, todo)}>{todo.task}</li>)}
        </ul>
      </div>
    );
  }
}
```

In the render method, you can see we have an `onClick` attribute attached to each `li` method in the `map` iteration. This attribute attaches a DOM event; a click event to be precise.

When this button is clicked, the `handleToggleTodo` method is called with the right context while passing the actual todo item that was clicked.

The `handleToggleTodo` method then emits a custom event. This custom event (`toggleTodo`) is decorated as `Event` and defined as `EventEmitter` type. Calling `emit` on the custom event triggers a global event that we can listen to from anywhere in the app.

We can head to the parent component (Site) and create a listener for the event:

```
import { Component, State, Listen } from '@stencil/core';
...
export class Site {
  ...
  @Listen('toggleTodo')
  toggleTodo(e): void {
    // Retrieve event payload
    // from e.detail
    const todo = e.detail;
    this.todos = this.todos.map(x => {
      if (x.task === todo.task) {
        const updated = {
          task: x.task,
          completed: !x.completed
        };
        return updated;
      }
      return x;
    })
  }
  ...
}
```

The event listener is of course a decorated method. The method must be decorated with a `Listener` and the decorator is passed the actual name of the emitter; in our case `toggleTodo`.

![Todo Event](https://cloudinary-res.cloudinary.com/image/upload/w_700,c_fill/dpr_auto/Screen_Shot_2017-09-25_at_6.24.09_AM_vzbgkv.png)