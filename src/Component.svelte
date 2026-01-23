<script>
  import { getContext } from "svelte";
  import Interval from "./lib/Interval.svelte";
  const { styleable } = getContext("sdk");
  const component = getContext("component");
  export let isActive = true;
  $: dataContext = {
  	isActive
  }

  export let trigger;
  export let interval;
  export let display;
  export let displayIcon;
  export let text;

  if (!interval) isActive=false;
</script>

<div use:styleable={$component.styles}>
  <Interval on:trigger={trigger} interval={interval} display={display} displayIcon={displayIcon} text={text} isActive={isActive}/>
</div>
