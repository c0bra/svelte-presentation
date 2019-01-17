# HTML Syntax

(Spoiler: It's [HTMLX](https://github.com/htmlx-org/HTMLx))


# Interpolated Tags

```html
<div>{name}</div>
<div>{Math.floor(counter / 2)}</div>
<div style="color: {color}">Foo</div>
<div hidden={isHidden}>Bar</div>
<div {hidden}>Maybe I'm hidden</div>

<!-- Transitions -->
<p in:fly="{y: 50}" out:fade>flies up, fades out</p>

<script>
  import { fade, fly } from 'svelte-transitions';
</script>
```


# Logic

```html
<div>
  {#if counter > 0}
    More than zero
  {:elseif counter < 0}
    Less than zero
  {:else}
    Zero
  {/if}
</div>
```


# Loops

```html
<ul>
  <!-- Destructure loop variables -->
  {#each developers as {name, location}, i}
    <li>{i} - {name}, {location}</li>
  {:else}
    <li>No developers!</li>
  {/each}
</ul>
```


# Async

```html
<script>
  let promise = fetch('https://reqres.in/api/users')
    .then(res => res.json())
    .then(res => res.data);
</script>

<div>
  {#await promise}
    Fetching...
  {:then users}
    {#each users as {name}} {name} {/each}
  {:catch error}
    <p>Couldn't fetch users: {error}</p>
  {/await}
</div>
```


# Directives

`x:y` - Event handlers, bindings, transitions

```html
<button on:click="{() => counter += 1}">+1</button>

<!-- Two-way binding -->
<input bind:value={name}>

<!-- Attribute binding -->
<span class:active={isActive}>Am I active?</span>

<!-- Bring element into js -->
<canvas bind:this={canvas}></canvas>
```


# Special elements

* `<svelte:self>` recursion
* `<svelte:component>` dynamic components
* `<svelte:window>` window event listeners
* `<svelte:body>` similar
* `<svelte:head>` title element, etc


# Dynamic content with `<slot>`

```html
<!-- Box.html -->
<div>
  <slot></slot>

  <small><slot name="comment"></slot></small>
</div>
```

```html
<Box>
  Box content here

  <span slot="comment">Comment here</span>
</Box>

<script>
  import Box from './Box.html';
</script>
```


# Styles


# Scoped CSS

Styles are scoped by default

```html
<style>
  .red {
    color: red
  }
</style>
```

becomes

```css
.red.svelte-1xi0wsh {
  color:red
}
```


# :global()

Modifier makes classes global

```html
<style>
  .user :global(p) {
    font-size: 2rem;
  }
</style>
```


# Unused styles

Removed automatically! ✨
