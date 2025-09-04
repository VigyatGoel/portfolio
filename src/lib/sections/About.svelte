<script>
  import Section from '../ui/Section.svelte';
  const { data } = $props();
  const about = $derived(data?.about || '');
  const aboutParagraphs = $derived(about.split('\n\n').filter(p => p.trim()));
</script>

<Section id="about" title="About Me" description="">
  <div class="about">
    {#each aboutParagraphs as paragraph}
      <p>{paragraph}</p>
    {/each}
  </div>
</Section>

<style>
  .about p { 
    margin: 0 0 1rem 0; 
    color: var(--fg); 
    font-size: clamp(1.3rem, 3vw, 1rem);
    line-height: 1.7;
    text-align: justify;
  }
  .about p:last-child { margin-bottom: 0; }
</style>
