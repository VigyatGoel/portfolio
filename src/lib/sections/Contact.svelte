<script>
  import Section from '../ui/Section.svelte';
  import Reveal from '../ui/Reveal.svelte';
  import emailjs from '@emailjs/browser';
  
  let name = $state('');
  let message = $state('');
  let email = $state('');
  let isLoading = $state(false);
  let status = $state('');

  // EmailJS configuration from environment variables
  const SERVICE_ID = import.meta.env.VITE_EMAILJS_SERVICE_ID;
  const TEMPLATE_ID = import.meta.env.VITE_EMAILJS_TEMPLATE_ID;
  const PUBLIC_KEY = import.meta.env.VITE_EMAILJS_PUBLIC_KEY;

  async function sendEmail(e) {
    e.preventDefault();
    
    if (!name || !email || !message) {
      status = 'Please fill in all fields';
      return;
    }

    isLoading = true;
    status = '';

    try {
      const templateParams = {
        from_name: name,
        from_email: email,
        message: message,
        to_name: 'Vigyat Goel',
      };

      await emailjs.send(SERVICE_ID, TEMPLATE_ID, templateParams, PUBLIC_KEY);
      
      status = 'Message sent successfully!';
      name = '';
      email = '';
      message = '';
    } catch (error) {
      console.error('EmailJS error:', error);
      status = 'Failed to send message. Please try again.';
    } finally {
      isLoading = false;
    }
  }
</script>

<Section id="contact" title="Contact" description="Let's connect! Feel free to reach out for collaborations, opportunities, or just to say hello.">
  <div class="contact-form">
    <Reveal as="div" direction="up">
      <form class="card" onsubmit={sendEmail}>
        <label>
          Name
          <input placeholder="Your name" bind:value={name} required />
        </label>
        <label>
          Email
          <input type="email" placeholder="Your email" bind:value={email} required />
        </label>
        <label>
          Message
          <textarea rows="4" placeholder="Write your message..." bind:value={message} required></textarea>
        </label>
        {#if status}
          <div class="status" class:success={status.includes('success')} class:error={!status.includes('success')}>
            {status}
          </div>
        {/if}
        <button class="primary" type="submit" disabled={isLoading}>
          {isLoading ? 'Sending...' : 'Send Message'}
        </button>
      </form>
    </Reveal>
  </div>
</Section>

<style>
  .contact-form { max-width: 900px; margin: 0 auto; width: 60%; }
  .card { background: var(--card); border: 1px solid var(--border); border-radius: 12px; padding: 2rem; display: grid; gap: 0.75rem; transition: transform .18s ease, border-color .18s ease, box-shadow .18s ease; }
  .card:hover { transform: translateY(-3px); border-color: color-mix(in oklab, var(--accent) 35%, var(--border)); box-shadow: 0 8px 20px color-mix(in oklab, var(--accent) 10%, transparent); }
  input, textarea { width: 100%; background: var(--hover); border: 1px solid var(--border); color: var(--fg); border-radius: 8px; padding: 0.6rem; font-size: 0.9rem; }
  label { display: grid; gap: 0.35rem; font-size: 1rem; }
  .primary { background: var(--accent); color: black; border: 1px solid var(--accent-700); border-radius: 10px; padding: 0.6rem 0.9rem; font-weight: 600; font-size: 1rem; }
  .primary:disabled { opacity: 0.6; cursor: not-allowed; }
  .status { padding: 0.5rem; border-radius: 8px; text-align: center; font-size: 0.9rem; }
  .status.success { background: color-mix(in oklab, green 20%, transparent); color: green; border: 1px solid green; }
  .status.error { background: color-mix(in oklab, red 20%, transparent); color: red; border: 1px solid red; }

  :global(#contact .section-description) {
    text-align: center;
  }
</style>
