<script>
  // Svelte 5 runes mode props
  let {
    isActive = true,
    interval = 10,
    trigger = undefined, // function callback from parent/budibase
  } = $props();

  $effect(() => {
    const seconds = Number(interval);

    // Stop timer when inactive OR invalid interval
    if (!isActive || !Number.isFinite(seconds) || seconds <= 0) return;

    const id = window.setInterval(() => {
      // Safely call callback if provided
      trigger?.();
    }, seconds * 1000);

    // Cleanup on prop change/unmount
    return () => window.clearInterval(id);
  });
</script>
