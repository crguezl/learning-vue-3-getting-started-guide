## Introduction to Vue.js 3 {#introduction}

Vue (pronounced /vjuː/, like view) is a progressive framework for building user interfaces. 

Unlike other monolithic frameworks, Vue is designed from the ground up to be incrementally adoptable. 

The core library is focused on the view layer only, and is easy to pick up and integrate with other libraries or existing projects. 

On the other hand, Vue is also perfectly capable of powering sophisticated Single-Page Applications when used in combination with [modern tooling](https://v3.vuejs.org/guide/single-file-component.html) and [supporting libraries](https://github.com/vuejs/awesome-vue#components--libraries).

<a href="https://www.vuemastery.com/courses/intro-to-vue-3/intro-to-vue3" target="_blank" rel="sponsored noopener" title="Watch a free video course on Vue Mastery">Watch a video course on Vue Mastery</a>

The easiest way to try out Vue.js is using the <a href="https://codepen.io/team/Vue/pen/KKpRVpx" target="_blank" rel="noopener noreferrer">Hello World example<span>:

```html
<div id="hello-vue" class="execution">
  {{ message }}
</div>

<script>
const HelloVueApp = {
  data() {
    return {
      message: 'Hello Vue!!'
    }
  }
}

let helloVue = Vue.createApp(HelloVueApp).mount('#hello-vue')
</script>
```

<div id="hello-vue" class="execution">
  {{ message }}
</div>

<script>
const HelloVueApp = {
  data() {
    return {
      message: 'Hello Vue!!'
    }
  }
}

let helloVue = Vue.createApp(HelloVueApp).mount('#hello-vue')
</script>


### Declarative Rendering and v-on

At the core of Vue.js is a system that enables us to declaratively render data to the DOM using straightforward template syntax:


```html
<div id="counter">
  Counter: {{ counter }}
</div>

<script>
const Counter = {
  data() {
    return {
      counter: 0
    }
  }
}

let counterApp = Vue.createApp(Counter).mount('#counter')
</script>
```

**Execution:**

<div id="counter" class="execution">
  Counter: {{ counter }}
</div>

<script>
const Counter = {
  data() {
    return {
      counter: 0
    }
  }
}

let counterApp = Vue.createApp(Counter).mount('#counter')
</script>

We have already created our very first Vue app! 

This looks pretty similar to rendering a string template, but Vue has
done a lot of work under the hood. <strong>The data and the DOM are now linked</strong>, 
and everything is now <strong>reactive</strong>!.

<img src="assets/images/vue3-debugging.png" width="90%" />


Take a look at the example below where `counter` property increments every second and you will see how rendered DOM changes:

```html
<div id="counter2" class="execution input-group mb-3"">
  Counter: {{ counter }}
  <div class="input-group-append">
  <button v-on:click="stopTimer" class="btn btn-danger">Stop Timer</button>
  </div>
</div>

<script>
const Counter2 = {
  data() {
    return {
      clock: null,
      counter: 0
    }
  },
  mounted() {
    this.clock = setInterval(() => {
      this.counter++
    }, 1000)
  },
  methods: {
    stopTimer() {
      clearInterval(this.clock);
      this.counter = 0;
    }
  }
}

const Counter2App = Vue.createApp(Counter2).mount('#counter2')
</script>
```

<div id="counter2" class="execution input-group mb-3"">
  Counter: {{ counter }}
  <div class="input-group-append">
  <button v-on:click="stopTimer" class="btn btn-danger">Stop Timer</button>
  </div>
</div>

<script>
const Counter2 = {
  data() {
    return {
      clock: null,
      counter: 0
    }
  },
  mounted() {
    this.clock = setInterval(() => {
      this.counter++
    }, 1000)
  },
  methods: {
    stopTimer() {
      clearInterval(this.clock);
      this.counter = 0;
    }
  }
}

const Counter2App = Vue.createApp(Counter2).mount('#counter2')
</script>

To let users interact with our app, we can use the `v-on` directive to attach event listeners that invoke methods on our instances.

Note that in this method we update the state of our app without touching the DOM - all DOM manipulations are handled by Vue, and the code you write is focused on the underlying logic.


In addition to text interpolation, we can also bind element attributes like this:

<div id="bind-attribute" class="execution">
  <span v-bind:title="message">
    Hover your mouse over me for a few seconds to see my dynamically bound
    title!
  </span>
</div>

<script>
const AttributeBinding = {
  data() {
    return {
      message: 'You loaded this page on ' + new Date().toLocaleString()
    }
  }
}

Vue.createApp(AttributeBinding).mount('#bind-attribute')
</script>

Here we're encountering something new. 

The <code>v-bind</code> attribute you're seeing is called a <strong>directive</strong>. 

Directives are prefixed with <code>v-</code> to indicate that they are special attributes provided by Vue, 
and as you may have guessed, they apply special reactive behavior to the rendered DOM. 

Here, we're basically saying 
"<em>keep this element's <code>title</code> attribute up-to-date with the <code>message</code> property on the current active instance.</em>"

### Handling User Input with v-on and v-model

To let users interact with our app, we can use the `v-on` directive to attach event listeners that invoke methods on our instances.

Note that in this method we update the state of our app without touching the DOM - all DOM manipulations are handled by Vue, and the code you write is focused on the underlying logic.


```html 

<div id="event-handling" class="execution">
  <p>{{ message }}</p>
  <button v-on:click="reverseMessage" class="btn btn-danger">Reverse Message</button>
</div>

<script>
const EventHandling = {
  data() {
    return {
      message: 'Hello Vue.js!'
    }
  },
  methods: {
    reverseMessage() {
      this.message = this.message
        .split('')
        .reverse()
        .join('')
    }
  }
}

let EventHandlingApp = Vue.createApp(EventHandling).mount('#event-handling')
</script>
```

<div id="event-handling" class="execution">
  <p>{{ message }}</p>
  <button v-on:click="reverseMessage" class="btn btn-danger">Reverse Message</button>
</div>

<script>
const EventHandling = {
  data() {
    return {
      message: 'Hello Vue.js!'
    }
  },
  methods: {
    reverseMessage() {
      this.message = this.message
        .split('')
        .reverse()
        .join('')
    }
  }
}

let EventHandlingApp = Vue.createApp(EventHandling).mount('#event-handling')
</script>

Vue also provides the v-model directive that makes two-way binding between form input and app state a breeze:

```html 
<div id="two-way-binding">
  <p>{{ message }}</p>
  <input v-model="message" />
</div>

<script>
const TwoWayBinding = {
  data() {
    return {
      message: 'Write inside the box!'
    }
  }
}

let twoWayBindingApp = Vue.createApp(TwoWayBinding).mount('#two-way-binding')
</script>
```

<div id="two-way-binding">
  <p>{{ message }}</p>
  <input v-model="message" />
</div>

<script>
const TwoWayBinding = {
  data() {
    return {
      message: 'Write inside the box!'
    }
  }
}

let twoWayBindingApp = Vue.createApp(TwoWayBinding).mount('#two-way-binding')
</script>

Open the developer tools and change `twoWayBindingApp.message`


### Conditionals and Loops

#### v-if 

It's easy to toggle the presence of an element, too:

```html
<div id="conditional-rendering" class="execution">
  <span v-if="seen">Now you see me</span>
</div>

<script>
const ConditionalRendering = {
  data() {
    return {
      seen: true
    }
  }
}

const ConditionalRenderingApp = Vue.createApp(ConditionalRendering).mount('#conditional-rendering')
</script>
```

<div id="conditional-rendering" class="execution">
  <span v-if="seen">Now you see me</span>
</div>

<script>
const ConditionalRendering = {
  data() {
    return {
      seen: true
    }
  }
}

const ConditionalRenderingApp = Vue.createApp(ConditionalRendering).mount('#conditional-rendering')
</script>

This example demonstrates that we can bind data to not only text and attributes, 
**but also the structure of the DOM**. 

Moreover, Vue also provides a powerful transition effect system that can automatically 
apply transition effects when elements are inserted/updated/removed by Vue.

You can change `ConditionalRenderingApp.seen = false` in the developper tools to check the effect.

#### v-for

The `v-for` directive can be used to display a list of items using the data from an array:

```html
<div id="list-rendering">
  <ol>
    <li v-for="todo in todos">
      {{ todo.text }}
    </li>
  </ol>
</div>

<script>
const ListRendering = {
  data() {
    return {
      todos: [
        { text: 'Learn JavaScript' },
        { text: 'Learn Vue' },
        { text: 'Build something awesome' }
      ]
    }
  }
}

const ListRenderingApp = Vue.createApp(ListRendering).mount('#list-rendering')
</script>
```

<div id="list-rendering" class="execution">
  <ol>
    <li v-for="todo in todos">
      {{ todo.text }}
    </li>
  </ol>
</div>

<script>
const ListRendering = {
  data() {
    return {
      todos: [
        { text: 'Learn JavaScript' },
        { text: 'Learn Vue' },
        { text: 'Build something awesome' }
      ]
    }
  }
}

const ListRenderingApp = Vue.createApp(ListRendering).mount('#list-rendering')
</script>

Open the developer tools and add a new item: `ListRenderingApp.todos.push({text:"Learn TypeScript"})`


### Composing with Components

The component system is another important concept in Vue, because it's an abstraction that allows us to build large-scale applications composed of small, self-contained, and often reusable components.

 If we think about it, almost any type of application interface can be abstracted into a tree of components:

 ![](assets/images/components.png){width="60%"}

In Vue, a component is essentially an instance with pre-defined options. 

Registering a component in Vue is straightforward: 

1. We create a component object as we did with App objects and 
2. We define it in parent's `components` option:

```html

<div id="todo-list-app1" class="execution">
<ol>
  <todo-item
      v-for="item in 3" 
      v-bind:key="item"
    >
</ol>
</div>

<script>
// Create Vue application
const TodoListApp1 = Vue.createApp({
  components: {
    todoItem: { template: `<li>This is a todo</li>`} // Register a new component
  }
}).mount('#todo-list-app1')
</script>
```

<div id="todo-list-app1" class="execution">
<ol>
  <todo-item
      v-for="item in 3" 
      v-bind:key="item"
    >
</ol>
</div>

<script>
// Create Vue application
const TodoListApp1 = Vue.createApp({
  components: {
    todoItem: { template: `<li>This is a todo</li>`} // Register a new component
  }
}).mount('#todo-list-app1')
</script>

But this would render the same text for every todo, which is not super interesting. 

We should be able to pass data from the parent scope into child components. 

Let's modify the component definition to make it accept a prop:

```js
app.component('todo-item', {
  props: ['todo'],
  template: `<li>{{ todo.text }}</li>`
})
```

Now we can pass the todo into each repeated component using `v-bind`:


```html
<div id="todo-list-app" class="execution">
  <ol>
    <!--
      Now we provide each todo-item with the todo object
      it's representing, so that its content can be dynamic.
      We also need to provide each component with a "key",
      which will be explained later.
    -->
    <todo-item
      v-for="item in groceryList"
      v-bind:todo="item"
      v-bind:key="item.id"
    ></todo-item>
  </ol>
</div>

<script>
const TodoList = {
  data() {
    return {
      groceryList: [
        { id: 0, text: 'Vegetables' },
        { id: 1, text: 'Cheese' },
        { id: 2, text: 'Whatever else humans are supposed to eat' }
      ]
    }
  }
}

const TodoListAapp = Vue.createApp(TodoList)

TodoListAapp.component('todo-item', {
  props: ['todo'],
  template: `<li>{{ todo.text }}</li>`
})

TodoListAapp.mount('#todo-list-app')
</script>
```

**Execution:**

<div id="todo-list-app" class="execution">
  <ol>
    <!--
      Now we provide each todo-item with the todo object
      it's representing, so that its content can be dynamic.
      We also need to provide each component with a "key",
      which will be explained later.
    -->
    <todo-item
      v-for="item in groceryList"
      v-bind:todo="item"
      v-bind:key="item.id"
    ></todo-item>
  </ol>
</div>

<script>
const TodoList = {
  data() {
    return {
      groceryList: [
        { id: 0, text: 'Vegetables' },
        { id: 1, text: 'Cheese' },
        { id: 2, text: 'Whatever else humans are supposed to eat' }
      ]
    }
  }
}

const TodoListAapp = Vue.createApp(TodoList)

TodoListAapp.component('todo-item', {
  props: ['todo'],
  template: `<li>{{ todo.text }}</li>`
})

TodoListAapp.mount('#todo-list-app')
</script>
