<script>
  import { createEventDispatcher, onDestroy } from "svelte";
  import stopwatchSvg from './icons/stopwatch.svg';

  const dispatch = createEventDispatcher();
  export let interval;
  export let isActive;
  export let display = true;
  export let displayIcon = true;
  export let text = "Interval";

  let intervalID = null;

  if (interval > 0 && isActive) {
    intervalID = window.setInterval(() => { dispatch("trigger"); }, interval * 1000);
  }

  onDestroy(() => {
    if(intervalID) window.clearInterval(intervalID);
  });
</script>

{#if display}
  <div class="container">
    {#if displayIcon}
    {@html stopwatchSvg} 
    {/if}
    <span>{text}</span>
  </div>
{/if}

<style>
  .container {
    display: flex;
    align-items: center;
    gap: 5px;
  }
</style>
