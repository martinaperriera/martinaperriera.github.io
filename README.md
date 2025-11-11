<html lang="en">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>Martina Perriera's Portfolio</title>

<!-- Fonts -->
<link href="https://fonts.googleapis.com/css2?family=Press+Start+2P&family=Space+Mono:wght@400;700&display=swap" rel="stylesheet">

<!-- Howler.js for sounds -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/howler/2.2.3/howler.min.js"></script>

<style>
  :root {
    /* Light mode */
    --bg: #f5f5f5;
    --text: #2d2d2d;
    --accent: #ff6b9d;
    --accent-2: #c44569;
    --muted: #666;
    --card-bg: #fff;
    --border: #e0e0e0;
    --shadow: rgba(0,0,0,0.1);
    --pixel-primary: #ff6b9d;
    --pixel-secondary: #ffd93d;
    --pixel-skin: #ffdbac;
    --bubble-bg: #fff;
    --bubble-border: #2d2d2d;
  }
  
  [data-theme="dark"] {
    --bg: #1a1a2e;
    --text: #eee;
    --accent: #00d4ff;
    --accent-2: #00a8cc;
    --muted: #aaa;
    --card-bg: #16213e;
    --border: #2d3561;
    --shadow: rgba(0,0,0,0.4);
    --pixel-primary: #00d4ff;
    --pixel-secondary: #ffd93d;
    --pixel-skin: #ffdbac;
    --bubble-bg: #16213e;
    --bubble-border: #00d4ff;
  }
  
  * { box-sizing: border-box; margin: 0; padding: 0; }
  
  body {
    font-family: 'Space Mono', monospace;
    background: var(--bg);
    color: var(--text);
    transition: background 0.3s, color 0.3s;
    min-height: 100vh;
    padding: 20px;
  }

