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
      counter: 1
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

Vue.createApp(Counter2).mount('#counter2')
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

Vue.createApp(Counter2).mount('#counter2')
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

Vue.createApp(EventHandling).mount('#event-handling')
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

Vue.createApp(EventHandling).mount('#event-handling')
</script>

