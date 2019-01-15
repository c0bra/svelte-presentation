# Reactivity

* Stores
* Reactive declarations

# Stores


```js
// stores.js
import { writable } from 'svelte/store';

export const user = writable({ });
```

```html
<!-- $ prefix for stores -->
<div><b>User:</b> {$user.name}</div>

<script>
  import { onMount } from 'svelte';
  import { user } from './stores';

  onMount(async () => {
    const data = await (await fetch('/api/users')).json();
    user.$set(data);
  });
</script>
```
 

# Reactive declarations

`$:` the destiny operator

<small>
  Replaces `computed` values. Tells compiler to run statement any time value on
  eight-side changes.
</small>

```html
<p>Counter: {counter}</p>
<p>Double: {dobule}</p>
<button on:click="{counter += 1 }">+1</button>

<script>
  let counter = 1;
  $: double = counter * 2;
</script>
```