.avatar-img {
  image-rendering: pixelated;
  background: transparent;
  display: block;
}
  
  /* Theme toggle */
  .theme-toggle {
    position: fixed;
    top: 20px;
    right: 20px;
    width: 60px;
    height: 60px;
    border-radius: 50%;
    background: var(--card-bg);
    border: 3px solid var(--border);
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 28px;
    transition: all 0.3s;
    z-index: 1000;
    box-shadow: 0 4px 15px var(--shadow);
  }
  
  .theme-toggle:hover {
    transform: scale(1.1) rotate(15deg);
    box-shadow: 0 6px 20px var(--shadow);
  }
  
  /* Container */
  .container {
    max-width: 900px;
    margin: 0 auto;
    text-align: center;
  }
  
  /* Start screen */
  .start-screen {
    min-height: 80vh;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: 30px;
  }
  
  .start-screen.hidden {
    display: none;
  }
  
  /* Pixel avatar */
  .pixel-avatar {
    width: 120px;
    height: 120px;
    display: grid;
    grid-template-columns: repeat(12, 1fr);
    grid-template-rows: repeat(12, 1fr);
    gap: 0;
    margin: 0 auto;
    image-rendering: pixelated;
    image-rendering: crisp-edges;
    background: transparent;
  }
  
  .pixel {
    width: 100%;
    height: 100%;
  }
  
  /* Speech bubble */
  .speech-bubble {
    position: relative;
    background: var(--bubble-bg);
    border: 3px solid var(--bubble-border);
    border-radius: 20px;
    padding: 25px 30px;
    max-width: 500px;
    box-shadow: 0 8px 25px var(--shadow);
    animation: float 3s ease-in-out infinite;
  }
  
  @keyframes float {
    0%, 100% { transform: translateY(0px); }
    50% { transform: translateY(-10px); }
  }
  
  .speech-bubble::after {
    content: '';
    position: absolute;
    bottom: -20px;
    left: 50%;
    transform: translateX(-50%);
    width: 0;
    height: 0;
    border-left: 15px solid transparent;
    border-right: 15px solid transparent;
    border-top: 20px solid var(--bubble-border);
  }
  
  .speech-bubble::before {
    content: '';
    position: absolute;
    bottom: -14px;
    left: 50%;
    transform: translateX(-50%);
    width: 0;
    height: 0;
    border-left: 12px solid transparent;
    border-right: 12px solid transparent;
    border-top: 17px solid var(--bubble-bg);
    z-index: 1;
  }
  
  .bubble-text {
    font-family: 'Press Start 2P', monospace;
    font-size: 14px;
    line-height: 1.8;
    color: var(--text);
  }
  
  /* Start button */
  .start-btn {
    font-family: 'Press Start 2P', monospace;
    font-size: 16px;
    padding: 20px 40px;
    background: var(--accent);
    color: #fff;
    border: 4px solid var(--accent-2);
    border-radius: 12px;
    cursor: pointer;
    transition: all 0.2s;
    box-shadow: 0 6px 0 var(--accent-2), 0 10px 20px var(--shadow);
    position: relative;
    top: 0;
  }
  
  .start-btn:hover {
    top: 3px;
    box-shadow: 0 3px 0 var(--accent-2), 0 6px 15px var(--shadow);
  }
  
  .start-btn:active {
    top: 6px;
    box-shadow: 0 0 0 var(--accent-2), 0 3px 10px var(--shadow);
  }
  
  /* Loading bar */
  .loading-container {
    width: 100%;
    max-width: 500px;
    display: none;
    flex-direction: column;
    gap: 15px;
    margin-top: 30px;
  }
  
  .loading-container.active {
    display: flex;
  }
  
  .loading-label {
    font-family: 'Press Start 2P', monospace;
    font-size: 12px;
    color: var(--accent);
  }
  
  .progress-bar {
    width: 100%;
    height: 40px;
    background: var(--card-bg);
    border: 4px solid var(--border);
    border-radius: 8px;
    overflow: hidden;
    box-shadow: inset 0 4px 8px var(--shadow);
    position: relative;
  }
  
  .progress-fill {
    height: 100%;
    width: 0%;
    background: linear-gradient(90deg, var(--accent), var(--accent-2));
    transition: width 0.3s;
    position: relative;
    overflow: hidden;
  }
  
  .progress-fill::after {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: linear-gradient(90deg, 
      transparent 0%, 
      rgba(255,255,255,0.3) 50%, 
      transparent 100%);
    animation: shimmer 1s infinite;
  }
  
  @keyframes shimmer {
    0% { transform: translateX(-100%); }
    100% { transform: translateX(100%); }
  }
  
  .progress-text {
    font-family: 'Press Start 2P', monospace;
    font-size: 14px;
    color: var(--accent);
  }
  
  /* Main content */
  .main-content {
    display: none;
    padding: 40px 20px;
  }
  
  .main-content.active {
    display: block;
    animation: fadeIn 0.6s;
  }
  
  @keyframes fadeIn {
    from { opacity: 0; transform: translateY(20px); }
    to { opacity: 1; transform: translateY(0); }
  }
  
  /* Header */
  .header {
    margin-bottom: 60px;
  }
  
  .name {
    font-family: 'Press Start 2P', monospace;
    font-size: 28px;
    color: var(--accent);
    margin-bottom: 15px;
  }
  
  .tagline {
    font-size: 16px;
    color: var(--muted);
    margin-bottom: 30px;
  }
  
  /* Navigation */
  .nav {
    display: flex;
    justify-content: center;
    gap: 20px;
    flex-wrap: wrap;
    margin-bottom: 50px;
  }
  
  .nav-btn {
    font-family: 'Press Start 2P', monospace;
    font-size: 12px;
    padding: 12px 24px;
    background: var(--card-bg);
    color: var(--text);
    border: 3px solid var(--border);
    border-radius: 8px;
    cursor: pointer;
    transition: all 0.2s;
  }
  
  .nav-btn:hover, .nav-btn.active {
    background: var(--accent);
    color: #fff;
    border-color: var(--accent-2);
    transform: translateY(-3px);
    box-shadow: 0 5px 15px var(--shadow);
  }
  
  /* Sections */
  .section {
    display: none;
    text-align: left;
  }
  
  .section.active {
    display: block;
    animation: fadeIn 0.5s;
  }
  
  .section-title {
    font-family: 'Press Start 2P', monospace;
    font-size: 20px;
    color: var(--accent);
    margin-bottom: 30px;
    text-align: center;
  }
  
  /* Projects grid */
  .projects-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: 25px;
    margin-top: 30px;
  }
  
  .project-card {
    background: var(--card-bg);
    border: 3px solid var(--border);
    border-radius: 12px;
    padding: 20px;
    transition: all 0.3s;
    box-shadow: 0 4px 10px var(--shadow);
  }
  
  .project-card:hover {
    transform: translateY(-5px);
    box-shadow: 0 8px 20px var(--shadow);
    border-color: var(--accent);
  }
  
  .project-title {
    font-family: 'Press Start 2P', monospace;
    font-size: 12px;
    color: var(--accent);
    margin-bottom: 15px;
    line-height: 1.6;
  }
  
  .project-desc {
    font-size: 14px;
    color: var(--muted);
    line-height: 1.6;
    margin-bottom: 15px;
  }
  
  .project-tags {
    display: flex;
    gap: 8px;
    flex-wrap: wrap;
    margin-top: 15px;
  }
  
  .tag {
    font-family: 'Press Start 2P', monospace;
    font-size: 9px;
    padding: 6px 12px;
    background: var(--accent);
    color: #fff;
    border-radius: 6px;
  }
  
  /* About section */
  .about-content {
    max-width: 700px;
    margin: 0 auto;
    text-align: center;
  }
  
  .bio {
    font-size: 16px;
    line-height: 1.8;
    color: var(--text);
    margin-bottom: 25px;
  }
  
  .skills-container {
    margin-top: 40px;
  }
  
  .skills-title {
    font-family: 'Press Start 2P', monospace;
    font-size: 14px;
    color: var(--accent);
    margin-bottom: 20px;
  }
  
  .skills-grid {
    display: flex;
    justify-content: center;
    gap: 12px;
    flex-wrap: wrap;
  }
  
  .skill-tag {
    font-family: 'Press Start 2P', monospace;
    font-size: 10px;
    padding: 10px 18px;
    background: var(--card-bg);
    color: var(--accent);
    border: 3px solid var(--border);
    border-radius: 8px;
  }
  
  /* Contact section */
  .contact-content {
    max-width: 600px;
    margin: 0 auto;
  }
  
  .contact-form {
    display: flex;
    flex-direction: column;
    gap: 20px;
    margin-top: 30px;
  }
  
  .form-input, .form-textarea {
    font-family: 'Space Mono', monospace;
    font-size: 14px;
    padding: 15px;
    background: var(--card-bg);
    color: var(--text);
    border: 3px solid var(--border);
    border-radius: 8px;
    transition: all 0.3s;
  }
  
  .form-input:focus, .form-textarea:focus {
    outline: none;
    border-color: var(--accent);
    box-shadow: 0 0 0 3px rgba(255, 107, 157, 0.1);
  }
  
  .form-textarea {
    min-height: 150px;
    resize: vertical;
  }
  
  .submit-btn {
    font-family: 'Press Start 2P', monospace;
    font-size: 14px;
    padding: 18px;
    background: var(--accent);
    color: #fff;
    border: 4px solid var(--accent-2);
    border-radius: 8px;
    cursor: pointer;
    transition: all 0.2s;
    box-shadow: 0 4px 0 var(--accent-2);
  }
  
  .submit-btn:hover {
    transform: translateY(-2px);
    box-shadow: 0 6px 0 var(--accent-2);
  }
  
  .submit-btn:active {
    transform: translateY(2px);
    box-shadow: 0 2px 0 var(--accent-2);
  }
  
  /* Footer */
  .footer {
    margin-top: 80px;
    padding: 30px;
    text-align: center;
    border-top: 3px solid var(--border);
  }
  
  .footer-links {
    display: flex;
    justify-content: center;
    gap: 30px;
    margin-top: 20px;
    flex-wrap: wrap;
  }
  
  .footer-link {
    font-family: 'Press Start 2P', monospace;
    font-size: 11px;
    color: var(--accent);
    text-decoration: none;
    transition: all 0.2s;
  }
  
  .footer-link:hover {
    color: var(--accent-2);
    transform: translateY(-2px);
  }
  
  /* Responsive */
  @media (max-width: 768px) {
    .bubble-text {
      font-size: 11px;
    }
    
    .name {
      font-size: 20px;
    }
    
    .projects-grid {
      grid-template-columns: 1fr;
    }
    
    .nav {
      gap: 10px;
    }
    
    .nav-btn {
      font-size: 10px;
      padding: 10px 18px;
    }
  }
