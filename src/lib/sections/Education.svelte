<script>
  import Section from '../ui/Section.svelte';
  import Reveal from '../ui/Reveal.svelte';
  const { data } = $props();
  const items = $derived(data?.education || []);
</script>

<Section id="education" title="Education" description="My academic journey reflects a deep interest in Artificial Intelligence, Machine Learning, and technology. Currently pursuing a B.Tech in AI/ML, I’ve built a strong foundation in computer science and mathematics. In school, I was honored with a Scholar Award for securing over 90.4% in Class 12, and I continue to carry that same dedication and passion for excellence into my undergraduate studies and beyond.">
  <div class="timeline" aria-label="Education timeline">
    {#each items as ed, i}
      <Reveal as="article" direction="up" delay={i * 45} className="entry">
        <div class="card hoverable">
          <header class="head">
            <div class="title-row">
              <h3>{@html ed.institution.replace(/\n/g, '<br>')}</h3>
              {#if ed.dateText}<span class="date">{ed.dateText}</span>{/if}
            </div>
          </header>
          {#if ed.details}
            <div class="details">
              {@html ed.details.replace(/\n/g, '<br>')}
            </div>
          {/if}
        </div>
      </Reveal>
    {/each}
  </div>
  {#if !items.length}
    <p>No education details found.</p>
  {/if}
</Section>

<style>
  .timeline { 
    display: grid; 
    gap: 1.75rem; 
  }
  :global(.entry) { position: relative; }

  .card { 
    background: var(--card); 
    border: 1px solid var(--border); 
    border-radius: 14px; 
    padding: 1.5rem; 
  }
  .hoverable { 
    transition: transform .2s ease, border-color .2s ease, box-shadow .2s ease; 
  }
  .hoverable:hover { 
    transform: translateY(-3px); 
    border-color: color-mix(in oklab, var(--accent) 35%, var(--border)); 
    box-shadow: 0 10px 26px color-mix(in oklab, var(--accent) 12%, transparent); 
  }

  .head { 
    display: grid; 
    gap: .35rem; 
  }
  .title-row { 
    display: grid; 
    grid-template-columns: 1fr auto; 
    align-items: baseline; 
    gap: .5rem; 
  }
  h3 { 
    margin: 0; 
    font-size: 1.08rem; 
    line-height: 1.3;
  }
  .date { 
    color: var(--muted-2); 
    font-size: 0.95rem; 
    white-space: nowrap; 
  }

  .details { 
    color: var(--muted); 
    margin: 0.6rem 0 0; 
    line-height: 1.5;
    font-size: 0.95rem;
  }

  @media (min-width: 780px) {
    .card { padding: 1.75rem 1.5rem; }
  }

  /* Mobile responsiveness */
  @media (max-width: 768px) {
    .title-row { 
      grid-template-columns: 1fr; 
      gap: 0.5rem; 
    }
    .date { 
      justify-self: start; 
      white-space: normal; 
    }
    .card { 
      padding: 1.25rem; 
    }
  }

  @media (max-width: 480px) {
    .card { 
      padding: 1rem; 
    }
    h3 { 
      font-size: 1rem; 
    }
    .details { 
      font-size: 0.9rem; 
    }
  }
</style>
