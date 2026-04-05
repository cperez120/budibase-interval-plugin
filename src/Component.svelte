<script>
  import stopwatchSvg from "./lib/icons/stopwatch.svg";
  import { getContext } from "svelte";

  import Interval from "./lib/Interval.svelte";

  const { styleable } = getContext("sdk");
  const component = getContext("component");

  // Props in runes mode
  let {
    isActive = true,
    interval = 10,
    display = true,
    displayIcon = false,
    text = "",
    trigger = undefined, // <-- Budibase action prop
  } = $props();
</script>

<div use:styleable={component?.styles}>
  <!-- Timer runner (no UI) -->
  <Interval
    isActive={isActive}
    interval={interval}
    trigger={trigger}
  />

  {#if display}
    <div class="intervalContainer">
      {#if displayIcon}
        {@html stopwatchSvg}
      {/if}
      <span>{text}</span>
    </div>
  {/if}
</div>

<style>
  .intervalContainer {
    display: flex;
    align-items: center;
    gap: 5px;
  }
</style>