</style>
</head>
<body>

<!-- Theme toggle -->
<div class="theme-toggle" id="themeToggle">
  <span id="themeIcon">🌙</span>
</div>

<div class="container">
  <!-- Start Screen -->
  <div class="start-screen" id="startScreen">

<img class="avatar-img" src="avatar-pix.png" alt="Avatar pixellato" width="128" height="128" />

    
    <!-- Speech Bubble -->
    <div class="speech-bubble">
      <div class="bubble-text">
        Ciao! Welcome to my AI-powered creative space. Ready to explore?
      </div>
    </div>
    
    <!-- Start Button -->
    <button class="start-btn" id="startBtn">START</button>
    
    <!-- Loading Bar -->
    <div class="loading-container" id="loadingContainer">
      <div class="loading-label">LOADING...</div>
      <div class="progress-bar">
        <div class="progress-fill" id="progressFill"></div>
      </div>
      <div class="progress-text" id="progressText">0%</div>
    </div>
  </div>
  
  <!-- Main Content -->
  <div class="main-content" id="mainContent">
    <div class="header">
      <h1 class="name">Martina Perriera</h1>
      <p class="tagline">AI enthusiast blending language, art, and technology.</p>
      
      <nav class="nav">
        <button class="nav-btn active" data-section="about">ABOUT</button>
        <button class="nav-btn" data-section="projects">PROJECTS</button>
        <button class="nav-btn" data-section="contact">CONTACT</button>
      </nav>
    </div>
    
    <!-- About Section -->
    <section id="about" class="section active">
      <h2 class="section-title">ABOUT ME</h2>
      <div class="about-content">
        <p class="bio">
          I am a language & data specialist combining a humanistic background with a growing technical toolkit. I work at the intersection of prompt design, content evaluation and creative AI experimentation. My work blends rigorous linguistic thinking with a passion for visual storytelling.
        </p>

        
        <div class="skills-container">
          <h3 class="skills-title">SKILLS & TOOLS</h3>
          <div class="skills-grid">
            <span class="skill-tag">PROMPT ENGINEERING</span>
            <span class="skill-tag">LLM EVALUATION</span>
            <span class="skill-tag">MIDJOURNEY</span>
            <span class="skill-tag">DALL·E</span>
            <span class="skill-tag">CANVA</span>
            <span class="skill-tag">PYTHON</span>
            <span class="skill-tag">COPYWRITING</span>
          </div>
        </div>
      </div>
    </section>
    
    <!-- Projects Section -->
    <section id="projects" class="section">
      <h2 class="section-title">PROJECTS</h2>
      <div class="projects-grid">
        <div class="project-card">
          <h3 class="project-title">Mindful Journals — AI Book Series</h3>
          <p class="project-desc">Prompt design and iterative refinement to generate cover art and low-content interior pages for a mindfulness journal series.</p>
          <div class="project-tags">
            <span class="tag">MIDJOURNEY</span>
            <span class="tag">CHATGPT</span>
          </div>
        </div>
        
        <div class="project-card">
          <h3 class="project-title">Prompt Engineering & Model Evaluation</h3>
          <p class="project-desc">Freelance evaluation and refinement of prompts for LLMs, focusing on clarity, instruction adherence and factual accuracy.</p>
          <div class="project-tags">
            <span class="tag">GPT</span>
            <span class="tag">ANNOTATION</span>
          </div>
        </div>
        
        <div class="project-card">
          <h3 class="project-title">AI x Cinema — Visual Tribute</h3>
          <p class="project-desc">Generative visual experiments inspired by European cinema; poster-style images combining poetic motifs and cinematic references.</p>
          <div class="project-tags">
            <span class="tag">DALL·E</span>
            <span class="tag">PHOTOSHOP</span>
          </div>
        </div>
        
        <div class="project-card">
          <h3 class="project-title">Social Visuals & Copy</h3>
          <p class="project-desc">AI-assisted social concepts combining generated visuals and copywriting to promote sustainable creative practices.</p>
          <div class="project-tags">
            <span class="tag">CHATGPT</span>
            <span class="tag">CANVA</span>
          </div>
        </div>
      </div>
    </section>
    
    <!-- About Section -->
    <section id="about" class="section">
      <h2 class="section-title">ABOUT ME</h2>
      <div class="about-content">
        <p class="bio">
          I am a language & data specialist combining a humanistic background with a growing technical toolkit. I work at the intersection of prompt design, content evaluation and creative AI experimentation. My work blends rigorous linguistic thinking with a passion for visual storytelling.
        </p>
        <p class="bio">
          Selected for the Schuman Traineeship Programme (European Parliament, Luxembourg, 2024). Experience in academic project coordination, festival volunteering (Cinema City Palermo) and international presentations (conference in Salamanca).
        </p>
        
        <div class="skills-container">
          <h3 class="skills-title">SKILLS & TOOLS</h3>
          <div class="skills-grid">
            <span class="skill-tag">PROMPT ENGINEERING</span>
            <span class="skill-tag">LLM EVALUATION</span>
            <span class="skill-tag">MIDJOURNEY</span>
            <span class="skill-tag">DALL·E</span>
            <span class="skill-tag">CANVA</span>
            <span class="skill-tag">PYTHON</span>
            <span class="skill-tag">COPYWRITING</span>
          </div>
        </div>
      </div>
    </section>
    
    <!-- Contact Section -->
    <section id="contact" class="section">
      <h2 class="section-title">GET IN TOUCH</h2>
      <div class="contact-content">
        <p class="bio">Interested in collaborating or want to see more work? Drop me a message!</p>
        <form class="contact-form" id="contactForm">
          <input type="text" class="form-input" placeholder="Your Name" id="nameInput" required>
          <input type="email" class="form-input" placeholder="Your Email" id="emailInput" required>
          <textarea class="form-textarea" placeholder="Your Message" id="messageInput" required></textarea>
          <button type="submit" class="submit-btn">SEND MESSAGE</button>
        </form>
      </div>
    </section>
    
    <!-- Footer -->
    <footer class="footer">
      <p style="color: var(--muted); font-size: 12px;">Based in Palermo, Italy 🇮🇹</p>
      <div class="footer-links">
        <a href="#" class="footer-link" id="cvLink">DOWNLOAD CV</a>
        <a href="https://linkedin.com/in/yourprofile" class="footer-link" target="_blank">LINKEDIN</a>
        <a href="mailto:your.email@example.com" class="footer-link">EMAIL</a>
      </div>
    </footer>
  </div>
