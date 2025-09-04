<script>
  // Simple reveal-on-scroll wrapper
  const { as = 'div', direction = 'up', delay = 0, className = '', children } = $props();
  let el;
  let visible = $state(false);

  $effect(() => {
    const node = el;
    if (!node) return;
    const io = new IntersectionObserver(
      (entries) => {
        for (const e of entries) {
          if (e.isIntersecting) {
            visible = true;
            io.disconnect();
            break;
          }
        }
      },
      { rootMargin: '0px 0px -10% 0px', threshold: 0.15 }
    );
    io.observe(node);
    return () => io.disconnect();
  });
</script>

<svelte:element this={as} bind:this={el} class={"reveal " + (visible ? 'in' : '') + ' dir-' + direction + (className ? ' ' + className : '')} style={"--rev-delay:" + delay + "ms"}>
  {@render children?.()}
</svelte:element>

<style>
  .reveal { opacity: 0; transform: translate3d(0, 8px, 0); transition: opacity .5s ease, transform .6s cubic-bezier(.2,.7,.2,1); transition-delay: var(--rev-delay, 0ms); }
  .reveal.dir-up { transform: translate3d(0, 14px, 0); }
  .reveal.dir-down { transform: translate3d(0, -14px, 0); }
  .reveal.dir-left { transform: translate3d(14px, 0, 0); }
  .reveal.dir-right { transform: translate3d(-14px, 0, 0); }
  .reveal.in { opacity: 1; transform: none; }

  @media (prefers-reduced-motion: reduce) {
    .reveal { opacity: 1; transform: none; transition: none; }
  }
</style>
