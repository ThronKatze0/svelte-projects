<script lang="ts">
  let counter: number = 0;
  let input: number = NaN;
</script>

<h1>{counter}</h1>
<button
  on:click={() => {
    counter++;
  }}>Plus</button
>
<button
  on:click={() => {
    counter = 0;
  }}>Reset</button
>
<br />
<input type="number" bind:value={input} />
<button
  on:click={() => {
    counter += input;
    input = NaN;
  }}>Plus Custom</button
>
