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


### Declarative Rendering

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

```html

<div id="counter2" class="execution">
  Counter: {{ counter }}
</div>


<script>
const Counter2 = {
  data() {
    return {
      counter: 0
    }
  },
  mounted() {
    setInterval(() => {
      this.counter++
    }, 1000)
  }
}

Vue.createApp(Counter2).mount('#counter2')
</script>
```

<div id="counter2" class="execution">
  Counter: {{ counter }}
</div>


<script>
const Counter2 = {
  data() {
    return {
      counter: 0
    }
  },
  mounted() {
    setInterval(() => {
      this.counter++
    }, 1000)
  }
}

Vue.createApp(Counter2).mount('#counter2')
</script>