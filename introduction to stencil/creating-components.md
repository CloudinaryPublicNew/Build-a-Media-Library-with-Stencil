## Creating Components

Each component is saved in a containing folder, such as a TSX file. The containing folder also can contain an SCSS file for the component's styles.

Let's start with a container component that will serve as the app's shell. Create a folder named **site** in the **components** folder, then add **site.tsx** and **site.scss** files in the folder. You just created an empty Stencil component.

Throughout the article, we will skip the SCSS contents for brevity. You can grab them from the [GitHub repo provided](https://github.com/christiannwamba/stencil-gs). With that in mind, let's add some component content:

```
// components/site/site.tsx
import { Component } from '@stencil/core';

@Component({
  tag: 'todo-site',
  styleUrl: 'site.scss'
})
export class Site {

  render() {
    return (
      <div class="wrapper">
        <nav>
          <div class="container">
            <h2>To - Do</h2>
          </div>
        </nav>
        <div class="container">
          <div class="row">
            <div class="col-md-offset-4 col-md-4 col-sm 12">
                {/* Todo App goes here */}

            </div>
          </div>
        </div>
      </div>
    );
  }
}
```

* The **Component** decorator - which is imported from @stencil/core - defines a class as a component.

* The **Site** class, which is decorated with the Component decorator, gets extended by the decorator to posses component features.

* One of these features is having a tag, a style and a template. The tag and style is defined using an object and passing the object as argument to the decorator. The **render** method returns JSX, which serves as the template for the component. This template is what gets rendered to the browser when the component is mounted.

The tag is used to mount the component. In this case, replace **my-name** tag in `index.html` with the following:

```
<todo-site></todo-site>
```

Then run the app using `npm start`. You should get the following:

![Todo](https://cloudinary-res.cloudinary.com/image/upload/w_700,c_fill/dpr_auto/getting-started-with-stencil_jbni1b.png)