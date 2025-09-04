<script>
  let { id = '', title = '', description = '', children } = $props();
</script>

<section id={id} class="section">
  {#if title}
    <h2 class="section-title">{title}</h2>
  {/if}
  {#if description}
    <p class="section-description">{description}</p>
  {/if}
  <div class="section-body">
    {@render children?.()}
  </div>
</section>

<style>
  .section {
    padding: clamp(2rem, 6vw, 5rem) 0;
    border-bottom: 1px solid var(--border);
  }
  .section-title {
    font-size: clamp(1.4rem, 2.8vw, 2rem);
    font-weight: 700;
    margin: 0 0 1.25rem 0;
    letter-spacing: 0.3px;
    transition: color .2s ease;
    text-align: center;
  }
  .section-description {
    font-size: clamp(0.9rem, 2vw, 1.1rem);
    color: var(--muted);
    text-align:justify;
    margin: 0 auto 2rem auto;
    max-width: 100ch;
    line-height: 1.6;
  }
  .section-body { display: grid; gap: 1rem; }
</style>
