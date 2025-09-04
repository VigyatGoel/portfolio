<script>
  import Navbar from './lib/Navbar.svelte';
  import Hero from './lib/sections/Hero.svelte';
  import About from './lib/sections/About.svelte';
  import Skills from './lib/sections/Skills.svelte';
  import Projects from './lib/sections/Projects.svelte';
  import Experience from './lib/sections/Experience.svelte';
  import Education from './lib/sections/Education.svelte';
  import Contact from './lib/sections/Contact.svelte';

  // Hardcoded resume data (sourced from public/resume.md)
  let data = $state({
    name: 'Vigyat Goel',
    summary:
      'AI/ML student with a strong foundation in deep learning, backend development, and cloud infrastructure. Skilled in designing scalable systems, developing machine learning frameworks, and integrating advanced technologies into practical solutions. Passionate about exploring innovative tools, building efficient software, and bridging the gap between research and engineering.',
    about:
      'Hey! I\'m Vigyat, an AI/ML enthusiast who loves exploring how technology can solve real world problems. I\'m fascinated by intelligent systems, backend development, and cloud infrastructure, and I enjoy turning ideas into practical solutions.\n\nOutside of AI, I like experimenting with new tools, building side projects, and finding creative ways to make tech more accessible and impactful. For me, learning never stops whether it\'s diving into a new framework, exploring design concepts, or tinkering with code just for fun.',
    skills: [
      { category: 'Machine Learning & AI', items: ['PyTorch', 'TensorFlow', 'Scikit-learn', 'OpenCV', 'LangChain', 'Ollama'] },
      { category: 'Backend Development', items: ['FastAPI', 'Go', 'REST APIs', 'Deployment Pipelines'] },
      { category: 'DevOps & Cloud', items: ['Docker', 'GitHub Actions (CI/CD)', 'AWS', 'Google Cloud', 'Prometheus', 'Grafana'] },
      { category: 'Programming Languages', items: ['Python', 'Go', 'Java', 'C'] },
      { category: 'Databases', items: ['MySQL', 'MongoDB', 'SQLite'] },
      { category: 'Tools', items: ['Git', 'Postman'] },
      { category: 'Mobile Development (Secondary)', items: ['Android (Jetpack Compose, MVVM)', 'Firebase'] },
    ],
    projects: [
      {
        name: 'GoTorch - Deep Learning Library in Go',
        description:
          'Built a deep learning framework from scratch in Go supporting core neural network layers (Linear, Conv2D), optimizers (SGD, Adam), loss functions, and model serialization; includes a sequential API for training and persistence.',
        tech: ['Go', 'Gorgonia (Tensor)', 'Neural Network fundamentals'],
        github: 'https://github.com/VigyatGoel/GoTorch'
      },
      {
        name: 'Diabetic Retinopathy Detection',
        description:
          'Engineered a custom CNN architecture that outperformed established models (InceptionV3, EfficientNet, ResNet) in detecting Diabetic Retinopathy, achieving a 97% classification accuracy across five severity levels.',
        tech: ['Python', 'PyTorch', 'OpenCV', 'Scikit-learn'],
        github: 'https://github.com/VigyatGoel/Diabetic-Retinopathy-Detection'
      },
      {
        name: 'Vigyaan - ML & Data Science Platform',
        description:
          'Built a platform for rapid exploratory data analysis, interactive visualizations, and baseline ML model training from CSV inputs. Created end-to-end data ingestion, charting, and model inference workflows.',
        tech: ['FastAPI', 'Streamlit', 'Python', 'Pandas', 'NumPy', 'Matplotlib', 'Scikit-learn', 'CI/CD'],
        github: 'https://github.com/VigyatGoel/Vigyaan',
        website: 'https://vigyaan.onrender.com'
      },
      {
        name: 'Ollama Code CLI',
        description:
          'An interactive command-line AI agent that leverages local LLMs through Ollama for coding tasks with advanced tool calling features. Supports file operations, code execution, and conversational interactions with elegant terminal formatting.',
        tech: ['Python', 'Ollama', 'AI Agent', 'CLI', 'Rich', 'Click', 'Tool Calling'],
        github: 'https://github.com/VigyatGoel/ollama-code-cli'
      },
    ],
    experience: [
      {
        role: 'Research Intern',
        company: 'Defence Research and Development Organisation (DRDO)',
        location: undefined,
        dateText: 'June 2025 – July 2025',
        bullets: [
          'Engineered an air-gapped RAG Q&A system for secure PDF analysis using local LLMs, significantly reducing document analysis time.',
          'Managed the full pipeline from data preprocessing to prompt engineering.'
        ],
        tech: ['Python', 'Ollama', 'RAG', 'Gemma', 'Llama', 'PyPDF2', 'Prompt Engineering']
      },
      {
        role: 'Machine Learning & Backend Developer',
        company: 'Quamin Tech Solutions (Remote, Delhi)',
        location: undefined,
        dateText: 'Jan 2025 – Apr 2025',
        bullets: [
          'Developed and deployed backend APIs for ML model integration, improving model accuracy from 80% to 95%.',
          'Implemented CI/CD practices, managed cloud deployment and monitoring to enable scalable model serving.'
        ],
        tech: ['FastAPI', 'Docker', 'AWS', 'TensorFlow', 'Scikit-learn', 'LLM integration']
      },
      {
        role: 'Backend Developer Intern',
        company: 'DroidShift IT Solutions, Delhi',
        location: undefined,
        dateText: 'June 2024 – July 2024',
        bullets: [
          'Developed a backend API to reliably capture and store user event data, supporting the app’s core user tracking functionality.',
          'Integrated deployment pipelines to host the service on AWS EC2.'
        ],
        tech: ['FastAPI', 'Python', 'SQLite', 'MongoDB', 'AWS EC2']
      }
    ],
    education: [
      {
        institution: '<strong>B.Tech in Artificial Intelligence and Machine Learning</strong>',
        details:
          'University School of Automation and Robotics, Guru Gobind Singh Indraprastha University\nCGPA: 8.98',
        dateText: 'Nov 2022 – Aug 2026 (Expected)'
      },
      {
        institution: '<strong>Class XII (CBSE): PCM with Computer Science</strong>',
        details: 'Vivekanand School, Delhi\nPercentage: 90.4%',
        dateText: '2022'
      }
    ]
  });

  // Force dark mode always
  $effect(() => {
    const html = document.documentElement;
    html.classList.add('dark');
  });
</script>

<Navbar {data} />
<div class="container">
  <Hero {data} />
  <About {data} />
  <Education {data} />
  <Experience {data} />
  <Projects {data} />
  <Skills {data} />
  <Contact />
</div>

<style>
  :global(:root) {
    /* Dark theme tokens */
    --bg: oklch(17% 0.03 264);
    --card: oklch(21% 0.03 264);
    --hover: oklch(25% 0.03 264);
    --border: oklch(32% 0.03 264 / 0.5);
    --fg: oklch(92% 0.02 264);
    --muted: oklch(80% 0.02 264);
    --muted-2: oklch(72% 0.02 264);
    --accent: oklch(70% 0.21 29);
    --accent-700: oklch(60% 0.21 29);
    
    --container-x: clamp(1rem, 5vw, 2rem);
  }
  
  :global(html) { 
    scroll-behavior: smooth;
    color-scheme: dark;
  }
  
  :global(body) {
    background: var(--bg);
    color: var(--fg);
    margin: 0;
  }
  .container { max-width: 1100px; margin: 0 auto; padding: 0 var(--container-x); }
</style>
