
## Application & Component Instances

## Creating an Application Instance

Every Vue application starts by creating a new **application instance**
with the `createApp` function:


```js
const app = Vue.createApp({
  /* options */
})
```

The application instance is used to register \'globals\' that can then
be used by components within that application:

```js
const app = Vue.createApp({})
app.component('SearchInput', SearchInputComponent)
app.directive('focus', FocusDirective)
app.use(LocalePlugin)
```

Most of the methods exposed by the application instance return that same
instance, allowing for chaining:

```js
Vue.createApp({})
  .component('SearchInput', SearchInputComponent)
  .directive('focus', FocusDirective)
  .use(LocalePlugin)
```

You can browse the full application API in the [API reference](https://v3.vuejs.org/api/application-api.html).

## The Root Component

The options passed to `createApp` are used to configure the **root
component**. That component is used as the starting point for rendering
when we **mount** the application.

An application needs to be mounted into a DOM element. For example, if
we want to mount a Vue application into `<div id="app"></div>`, we
should pass `#app`:

```js
const RootComponent = {
  /* options */
}
const app = Vue.createApp(RootComponent)
const vm = app.mount('#app')
```

Unlike most of the application methods, `mount` does not return the
application. Instead it returns the root component instance.

Although not strictly associated with the [MVVM
pattern![](https://en.wikipedia.org/wiki/Model_View_ViewModel),
Vue\'s design was partly inspired by it. 

As a convention, we often use
the variable `vm` (short for ViewModel) to refer to a component
instance.

While all the examples on this page only need a single component, most
real applications are organized into a tree of nested, reusable
components. For example, a Todo application\'s component tree might look
like this:

```text
Root Component
└─ TodoList
   ├─ TodoItem
   │  ├─ DeleteTodoButton
   │  └─ EditTodoButton
   └─ TodoListFooter
      ├─ ClearTodosButton
      └─ TodoListStatistics
```

Each component will have its own component instance, `vm`. 

For some
components, such as `TodoItem`, there will likely be multiple instances
rendered at any one time. 

All of the component instances in this
application will share the same application instance.

The root component isn\'t
really any different from any other component. 

The configuration options
are the same, as is the behavior of the corresponding component
instance.

## Component Instance Properties

Properties defined in
`data` are exposed via the component instance:

```js
const app = Vue.createApp({
  data() {
    return { count: 4 }
  }
})

const vm = app.mount('#app')

console.log(vm.count) // => 4
```

There are various other component options that add user-defined
properties to the component instance, such as 
`methods`, 
`props`,
`computed`, 
`inject` and 
`setup`. 

All of the properties of the component instance, no
matter how they are defined, will be accessible in the component\'s
template.

Vue also exposes some built-in properties via the component instance,
such as `$attrs` and `$emit`. 

These properties all have a `$` prefix to
avoid conflicting with user-defined property names.

## Lifecycle Hooks

Each component instance goes through a series of initialization steps
when it\'s created - for example, it needs to set up data observation,
compile the template, mount the instance to the DOM, and update the DOM
when data changes. Along the way, it also runs functions called
**lifecycle hooks**, giving users the opportunity to add their own code
at specific stages.

For example, the [created](https://v3.vuejs.org/api/options-lifecycle-hooks.html#created)
hook can be used to run code after an instance is created:

```js
Vue.createApp({
  data() {
    return { count: 1 }
  },
  created() {
    // `this` points to the vm instance
    console.log('count is: ' + this.count) // => "count is: 1"
  }
})
```

There are also other hooks which will be called at different stages of
the instance\'s lifecycle, such as

* [mounted](https://v3.vuejs.org/api/options-lifecycle-hooks.html#mounted),
* [updated](https://v3.vuejs.org/api/options-lifecycle-hooks.html#updated), and
* [unmounted](https://v3.vuejs.org/api/options-lifecycle-hooks.html#unmounted). 

All lifecycle
hooks are called with their `this` context pointing to the current
active instance invoking it.

::: {.custom-block .tip}
TIP

Don\'t use [arrow functions](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Functions/Arrow_functions)
on an options property or callback, such as

`created: () => console.log(this.a)` or

`vm.$watch('a', newValue => this.myMethod())`. 

Since an arrow function
doesn\'t have a `this`, `this` will be treated as any other variable and
lexically looked up through parent scopes until found, often resulting
in errors such as
`Uncaught TypeError: Cannot read property of undefined` or
`Uncaught TypeError: this.myMethod is not a function`.
:::

## Lifecycle Diagram

Below is a diagram for the instance lifecycle. You don\'t need to fully
understand everything going on right now, but as you learn and build
more, it will be a useful reference.

![](https://v3.vuejs.org/images/lifecycle.svg){width="840"
height="auto"}
