<script>
  import Reveal from '../ui/Reveal.svelte';
  const { data } = $props();
  const name = $derived(data?.name || '');
  const summary = $derived(data?.summary || '');

  function toResume() {
    window.open('Vigyat_Resume.pdf', '_blank', 'noopener');
  }
</script>

<section id="home" class="hero">
  <!-- Subtle animated accents -->
  <div class="bg-accents" aria-hidden="true"></div>
  <div class="content">
    <Reveal as="div" direction="up">
      <h1 class="title">
        <span class="hello">Hi, I'm</span>
        <span class="grad anim-grad">{name}</span>
      </h1>
    </Reveal>
    <Reveal as="div" direction="up" delay={50}>
      <p class="subtitle">{summary}</p>
    </Reveal>
    <Reveal as="div" direction="up" delay={75}>
      <div class="actions">
        <button class="secondary" type="button" onclick={toResume}>View Résumé</button>
      </div>
    </Reveal>
  </div>
</section>

<style>
  .hero { padding: clamp(3rem, 12vw, 6rem) 0; position: relative; min-height: 100vh; display: grid; place-items: center; }
  .bg-accents { position: absolute; inset: 0; pointer-events: none; z-index: 0; }
  .bg-accents::before,
  .bg-accents::after {
    content: '';
    position: absolute;
    inset: 0;
    pointer-events: none;
  }
  /* Top glow */
  .bg-accents::before {
    background: radial-gradient(60% 50% at 50% 0%, color-mix(in oklab, var(--accent) 22%, transparent) 0%, transparent 70%);
    filter: blur(18px);
    opacity: 0.9;
    transform: translateZ(0);
  }
  /* Soft sheen */
  .bg-accents::after {
    background:
      linear-gradient(transparent 40%, color-mix(in oklab, var(--accent) 18%, transparent) 120%) top/100% 200% no-repeat;
    mask: linear-gradient(to bottom, black 0%, black 50%, transparent 100%);
    animation: sheen 8s linear infinite;
    opacity: .65;
  }
  @keyframes sheen { to { background-position: top, 0 0, 0 0; } from { background-position: bottom, 0 0, 0 0; } }

  .content { position: relative; z-index: 1; max-width: 900px; margin: 0 auto; text-align: center; padding: 0 1rem; }
  .title { font-size: clamp(2.5rem, 8vw, 5rem); margin: 0 0 .25rem; letter-spacing: 0.3px; font-weight: 800; }
  .hello { display: block; font-size: clamp(1rem, 3.5vw, 1.4rem); color: var(--muted-2); margin-bottom: .2rem; }
  .grad { background: linear-gradient(92deg, var(--fg), var(--accent)); -webkit-background-clip: text; background-clip: text; color: transparent; filter: drop-shadow(0 6px 18px color-mix(in oklab, var(--accent) 25%, transparent)); }
  .anim-grad { background-size: 200% 200%; animation: pan 6s ease-in-out infinite; }
  @keyframes pan { 0%,100% { background-position: 0% 50%; } 50% { background-position: 100% 50%; } }

  .subtitle { color: var(--muted); font-size: clamp(1rem, 3vw, 1.2rem); margin: .2rem auto 0; max-width: 65ch; text-align: justify; line-height: 1.7; }
  .actions { margin-top: 2rem; display: flex; justify-content: center; }
  .secondary { 
    background: color-mix(in oklab, var(--accent) 12%, transparent); 
    color: var(--fg); 
    border: 1px solid color-mix(in oklab, var(--accent) 35%, var(--border)); 
    font-size: 1.1em; 
    padding: 0.8rem 2rem; 
  }
  button { border-radius: 999px; padding: 0.7rem 1rem; font-weight: 700; letter-spacing: .2px; transition: transform .12s ease, background .2s ease, box-shadow .2s ease; }
  button:hover { transform: translateY(-1px); box-shadow: 0 8px 28px -12px color-mix(in oklab, var(--accent) 45%, transparent); }
  button:active { transform: translateY(0); }

  @media (prefers-reduced-motion: reduce) {
    :global(.reveal) { opacity: 1; transform: none; transition: none; }
    .anim-grad, .bg-accents::after { animation: none; }
  }
</style>
