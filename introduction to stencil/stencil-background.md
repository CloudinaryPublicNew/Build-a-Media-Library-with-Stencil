## [Background](https://cloudinary.com/blog/getting_started_with_stenciljs#background)

Stencil is basically a compiler, not necessarily a UI library. A compiler that transforms TSX \(TypeScript + JSX\) into self-contained custom components.

Before you start learning about the tool, it’s important to note that Stencil is not another heavy JavaScript framework you need to learn. If you have worked with Angular or React, or understand web components, then Stencil is worth a look.

Stencil enables you to write some TSX and SCSS, which it compiles down into shippable components. It was built by the Ionic team to help them write smaller, reusable components without having to carry along the weight of Angular. However, this led to solving a more general problem. We can write platform-independent component with our favorite tools \(TS, JSX, etc\) and compile to standard custom components which can then be used with any framework and supporting browsers. All features of Stencil boil down to optimization and performance, which is the motivation behind Stencil.

Stencil also provides a lot of progressive features out of the box, including easy server-side rendering and service worker installation. Now let’s take a look at a practical approach to using Stencil and some of its interesting features.

  


