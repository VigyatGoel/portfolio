<script>
  import Section from '../ui/Section.svelte';
  import Reveal from '../ui/Reveal.svelte';
  import TechIcon from '../ui/TechIcon.svelte';
  
  const { data } = $props();
  const skills = $derived(data?.skills || []);
</script>

<Section id="skills" title="Skills" description="I have built a diverse skill set through hands on experience and self driven learning. My expertise spans machine learning, backend development, and cloud computing, with several projects demonstrating my practical knowledge in these areas.">
  <div class="skills-container">
    {#each skills as group, i}
      <Reveal as="div" direction="up" delay={i * 40}>
        <div class="skill-category">
          <h3>{group.category}</h3>
          <div class="skill-grid">
            {#each group.items as item}
              <div class="skill-card">
                <div class="skill-icon" class:aws-icon={item === 'AWS'}>
                  <TechIcon name={item} size={36} />
                </div>
                <span class="skill-name">{item}</span>
              </div>
            {/each}
          </div>
        </div>
      </Reveal>
    {/each}
  </div>
  {#if !skills.length}
    <p>No skills found.</p>
  {/if}
</Section>

<style>
  .skills-container {
    display: flex;
    flex-direction: column;
    gap: 2rem;
  }

  .skill-category {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 16px;
    padding: 1.5rem;
    transition: transform 0.2s ease, box-shadow 0.2s ease, border-color 0.2s ease;
  }

  .skill-category:hover {
    transform: translateY(-3px);
    box-shadow: 0 10px 26px color-mix(in oklab, var(--accent) 12%, transparent);
    border-color: color-mix(in oklab, var(--accent) 35%, var(--border));
  }

  h3 {
    margin: 0 0 1rem;
    font-size: 1.2rem;
    color: var(--accent);
  }

  .skill-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(160px, 1fr));
    gap: 1.25rem;
  }

  .skill-card {
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 1rem;
    background: color-mix(in oklab, var(--card) 50%, var(--bg));
    border-radius: 12px;
    border: 1px solid var(--border);
  }

  .skill-icon {
    width: 64px;
    height: 64px;
    display: flex;
    align-items: center;
    justify-content: center;
    background: color-mix(in oklab, var(--accent) 8%, transparent);
    border-radius: 16px;
    margin-bottom: 1rem;
    color: var(--accent);
  }

  .skill-name {
    font-weight: 600;
    font-size: 0.95rem;
    text-align: center;
    line-height: 1.3;
  }

  @media (max-width: 768px) {
    .skill-grid {
      grid-template-columns: repeat(auto-fill, minmax(140px, 1fr));
      gap: 1rem;
    }
    .skill-category {
      padding: 1.25rem;
    }
  }

  @media (max-width: 480px) {
    .skill-grid {
      grid-template-columns: repeat(auto-fill, minmax(120px, 1fr));
      gap: 0.75rem;
    }
    .skill-category {
      padding: 1rem;
    }
    .skill-card {
      padding: 0.75rem;
    }
    .skill-icon {
      width: 48px;
      height: 48px;
      margin-bottom: 0.75rem;
    }
    .skill-name {
      font-size: 0.85rem;
    }
  }
</style>
