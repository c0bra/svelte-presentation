---
title: Svelte Lunch & Learn
pdf: svelte-lunch-and-learn.pdf
slideNumber: true
controls: true
---

# 

<img src="assets/svelte.svg" alt="logo" width="200"/> (v3)

A magically disappearing framework

# A compiler, not a runtime

```html
<!-- App.html -->
<h1>Hello {name}!</h1>
```

|
|

<small>Turns into Vanilla JS in the browser</small>


# The old days

```js
document.querySelector('input').addEventListener('input', function(event) {
  span.textContent = `Hello ${this.value}`;
});
```

<small>Directly attaching to DOM events. Gets messy fast.</small>


# Now

```html
<span>Hello, {{ name }}</span>
<input @input="name = $event.target.value">
```

<small>We write state-driven code, and it's the framework's job to tell the browser what to do.</small>


# DX vs UX {.ascii}

```render_a2s
                                #-----------------------------------#
#---------------------#         |[0]                                |
|[0]                  |         |   1. on state change              |
|                     |         |   2. re-render app                |
|  1. On event        |         |   3. reconcile new VDOM with the  |
|  2. Do this thing   |         |      current view, to figure out  |
|                     |         |      what we need to do           |
|                     |         |   4. do the things                |
#---------------------#         |                                   |
                                |                                   |
  Better for users              #-----------------------------------#

                                  Better for developers

[0]: {"fill": "lightyellow", "a2s:delref": true, "fillStyle": "solid"}
```


# Frameworks help us organize mentally

* Lets us think about our code as a series of interconnected states
* Abstracts away fiddly DOM management bits
* But that creates extra work (VDOM diffing, change detection) we didn't have to do originally


# Most frameworks have runtimes

* Runtimes that live in your browser
* When you ship your app you ship runtime too
* Examples: Angular, React, Vue
* Interpret your app code when browser loads


# What if you could have it both ways?

* State management
* Direct DOM manipulation


# Enter compilers!


# Compilers live in your dev env

* Turn your apps and components into plain JS
* Works as part of your build flow (webpack, rollup, parcel)
* Bundle overhead is just what's needed to modify DOM


# Why compile?


# Runtimes are big

> Svelte's Todo MVC weighs 3.6kb zipped. For comparison, React plus ReactDOM without any app code weighs about 45kb zipped

<small>Though they are getting smaller with Angular Ivy, React Prepack, etc.</small>

# Runtimes provide unnecessary code

* Difficult to tree-shake all of React
* Better to remove dead code or just don't generate it?


# Runtimes are slow 

![](assets/svelte-benchmarks2.jpg)


# Runtimes lock you in

No runtime means code can be re-used in any framework, or no framework.

|
|

Re-using Vue in React or vice-versa requires jumping through hoops. Don't even think about Angular (but maybe it's
easier with Ivy)


# How does Svelte work? {bg=white .dark-on-light}

```render_a2s
    #-------------#
    |             |
    | HTML Parser |------------+                            #---------------#
    |             |            |                            |   Blocks      |
    #-------------#            |                            |               |
                               |                            |  #----------# |
                               |                            |  | Main     | |
                               |      #----------------#    |  | Fragment | |
                               |      |                |    |  #----------# |
    #------------#             |      | Component AST  |--->|               |
    | Acorn (js) |-------------+----->|                |    |    #------#   |
    |            |             |      #----------------#    |    |      |   |
    #------------#             |                            |    #------#   |
                               |                            |               |
    #----------#               |                            |    #------#   |
    |          |               |                            |    |      |   |
    | css-tree |---------------+                            |    #------#   |
    |          |                                            #---------------#
    #----------#
```

<small>
Each block has methods for creating, updating, and destroying the DOM.
No need for Virtual DOM.

Svelte works with the DOM directly.
</small>


# How do you write Svelte?

Components are done in a single file, like Vue or React.

```html
<!-- Greeting.html -->
<h1>Hi, {name}, I'm your component!</h1>

<script>
  export let name = 'Bob';
</script>

<style>
  h1 {
    color: blue;
  }
</style>
```


# How do you use Svelte components?


```js
const greet = new Greeting({
  target: document.body,
  props: {
    name: 'Fred',
  },
});

// Plain prop accessors
greet.name = 'Bobby';

// Set multiple props
greet.$set({ name: 'Jimmy' });
```


# How you do you build with components?

```html
<!-- App.html -->
<div>
  <Greeting name={name}></Greeting>
</div>

<script>
  import Greeting from './Greeting.html';

  let name = 'Randall';
</script>
```