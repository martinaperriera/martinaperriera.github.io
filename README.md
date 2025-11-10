<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>AI Arcade Portfolio – [Your Name]</title>
  <link href="https://unpkg.com/nes.css/css/nes.min.css" rel="stylesheet" />
  <style>
    @import url('https://fonts.googleapis.com/css2?family=Press+Start+2P&display=swap');

    body {
      margin: 0;
      padding: 0;
      background: #000;
      color: #0f0;
      font-family: 'Press Start 2P', monospace;
      text-align: center;
      overflow-x: hidden;
    }
    .container {
      max-width: 800px;
      margin: auto;
      padding: 20px;
    }
    header {
      margin-top: 60px;
      animation: fadeIn 2s ease-in-out;
    }
    header h1 {
      font-size: 2em;
      color: #0f0;
    }
    header p {
      color: #0a0;
      font-size: 1em;
    }
    nav {
      margin: 40px 0;
    }
    .btn {
      display: inline-block;
      margin: 10px;
      padding: 10px 20px;
      color: #0f0;
      border: 2px solid #0f0;
      background: transparent;
      cursor: pointer;
      transition: 0.3s;
    }
    .btn:hover {
      background: #0f0;
      color: #000;
    }
    .screen {
      border: 3px solid #0f0;
      padding: 30px;
      background: #111;
      min-height: 300px;
      animation: slideIn 0.5s ease-in-out;
    }
    @keyframes fadeIn {
      from { opacity: 0; }
      to { opacity: 1; }
    }
    @keyframes slideIn {
      from { transform: translateY(50px); opacity: 0; }
      to { transform: translateY(0); opacity: 1; }
    }
    .project-card {
      margin: 20px 0;
      padding: 15px;
      border: 1px solid #0f0;
    }
    .project-card img {
      max-width: 100%;
      height: auto;
      border: 1px solid #0f0;
      margin-top: 10px;
    }
    footer {
      margin: 60px 0;
      color: #0a0;
      font-size: 0.8em;
    }
    a {
      color: #0f0;
      text-decoration: none;
    }
    a:hover {
      text-decoration: underline;
    }
  </style>
</head>
<body>
  <div class="container">
    <header>
      <h1>AI Arcade Portfolio</h1>
      <p>Exploring the intersection of language, creativity & artificial intelligence</p>
    </header>
    <nav>
      <button class="btn" onclick="showSection('projects')">→ Projects</button>
      <button class="btn" onclick="showSection('about')">→ About Me</button>
      <button class="btn" onclick="showSection('contact')">→ Contact</button>
    </nav>
    <div id="content" class="screen">
      <h2>Welcome Player 1</h2>
      <p>Select a section to begin your journey...</p>
    </div>
    <footer>
      © [Your Name] - 2025 | Based in Palermo | Designed with ❤️ using AI
    </footer>
  </div>

  <script>
    function showSection(section) {
      const content = document.getElementById('content');
      if (section === 'projects') {
        content.innerHTML = `
          <h2>🎮 Projects</h2>
          <div class="project-card">
            <h3>Mindful Journals – AI-Generated Books</h3>
            <p>Tools: ChatGPT, Midjourney, Canva</p>
            <img src="journal-cover1.jpg" alt="Journal Cover 1">
            <img src="journal-cover2.jpg" alt="Journal Cover 2">
            <p>Designed and refined prompts to produce a series of journals combining textual and visual coherence.</p>
          </div>
          <div class="project-card">
            <h3>Prompt Engineering & Model Evaluation</h3>
            <p>Tools: GPT-4, internal evaluation frameworks</p>
            <img src="diagram-flow.png" alt="Prompt Flow Diagram">
            <img src="output-comparison.png" alt="Model Output Comparison">
            <p>Created, tested and evaluated prompts for large language models focusing on clarity, accuracy, and instruction adherence.</p>
          </div>
          <div class="project-card">
            <h3>AI x Cinema – Visual Tribute Project</h3>
            <p>Tools: DALL·E, Photoshop</p>
            <img src="cinema-poster1.jpg" alt="AI Cinema Poster 1">
            <img src="cinema-poster2.jpg" alt="AI Cinema Poster 2">
            <p>Generative visual experiment inspired by European cinema and storytelling through AI-generated imagery.</p>
          </div>
          <button class="btn" onclick="showSection('main')">⬅️ Back</button>
        `;
      } else if (section === 'about') {
        content.innerHTML = `
          <h2>👤 About Me</h2>
          <p>I am a language and data specialist passionate about the creative potential of AI. My experience spans prompt design, data annotation, and digital content creation. I hold a Master’s in Languages & Intercultural Studies and have worked on international projects blending technology and communication.</p>
          <button class="btn" onclick="showSection('main')">⬅️ Back</button>
        `;
      } else if (section === 'contact') {
        content.innerHTML = `
          <h2>📩 Contact</h2>
          <p>📍 Based in Palermo, Italy</p>
          <p>📧 your.email@example.com</p>
          <p>🔗 <a href="https://linkedin.com/in/yourprofile" target="_blank">LinkedIn Profile</a></p>
          <button class="btn" onclick="showSection('main')">⬅️ Back</button>
        `;
      } else {
        content.innerHTML = `
          <h2>Welcome Player 1</h2>
          <p>Select a section to begin your journey...</p>
        `;
      }
    }
  </script>
</body>
</html>
