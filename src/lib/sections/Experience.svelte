<script>
  import Section from '../ui/Section.svelte';
  import Reveal from '../ui/Reveal.svelte';
  const { data } = $props();
  const items = $derived(data?.experience || []);

  // Expand/collapse long bullet lists per item (mobile friendly)
  let expanded = $state({});
  function toggle(idx) {
    expanded = { ...expanded, [idx]: !expanded[idx] };
  }
</script>

<Section id="experience" title="Experience" description="I’ve gained practical exposure by working on real world problems, collaborating with teams, and building impactful solutions. These experiences have helped me strengthen my technical expertise, explore emerging technologies, and develop a strong problem solving mindset in professional environments.">
  <div class="timeline" aria-label="Experience timeline">
    {#each items as e, i}
      <Reveal as="article" direction="up" delay={i * 45} className="entry">
        <div class="card hoverable">
          <header class="head">
            <div class="title-row">
              <h3>{e.role}</h3>
              {#if e.dateText}<span class="date">{e.dateText}</span>{/if}
            </div>
            {#if e.company}
              <div class="meta">
                <span class="chip">{e.company}{#if e.location} • {e.location}{/if}</span>
              </div>
            {/if}
          </header>
          {#if e.bullets?.length}
            <ul class="bullets">
              {#each e.bullets as b, j}
                {#if expanded[i] || j < 2}<li>{b}</li>{/if}
              {/each}
            </ul>
            {#if e.bullets.length > 2}
              <button class="link-btn" type="button" onclick={() => toggle(i)}>
                {expanded[i] ? 'Show less' : 'Show more'}
              </button>
            {/if}
          {/if}
          {#if e.tech?.length}
            <div class="tags">{#each e.tech as t}<span class="tag">{t}</span>{/each}</div>
          {/if}
        </div>
      </Reveal>
    {/each}
  </div>
  {#if !items.length}
    <p>No experience listed.</p>
  {/if}
</Section>

<style>
  .timeline { 
    display: grid; 
    gap: 1.75rem; 
  }
  :global(.entry) { position: relative; }

  .card { background: var(--card); border: 1px solid var(--border); border-radius: 14px; padding: 1.5rem; }
  .hoverable { transition: transform .2s ease, border-color .2s ease, box-shadow .2s ease; }
  .hoverable:hover { transform: translateY(-3px); border-color: color-mix(in oklab, var(--accent) 35%, var(--border)); box-shadow: 0 10px 26px color-mix(in oklab, var(--accent) 12%, transparent); }

  .head { display: grid; gap: .35rem; }
  .title-row { display: grid; grid-template-columns: 1fr auto; align-items: baseline; gap: .5rem; }
  h3 { margin: 0; font-size: 1.08rem; }
  .date { color: var(--muted-2); font-size: 0.95rem; white-space: nowrap; }
  .meta { display: flex; gap: .5rem; align-items: center; }
  .chip { display: inline-flex; align-items: center; gap: .4rem; padding: .25rem .6rem; border-radius: 999px; background: color-mix(in oklab, var(--accent) 10%, transparent); border: 1px solid color-mix(in oklab, var(--accent) 30%, var(--border)); color: var(--fg); font-size: .88rem; }

  .bullets { margin: 0.4rem 0 0; padding-left: 1.1rem; }
  .bullets li { margin: 0.3rem 0; }
  .link-btn { margin-top: .25rem; background: transparent; border: none; color: var(--accent); font-weight: 700; letter-spacing: .2px; padding: .2rem 0; }
  .link-btn:hover { text-decoration: underline; }

  .tags { display: flex; gap: 0.5rem; flex-wrap: wrap; margin-top: 0.6rem; }
  .tag { background: var(--hover); border: 1px solid color-mix(in oklab, var(--accent) 25%, var(--border)); border-radius: 999px; padding: 0.28rem 0.6rem; font-size: 0.85rem; }

  @media (min-width: 780px) {
    .card { padding: 1.75rem 1.5rem; }
  }
</style>
