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
* CSS
  * Styles are scoped by default
  * `:global()` to unscope
  * Unused styles are removed automatically
* Special elements
  * self (recursive)
  * component (dynamic components)
  * window, body, head