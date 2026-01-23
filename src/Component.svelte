<script>
  import { getContext } from "svelte";
  import Interval from "./lib/Interval.svelte";

  const { styleable } = getContext("sdk");
  const component = getContext("component");

  export let isActive;
  export let interval;
  export let trigger;
  export let display;
  export let displayIcon;
  export let text;

  function toBool(v, d = false) {
    if (v === true) return true;
    if (v === false) return false;
    if (v == null) return d;

    if (typeof v === "number") return v !== 0;

    if (typeof v === "string") {
      const s = v.trim().toLowerCase();
      if (["true","1","yes","y","on","ok"].includes(s)) return true;
      if (["false","0","no","n","off",""].includes(s)) return false;
      try { return toBool(JSON.parse(v), d); } catch { return d; }
    }

    try { return toBool(JSON.parse(JSON.stringify(v)), d); }
    catch { return d; }
  }

  // ✅ bool interne fiable
  $: active = toBool(isActive, false);

  // optionnel : interval invalide => désactivation
  $: if (!Number(interval) || Number(interval) <= 0) active = false;

  // ✅ EXPOSE ce que Budibase attend dans le context
  $: activated = active;
</script>

<div use:styleable={$component.styles}>
  <Interval
    interval={interval}
    isActive={active}
    display={display}
    displayIcon={displayIcon}
    text={text}
    on:trigger={trigger}
  />
</div>