</div>

<script>
/* ========= SOUNDS ========= */
const sounds = {
  boot: new Howl({ src: ['https://freesound.org/data/previews/524/524913_10382503-lq.mp3'], volume: 0.25 }),
  tick: new Howl({ src: ['https://freesound.org/data/previews/466/466238_10026710-lq.mp3'], volume: 0.18 }),
  click: new Howl({ src: ['https://freesound.org/data/previews/66/66112_634166-lq.mp3'], volume: 0.18 }),
  success: new Howl({ src: ['https://freesound.org/data/previews/331/331912_3248244-lq.mp3'], volume: 0.18 }),
};

let soundOn = true;

/* ========= THEME TOGGLE ========= */
const themeToggle = document.getElementById('themeToggle');
const themeIcon = document.getElementById('themeIcon');
let isDark = false;

themeToggle.addEventListener('click', () => {
  isDark = !isDark;
  document.documentElement.setAttribute('data-theme', isDark ? 'dark' : 'light');
  themeIcon.textContent = isDark ? '☀️' : '🌙';
  if (soundOn) sounds.click.play();
});

/* ========= START SEQUENCE ========= */
const startBtn = document.getElementById('startBtn');
const startScreen = document.getElementById('startScreen');
const loadingContainer = document.getElementById('loadingContainer');
const progressFill = document.getElementById('progressFill');
const progressText = document.getElementById('progressText');
const mainContent = document.getElementById('mainContent');

