## Overview {#title}

In this code lab, you'll learn about Stencil - a new compiler for composing user interfaces using pure custom components. Stencil enables you to build components using new, cutting-edge technologies, such as TypeScript and JSX, then generates a pure custom component that can be used anywhere supported. In essence, you can import a Stencil generated component into React, Angular, Vue, e.t.c.



  


## **What you'll need**

* Basic knowledge of HTML and JavaScript
* Enthusiasm for going
  _fast_
  on the web
* Your favourite browser that supports Web Assembly—we recommend Chrome 57+
* The Emscripten SDK
* The sample code, available in the next step

## **What you'll build**

* You'll take an existing simple "Conway's Game of Life" game, written in C, and interface with it via JavaScript
* You'll also take a venerable Mandelbrot viewer, and expose it as a C++ class to JavaScript, using
  [Emscripten's Embind](https://kripken.github.io/emscripten-site/docs/porting/connecting_cpp_and_javascript/embind.html)
  functionality

Keep in mind that you don't_need_Emscripten to build Web Assembly, but it greatly simplifies the process—just like regular hardware assembly, Web Assembly can be tough to work with by hand.

If you'd like to learn more about Web Assembly, be sure to check out[Alex Danilo's Web Assembly talk](https://www.youtube.com/watch?v=6v4E6oksar0)\(recorded on the 1st day of I/O 2017\).

