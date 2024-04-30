<script lang="typescript">
  let count = 0;
  function countUp() {
    count += 1;
  }
  function reset() {
    count = 0;
  }
</script>

<h2>Counter</h2>
<p>{count}</p>
<button on:click={countUp}>Count up</button>
<button on:click={reset}>Reset</button>
