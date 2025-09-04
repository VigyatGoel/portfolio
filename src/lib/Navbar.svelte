<script>
  const { data } = $props();
  const sections = [
    { id: 'home', label: 'Home' },
    { id: 'about', label: 'About' },
    { id: 'education', label: 'Education' },
    { id: 'experience', label: 'Experience' },
    { id: 'projects', label: 'Projects' },
    { id: 'skills', label: 'Skills' },
    { id: 'contact', label: 'Contact' },
  ];
  const links = $derived(data?.contact?.links || []);
  let open = $state(false);

  function scrollTo(id) {
    const el = document.getElementById(id);
    if (el) {
      el.scrollIntoView({ behavior: 'smooth', block: 'start' });
      open = false;
    }
  }

  let active = $state('home');
  function onScroll() {
    let current = 'home';
    for (const s of sections) {
      const el = document.getElementById(s.id);
      if (!el) continue;
      const rect = el.getBoundingClientRect();
      if (rect.top <= 120 && rect.bottom > 120) {
        current = s.id;
        break;
      }
    }
    active = current;
  }

  $effect(() => {
    window.addEventListener('scroll', onScroll, { passive: true });
    return () => window.removeEventListener('scroll', onScroll);
  });
</script>

<nav class="nav">
  <ul class:open={open}>
    {#each sections as s}
      <li>
        <a href={`#${s.id}`} class:active={active === s.id} onclick={(e) => { e.preventDefault(); scrollTo(s.id); }}>{s.label}</a>
      </li>
    {/each}
    <li class="social-links">
      {#each links as l}
        {#if /github\.com/i.test(l.url)}
          <a class="icon" href={l.url} target="_blank" rel="noreferrer noopener" aria-label="GitHub">
            <img src="/svg/GitHub.svg" alt="GitHub" width="24" height="24" />
          </a>
        {:else if /linkedin\.com/i.test(l.url)}
          <a class="icon" href={l.url} target="_blank" rel="noreferrer noopener" aria-label="LinkedIn">
            <img src="/svg/LinkedIn.svg" alt="LinkedIn" width="24" height="24" />
          </a>
        {/if}
      {/each}
    </li>
  </ul>

  <button class="hamburger" aria-label="Menu" onclick={() => (open = !open)}>
    <span class:open={open}></span>
  </button>
</nav>

<style>
  .nav {
    position: sticky;
    top: 0;
    z-index: 50;
    backdrop-filter: blur(8px);
    -webkit-backdrop-filter: blur(8px);
    background: color-mix(in oklab, var(--bg) 88%, transparent);
    border-bottom: 1px solid var(--border);
    display: flex;
    align-items: center;
    justify-content: flex-end;
    padding: 0.75rem var(--container-x);
  }

  ul { list-style: none; display: flex; gap: 0.75rem; align-items: center; margin: 0; padding: 0; }
  a { cursor: pointer; color: var(--muted); padding: 0.5rem 0.6rem; border-radius: 8px; position: relative; transition: color 200ms, background 200ms; }
  a:hover { color: var(--fg); background: var(--hover); }
  a.active { color: var(--fg); background: var(--hover); }

  .social-links { display: flex; gap: 0.5rem; }
  .icon { display: inline-flex; align-items: center; justify-content: center; width: 45px; height: 45px; border-radius: 999px; border: 1px solid var(--border); color: var(--fg); background: var(--hover); transition: transform .12s ease, background .25s ease, border-color .2s ease; }
  .icon img { width: 28px !important; height: 28px !important; object-fit: contain; }
  .icon img[alt="GitHub"] { filter: invert(1); }
  .icon:hover { transform: translateY(-2px); background: color-mix(in oklab, var(--accent) 15%, transparent); border-color: color-mix(in oklab, var(--accent) 35%, var(--border)); }

  .hamburger { display: none; background: transparent; border: none; }
  .hamburger span {
    position: relative; display: inline-block; width: 22px; height: 2px; background: var(--fg);
  }
  .hamburger span::before, .hamburger span::after { content: ''; position: absolute; left: 0; width: 22px; height: 2px; background: var(--fg); transition: transform .2s ease; }
  .hamburger span::before { top: -6px; }
  .hamburger span::after { top: 6px; }
  .hamburger span.open { background: transparent; }
  .hamburger span.open::before { transform: translateY(6px) rotate(45deg); }
  .hamburger span.open::after { transform: translateY(-6px) rotate(-45deg); }

  @media (max-width: 820px) {
    .hamburger { display: inline-flex; }
    ul { position: fixed; right: 1rem; top: 3.25rem; background: var(--bg); border: 1px solid var(--border); border-radius: 12px; padding: 0.5rem; display: none; flex-direction: column; gap: 0.25rem; }
    ul.open { display: flex; }
  }
</style>
