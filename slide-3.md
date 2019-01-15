# State managemenet


# Internal state

```html
<script>
  // count is available internal
	let count = 0;
</script>

<div>{count}</div>
```


# External props

```html
<!-- Counter.html -->
<div>{count}</div>

<script>
  export let count = 0;
</script>
```

```html
<!-- App.html -->
<Counter count={count}></Counter>

<script>
  import Counter from './Counter.html';

  let count = 20;
</script>
```


# Lifecycle hooks

```html
<script>
	import { onMount, beforeUpdate, afterUpdate, onDestroy } from 'svelte';
</script>
```


# Event modifiers

```html
<div on:click|stopPropagation|preventDefault="{() => foo = !foo}">...</div>
```


# Component events

* Callbacks
* Event dispatching



# Binding callbacks

Callbacks are simply exposed function props

```html
<div>
  <!-- `changed` is an exposed prop -->
	<Select changed="{val => changedVal = val}"></Select>
	<br/>
	Changed to: {changedVal || ''}
</div>

<script>
	import Select from './Select.html';
	
	let changedVal;
</script>
```


# Triggering callbacks

```html
<!-- call `changed` prop -->
<select on:change="{e => changed(e.target.value)}">
	<option>1</option>
	<option>2</option>
</select>

<script>
  // Expose changed prop
  export let changed;
</script>
```


# Event dispatching

```html
<!-- Component.html -->
<script>
  import { createEventDispatch } from 'svelte';

  const dispatch = createEventDispatcher();

  setInternval(() => {
    dispatch('tick', { date: new Date() });
  }, 1000);
</script>
```

```html
<div>
  {newTickdate}
  <!-- e is a CustomEvent instance -->
  <Component on:tick="{e => newTickdate = e.detail.date}"></Component>
</div>

<script>
  let newTickDate;
</script>
```
