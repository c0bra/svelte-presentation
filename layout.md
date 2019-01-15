# Layout

* HTML
  * Interpolated tags (`{}`)
  * Conditionals: `#if`, `:else`, `:elseif`
  * Loops: `#each` 
  * Promises: `#await`, `:then`, `:catch`
  * Directives: `x:`
    * `class:`
    * `style:`
    * `on:`
    * transitions
  * Event handling: `on:*`
    * `on:click=""`
  * Special elements
    * self (recursive)
    * component (dynamic components)
    * window, body, head
* CSS
  * Styles are scoped by default
  * `:global()` to unscope
  * Unused styles are removed automatically
* Component state
  * Internal
  * External
  * Lifecycle hooks
  * Callbacks
  * Event dispatching
* State management
  * Store
* Sapper
  * Static sites