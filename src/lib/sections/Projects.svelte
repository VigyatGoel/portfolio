<script>
  import Section from '../ui/Section.svelte';
  import Reveal from '../ui/Reveal.svelte';
  const { data } = $props();
  const projects = $derived(data?.projects || []);
</script>

<Section id="projects" title="Projects" description="I’ve worked on a variety of projects spanning machine learning, backend development and cloud computing. Each project reflects my passion for building practical solutions, experimenting with new ideas, and turning those ideas into real world applications.">
  <div class="list">
    {#each projects as p, i}
      <Reveal as="div" direction="up" delay={i * 40}>
        <article class="card card-hover">
          <div class="card-head">
            <h3>{p.name}</h3>
            <div class="card-actions">
              {#if p.website}
                <a href={p.website} target="_blank" rel="noopener noreferrer" class="website-link" aria-label="Visit website">
                  <svg viewBox="0 0 24 24" width="30" height="30" fill="currentColor">
                    <path d="M14 3v2h3.59l-9.83 9.83 1.41 1.41L19 6.41V10h2V3h-7z"/>
                    <path d="M19 19H5V5h7V3H5a2 2 0 0 0-2 2v14a2 2 0 0 0 2 2h14a2 2 0 0 0 2-2v-7h-2v7z"/>
                  </svg>
                </a>
              {/if}
              {#if p.github}
                <a href={p.github} target="_blank" rel="noopener noreferrer" class="github-link" aria-label="View on GitHub">
                  <svg viewBox="0 0 24 24" width="30" height="30" fill="currentColor">
                    <path d="M12 2C6.477 2 2 6.484 2 12.017c0 4.425 2.865 8.18 6.839 9.504.5.092.682-.217.682-.483 0-.237-.008-.868-.013-1.703-2.782.605-3.369-1.343-3.369-1.343-.454-1.158-1.11-1.466-1.11-1.466-.908-.62.069-.608.069-.608 1.003.07 1.531 1.032 1.531 1.032.892 1.53 2.341 1.088 2.91.832.092-.647.35-1.088.636-1.338-2.22-.253-4.555-1.113-4.555-4.951 0-1.093.39-1.988 1.029-2.688-.103-.253-.446-1.272.098-2.65 0 0 .84-.27 2.75 1.026A9.564 9.564 0 0112 6.844c.85.004 1.705.115 2.504.337 1.909-1.296 2.747-1.027 2.747-1.027.546 1.379.202 2.398.1 2.651.64.7 1.028 1.595 1.028 2.688 0 3.848-2.339 4.695-4.566 4.943.359.309.678.92.678 1.855 0 1.338-.012 2.419-.012 2.747 0 .268.18.58.688.482A10.019 10.019 0 0022 12.017C22 6.484 17.522 2 12 2z"/>
                  </svg>
                </a>
              {/if}
            </div>
          </div>
          <p class="desc">{p.description}</p>
          {#if p.tech?.length}
            <div class="tags">
              {#each p.tech as t}<span class="tag">{t}</span>{/each}
            </div>
          {/if}
        </article>
      </Reveal>
    {/each}
  </div>
  {#if !projects.length}
    <p>No projects listed.</p>
  {/if}
</Section>

<style>
  .list { display: grid; gap: 1rem; }
  .card { position: relative; background: var(--card); border: 1px solid var(--border); border-radius: 14px; padding: 1rem; display: grid; gap: .6rem; min-height: 220px; }
  .card::after { content: ''; position: absolute; inset: 0; border-radius: inherit; pointer-events: none; background: radial-gradient(60% 60% at 20% 0%, color-mix(in oklab, var(--accent) 12%, transparent), transparent 60%); opacity: .65; }
  .card-hover { transition: transform .2s ease, box-shadow .2s ease, border-color .2s ease; }
  .card-hover:hover { transform: translateY(-4px); box-shadow: 0 10px 26px color-mix(in oklab, var(--accent) 14%, transparent); border-color: color-mix(in oklab, var(--accent) 40%, var(--border)); }

  .card-head { display: grid; grid-template-columns: 1fr auto; align-items: center; gap: .5rem; }
  h3 { margin: 0; font-size: 1.05rem; }
  .card-actions { display: flex; align-items: center; gap: 0.5rem; }
  .website-link,
  .github-link { 
    display: grid; 
    place-items: center; 
    width: 40px; 
    height: 40px; 
    border-radius: 8px; 
    color: var(--muted); 
    transition: color .2s ease, background .2s ease; 
  }
  .website-link:hover,
  .github-link:hover { 
    color: var(--fg); 
    background: var(--hover); 
  }

  .desc { color: var(--muted); margin: 0; display: -webkit-box; -webkit-line-clamp: 4; line-clamp: 4; -webkit-box-orient: vertical; overflow: hidden; }
  .tags { display: flex; gap: 0.5rem; flex-wrap: wrap; margin-top: auto; }
  .tag { background: var(--hover); border: 1px solid color-mix(in oklab, var(--accent) 25%, var(--border)); border-radius: 999px; padding: 0.25rem 0.6rem; font-size: 0.85rem; }

</style>
