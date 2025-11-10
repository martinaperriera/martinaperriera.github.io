<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>AI Arcade Portfolio</title>
  <link href="https://unpkg.com/nes.css/css/nes.min.css" rel="stylesheet" />
  <style>
    body {
      background-color: #000;
      color: #00ff99;
      font-family: 'Press Start 2P', monospace;
      text-align: center;
      margin: 0;
      padding: 40px;
    }
    .screen {
      border: 3px solid #00ff99;
      padding: 20px;
      max-width: 700px;
      margin: auto;
      background-color: #111;
    }
    .btn {
      margin: 10px;
      background: none;
      color: #00ff99;
      border: 2px solid #00ff99;
      padding: 10px 20px;
      cursor: pointer;
      transition: 0.3s;
    }
    .btn:hover { background-color: #00ff99; color: #111; }
  </style>
</head>
<body>
  <div class="screen">
    <h2>🕹️ Welcome to AI Arcade</h2>
    <p id="text"></p>
    <button class="btn" onclick="showProjects()">View Projects</button>
    <button class="btn" onclick="showAbout()">About Me</button>
    <button class="btn" onclick="showContact()">Contact</button>
  </div>

  <script src="https://cdn.jsdelivr.net/npm/typed.js@2.0.12"></script>
  <script>
    new Typed('#text', {
      strings: [
        '> Initializing portfolio.exe...',
        '> Loading creativity protocols...',
        '> Press any button to continue.'
      ],
      typeSpeed: 40,
      backSpeed: 0,
      loop: false
    });

    function showProjects() {
      document.querySelector('.screen').innerHTML = `
        <h2>🎨 Projects</h2>
        <p>> Mindful Journals – AI-Generated Books</p>
        <p>> Prompt Engineering & Evaluation</p>
        <p>> AI Visual Storytelling Experiments</p>
        <button class="btn" onclick="location.reload()">⬅️ Back</button>
      `;
    }

    function showAbout() {
      document.querySelector('.screen').innerHTML = `
        <h2>👩‍💻 About Me</h2>
        <p>> AI enthusiast blending language, art, and technology.</p>
        <p>> Passionate about digital creativity and prompt design.</p>
        <button class="btn" onclick="location.reload()">⬅️ Back</button>
      `;
    }

    function showContact() {
      document.querySelector('.screen').innerHTML = `
        <h2>📡 Contact</h2>
        <p>> Connect on LinkedIn: <a href="https://linkedin.com/in/yourprofile" target="_blank">here</a></p>
        <p>> Email: yourname@email.com</p>
        <button class="btn" onclick="location.reload()">⬅️ Back</button>
      `;
    }
  </script>
</body>
</html>
