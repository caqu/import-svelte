<script>
  import { onMount } from "svelte";
  import BundledChild from "./BundledChild.svelte";

  let DynamicallyLoadedChild;

  import("/build/child.js").then(function(_module) {
    DynamicallyLoadedChild = _module.default;
  });

  function remove_child() {
    DynamicallyLoadedChild = undefined;
  }

  ////
  let BundledChildRef = BundledChild;
  function remove_bundled_child() {
    BundledChildRef = undefined;
  }
  /////////////
  let DynamicallyLoadedChildWithFadeOut;

  import("/build/child_with_fade.js").then(function(_module) {
    DynamicallyLoadedChildWithFadeOut = _module.default;
  });
  function remove_child_with_fade() {
    DynamicallyLoadedChildWithFadeOut = undefined;
  }
</script>

<main>
  <h1>Dynamically imported child components</h1>
  <div style="background:#ccc;padding:10px">
    <svelte:component this={DynamicallyLoadedChild} />
  </div>
  <button on:click={remove_child}>Remove loaded child</button>
  // OK
  <div style="background:#ccc;padding:10px">
    <svelte:component this={BundledChildRef} />
  </div>
  <button on:click={remove_bundled_child}>
    Remove bundled child that uses out:fade outro
  </button>
  // OK
  <hr />
  <div style="background:#ccc;padding:10px">
    <svelte:component this={DynamicallyLoadedChildWithFadeOut} />
  </div>
  <button on:click={remove_child_with_fade}>
    Remove loaded child that uses out:fade outro
  </button>
  // Outro error
</main>

<hr />
<pre>Source code at https://github.com/caqu/import-svelte</pre>
