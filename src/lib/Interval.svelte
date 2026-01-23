<script>
  import { createEventDispatcher, onDestroy } from "svelte";
  import stopwatchSvg from "./icons/stopwatch.svg";

  const dispatch = createEventDispatcher();

  export let interval;
  export let isActive;
  export let display = true;
  export let displayIcon = true;
  export let text = "Interval";

  let intervalID = null;

  // On mémorise le "dernier état effectif" appliqué
  let lastActive = null;
  let lastSeconds = null;

  function stop() {
    if (intervalID) {
      clearInterval(intervalID);
      intervalID = null;
    }
  }

  function start(seconds) {
    intervalID = setInterval(() => dispatch("trigger"), seconds * 1000);
  }

  $: {
    const seconds = Number(interval);
    const active = (isActive === true) && (seconds > 0);

    // do nothing is already active
    if (active === lastActive && seconds === lastSeconds) {
      // no-op
    } else {
      // apply the new value
      stop();
      if (active) start(seconds);

      lastActive = active;
      lastSeconds = seconds;
    }
  }

  onDestroy(stop);
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
