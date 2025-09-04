<script>
  const { name, size = 40, class: className = '' } = $props();
  
  const iconMapping = {
    'PyTorch': 'PyTorch.svg',
    'TensorFlow': 'TensorFlow.svg',
    'Scikit-learn': 'scikit-learn.svg',
    'OpenCV': 'OpenCV.svg',
    'LangChain': 'Langchain.svg',
    'Ollama': 'ollama.svg',
    'FastAPI': 'FastAPI.svg',
    'Go': 'Go.svg',
    'REST APIs': 'OpenAPI.svg',
    'Deployment Pipelines': 'GitHub-Actions.svg',
    'Docker': 'Docker.svg',
    'GitHub Actions (CI/CD)': 'GitHub-Actions.svg',
    'AWS': 'AWS.svg',
    'Google Cloud': 'Google-Cloud.svg',
    'Prometheus': 'Prometheus.svg',
    'Grafana': 'Grafana.svg',
    'Python': 'Python.svg',
    'Java': 'Java.svg',
    'C': 'C.svg',
    'MySQL': 'MySQL.svg',
    'MongoDB': 'MongoDB.svg',
    'SQLite': 'SQLite.svg',
    'Git': 'Git.svg',
    'Postman': 'Postman.svg',
    'Android (Jetpack Compose, MVVM)': 'Android.svg',
    'Firebase': 'Firebase.svg'
  };
  
  const iconPath = $derived(`svg/${iconMapping[name] || 'Devicon.svg'}`);
  
  const shouldInvert = $derived(['Ollama', 'LangChain'].includes(name));
</script>

<div 
  class="tech-icon {className}" 
  style:width="{size}px" 
  style:height="{size}px"
>
  <img 
    src={iconPath} 
    alt={name} 
    class:invert={shouldInvert}
  />
</div>

<style>
  .tech-icon {
    display: inline-flex;
    align-items: center;
    justify-content: center;
    filter: drop-shadow(0 2px 4px rgba(0, 0, 0, 0.1));
  }
  
  .tech-icon img {
    width: 100%;
    height: 100%;
    object-fit: contain;
  }
  
  .tech-icon img.invert {
    filter: invert(1) brightness(1);
  }
</style>