startBtn.addEventListener('click', () => {
  if (soundOn) sounds.click.play();
  
  startBtn.style.display = 'none';
  loadingContainer.classList.add('active');
  
  if (soundOn) sounds.boot.play();
  
  let progress = 0;
  const interval = setInterval(() => {
    progress += Math.random() * 15;
    if (progress > 100) progress = 100;
    
    progressFill.style.width = progress + '%';
    progressText.textContent = Math.floor(progress) + '%';
    
    if (soundOn && Math.random() > 0.7) sounds.tick.play();
    
    if (progress >= 100) {
      clearInterval(interval);
      setTimeout(() => {
        if (soundOn) sounds.success.play();
        startScreen.classList.add('hidden');
        mainContent.classList.add('active');
      }, 500);
    }
  }, 200);
});

/* ========= NAVIGATION ========= */
const navBtns = document.querySelectorAll('.nav-btn');
const sections = document.querySelectorAll('.section');

navBtns.forEach(btn => {
  btn.addEventListener('click', () => {
    if (soundOn) sounds.click.play();
    
    // Update active button
    navBtns.forEach(b => b.classList.remove('active'));
    btn.classList.add('active');
    
    // Show corresponding section
    const targetSection = btn.getAttribute('data-section');
    sections.forEach(section => {
      section.classList.remove('active');
      if (section.id === targetSection) {
        section.classList.add('active');
      }
    });
    
    // Smooth scroll to top
    window.scrollTo({ top: 0, behavior: 'smooth' });
  });
});

/* ========= CONTACT FORM ========= */
const contactForm = document.getElementById('contactForm');

contactForm.addEventListener('submit', (e) => {
  e.preventDefault();
  
  const name = document.getElementById('nameInput').value;
  if (soundOn) sounds.success.play();
  
  alert(`Thanks ${name}! Your message has been sent (demo). I'll get back to you soon! 🚀`);
  contactForm.reset();
});

/* ========= CV LINK ========= */
document.getElementById('cvLink').addEventListener('click', (e) => {
  e.preventDefault();
  if (soundOn) sounds.click.play();
  alert('CV download placeholder — replace with your actual CV file link.');
});

/* ========= KEYBOARD SHORTCUTS ========= */
document.addEventListener('keydown', (e) => {
  if (!startScreen.classList.contains('hidden')) return;
  
  if (e.key === '1') navBtns[0].click();
  if (e.key === '2') navBtns[1].click();
  if (e.key === '3') navBtns[2].click();
});
</script>
</body>
</html>
