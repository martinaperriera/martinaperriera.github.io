<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>AI Arcade Portfolio — [Your Name]</title>

<!-- Fonts & icons -->
<link href="https://fonts.googleapis.com/css2?family=Press+Start+2P&family=Inter:wght@300;400;600&display=swap" rel="stylesheet">

<!-- Howler.js for sounds -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/howler/2.2.3/howler.min.js"></script>
<!-- Typed.js for typing effect -->
<script src="https://cdn.jsdelivr.net/npm/typed.js@2.0.12"></script>

<style>
  :root{
    --bg:#030305;
    --screen:#071018;
    --accent:#00ff99;
    --accent-2:#00d1ff;
    --muted:#99ffcc;
    --card:#0b1020;
    --glass: rgba(255,255,255,0.03);
    --mono: 'Press Start 2P', monospace;
    --ui: 'Inter', system-ui, sans-serif;
  }
  /* Basic reset */
  *{box-sizing:border-box}
  html,body{height:100%;margin:0;background:linear-gradient(180deg,#000 0%, #06050a 70%);color:var(--accent);font-family:var(--ui);-webkit-font-smoothing:antialiased}
  a{color:var(--accent-2);text-decoration:none}
  /* Center frame */
  .frame{
    max-width:1100px;
    margin:30px auto;
    padding:28px;
    border:2px solid rgba(0,255,153,0.06);
    background: radial-gradient(1200px 600px at 10% 10%, rgba(0,209,255,0.02), transparent 10%), linear-gradient(180deg, rgba(255,255,255,0.02), transparent);
    box-shadow: 0 8px 30px rgba(0,0,0,0.6);
    border-radius:12px;
  }

  /* Top header */
  header{display:flex;align-items:center;gap:20px;justify-content:space-between;margin-bottom:22px}
  .logo{display:flex;gap:12px;align-items:center}
  .logo .badge{width:60px;height:60px;background:linear-gradient(135deg,var(--accent),var(--accent-2));border-radius:8px;display:flex;align-items:center;justify-content:center;color:#001; font-family:var(--mono);font-weight:700}
  .logo h1{font-family:var(--mono);font-size:14px;margin:0;color:var(--accent)}
  .logo p{margin:0;font-size:12px;color:var(--muted)}

  /* screen area */
  .screen{
    background: linear-gradient(180deg, rgba(0,0,0,0.35), rgba(6,7,10,0.55));
    border-radius:10px;
    padding:34px;
    min-height:520px;
    position:relative;
    overflow:hidden;
  }

  /* Start overlay */
  .start-overlay{
    position:absolute;inset:0;display:flex;flex-direction:column;align-items:center;justify-content:center;background:linear-gradient(180deg, rgba(0,0,0,0.6), rgba(0,0,0,0.45));backdrop-filter: blur(2px);z-index:20;
  }
  .title{
    font-family:var(--mono);
    font-size:18px;
    letter-spacing:1px;
    color:var(--accent-2);
    margin-bottom:18px;
    text-shadow:0 0 8px rgba(0,255,153,0.08);
  }
  .typed-box{color:var(--muted);font-family:var(--ui);max-width:720px;padding:0 12px;margin-bottom:20px;font-size:13px;line-height:1.5}
  .start-btn{
    font-family:var(--mono);
    background:transparent;
    color:var(--accent);
    border:2px solid var(--accent);
    padding:14px 22px;border-radius:8px;
    cursor:pointer; transition:all .18s ease; box-shadow: 0 6px 18px rgba(0,255,153,0.04)
  }
  .start-btn:hover{transform:translateY(-3px);box-shadow: 0 14px 30px rgba(0,255,153,0.08);background:var(--accent);color:#011}

  /* Loading bar retro */
  .loading-wrap{margin-top:24px;width:420px;border:2px solid rgba(0,255,153,0.06);padding:6px;border-radius:8px;background:var(--glass);display:flex;flex-direction:column;gap:8px;align-items:center}
  .bar{
    width:100%;height:12px;background:#000;border:1px solid rgba(0,255,153,0.06);border-radius:4px;overflow:hidden;position:relative;
  }
  .bar-inner{height:100%;width:0;background:linear-gradient(90deg,var(--accent),var(--accent-2));box-shadow:0 4px 10px rgba(0,209,255,0.06)}
  .bar-perc{font-family:var(--mono);font-size:11px;color:var(--muted);}

  /* main nav */
  .nav{
    display:flex;gap:12px;flex-wrap:wrap;
    margin-bottom:18px; align-items:center;
  }
  .nav .chip{padding:8px 12px;border-radius:8px;background:rgba(255,255,255,0.02);border:1px solid rgba(0,255,153,0.04);font-size:13px;cursor:pointer;color:var(--accent);transition:all .12s}
  .nav .chip.active{background:linear-gradient(90deg, rgba(0,255,153,0.06), rgba(0,209,255,0.03));box-shadow: 0 8px 24px rgba(0,255,153,0.02)}

  /* sections */
  .section{display:none;opacity:0;transform:translateY(14px);transition:all .45s cubic-bezier(.2,.9,.3,1);padding:12px}
  .section.active{display:block;opacity:1;transform:translateY(0)}

  /* project cards */
  .projects-grid{display:grid;grid-template-columns:repeat(2,1fr);gap:18px;margin-top:12px;}
  .card{background:linear-gradient(180deg, rgba(255,255,255,0.01), rgba(255,255,255,0.02));border-radius:10px;padding:14px;border:1px solid rgba(0,255,153,0.04);min-height:220px;display:flex;flex-direction:column;justify-content:space-between}
  .card h3{font-family:var(--mono);font-size:12px;margin:0;color:var(--accent)}
  .card p{font-size:13px;color:var(--muted);margin:8px 0 12px}
  .card img{width:100%;height:120px;object-fit:cover;border-radius:6px;border:1px solid rgba(0,255,153,0.03)}
  .tag{font-family:var(--mono);font-size:11px;color:#001;background:var(--accent);padding:6px;border-radius:6px;display:inline-block;margin-top:6px}

  /* about */
  .about-grid{display:grid;grid-template-columns:1fr 320px;gap:20px;align-items:start}
  .bio{font-size:14px;color:var(--muted);line-height:1.6}
  .skills{background:linear-gradient(180deg, rgba(255,255,255,0.01), rgba(255,255,255,0.02));padding:12px;border-radius:10px;border:1px solid rgba(0,255,153,0.03)}
  .skill-row{display:flex;flex-wrap:wrap;gap:8px}

  /* contact */
  .contact-box{display:flex;flex-direction:column;gap:8px}
  .contact-box input, .contact-box textarea{background:transparent;border:1px solid rgba(0,255,153,0.06);padding:10px;border-radius:8px;color:var(--muted);font-size:13px}
  .cta{background:var(--accent);color:#001;padding:12px;border-radius:8px;border:none;cursor:pointer;font-family:var(--mono)}

  /* footer */
  .meta{display:flex;justify-content:space-between;align-items:center;margin-top:18px;font-size:12px;color:var(--muted)}
  .sound-toggle{cursor:pointer;padding:8px;border-radius:8px;border:1px solid rgba(0,255,153,0.04);background:transparent;color:var(--accent)}

  /* responsive */
  @media (max-width:900px){
    .projects-grid{grid-template-columns:1fr}
    .about-grid{grid-template-columns:1fr}
    .logo p{display:none}
    .frame{margin:14px}
    .screen{min-height:650px}
  }
</style>
</head>
<body>

<div class="frame">
  <header>
    <div class="logo">
      <div class="badge">AI</div>
      <div>
        <h1>[Your Name]</h1>
        <p>AI · Creativity · Language</p>
      </div>
    </div>
    <div style="display:flex;align-items:center;gap:12px">
      <div class="sound-toggle" id="soundToggle">Sound: ON</div>
      <div style="font-size:12px;color:var(--muted)">@Palermo</div>
    </div>
  </header>

  <div class="screen" id="screen">

    <!-- START OVERLAY -->
    <div class="start-overlay" id="startOverlay">
      <div class="title">WELCOME TO MY AI ARCADE</div>
      <div class="typed-box"><span id="typedIntro"></span></div>
      <button class="start-btn" id="startBtn">START</button>

      <div class="loading-wrap" style="display:none" id="loadingWrap">
        <div style="font-family:var(--mono);font-size:11px;color:var(--muted)">BOOT SEQUENCE</div>
        <div class="bar" aria-hidden="true"><div class="bar-inner" id="barInner"></div></div>
        <div class="bar-perc" id="barPerc">0%</div>
      </div>
    </div>

    <!-- NAV -->
    <nav class="nav" id="mainNav" style="display:none">
      <div class="chip active" data-target="projects">Projects</div>
      <div class="chip" data-target="about">About</div>
      <div class="chip" data-target="contact">Contact</div>
    </nav>

    <!-- CONTENT SECTIONS -->
    <div id="projects" class="section">
      <h2 style="margin-top:6px">Projects</h2>
      <div class="projects-grid">
        <div class="card">
          <div>
            <h3>Mindful Journals — AI Book Series</h3>
            <p>Prompt design and iterative refinement to generate cover art and low-content interior pages for a mindfulness journal series.</p>
          </div>
          <div>
            <img src="assets/journal-cover1.jpg" alt="journal cover 1">
          </div>
          <div style="display:flex;justify-content:space-between;align-items:center;margin-top:10px">
            <div class="tag">Midjourney • ChatGPT</div>
            <div style="font-size:11px;color:var(--muted)">2024</div>
          </div>
        </div>

        <div class="card">
          <div>
            <h3>Prompt Engineering & Model Evaluation</h3>
            <p>Freelance evaluation and refinement of prompts for LLMs, focusing on clarity, instruction adherence and factual accuracy.</p>
          </div>
          <div>
            <img src="assets/diagram-flow.png" alt="diagram flow">
          </div>
          <div style="display:flex;justify-content:space-between;align-items:center;margin-top:10px">
            <div class="tag">GPT • Annotation</div>
            <div style="font-size:11px;color:var(--muted)">2023–24</div>
          </div>
        </div>

        <div class="card">
          <div>
            <h3>AI x Cinema — Visual Tribute</h3>
            <p>Generative visual experiments inspired by European cinema; poster-style images combining poetic motifs and cinematic references.</p>
          </div>
          <div>
            <img src="assets/cinema-poster1.jpg" alt="cinema poster">
          </div>
          <div style="display:flex;justify-content:space-between;align-items:center;margin-top:10px">
            <div class="tag">DALL·E • Photoshop</div>
            <div style="font-size:11px;color:var(--muted)">2024</div>
          </div>
        </div>

        <div class="card">
          <div>
            <h3>Social Visuals & Copy</h3>
            <p>AI-assisted social concepts combining generated visuals and copywriting to promote sustainable creative practices.</p>
          </div>
          <div>
            <img src="assets/social-mock.jpg" alt="social mock">
          </div>
          <div style="display:flex;justify-content:space-between;align-items:center;margin-top:10px">
            <div class="tag">ChatGPT • Canva</div>
            <div style="font-size:11px;color:var(--muted)">2024</div>
          </div>
        </div>

      </div>
    </div>

    <div id="about" class="section">
      <h2>About me</h2>
      <div class="about-grid" style="margin-top:12px">
        <div>
          <p class="bio">I am a language & data specialist combining a humanistic background with a growing technical toolkit. I work at the intersection of prompt design, content evaluation and creative AI experimentation. My work blends rigorous linguistic thinking with a passion for visual storytelling.</p>

          <p class="bio" style="margin-top:12px">Selected for the Schuman Traineeship Programme (European Parliament, Luxembourg, 2024). Experience in academic project coordination, festival volunteering (Cinema City Palermo) and international presentations (conference in Salamanca).</p>
        </div>

        <aside class="skills">
          <div style="font-family:var(--mono);font-size:12px;color:var(--accent);margin-bottom:8px">Skills</div>
          <div class="skill-row">
            <div class="tag" style="background:#001;color:var(--accent)">Prompt Engineering</div>
            <div class="tag" style="background:#001;color:var(--accent)">LLM Evaluation</div>
            <div class="tag" style="background:#001;color:var(--accent)">Midjourney</div>
            <div class="tag" style="background:#001;color:var(--accent)">DALL·E</div>
            <div class="tag" style="background:#001;color:var(--accent)">Canva</div>
            <div class="tag" style="background:#001;color:var(--accent)">Basic Python</div>
            <div class="tag" style="background:#001;color:var(--accent)">Copywriting</div>
          </div>
        </aside>
      </div>
    </div>

    <div id="contact" class="section">
      <h2>Contact</h2>
      <div style="margin-top:12px" class="contact-box">
        <div style="font-size:13px;color:var(--muted)">Interested in collaborating or want to see more work? Drop a message.</div>
        <input type="text" id="name" placeholder="Your name" />
        <input type="email" id="email" placeholder="Email" />
        <textarea id="message" rows="4" placeholder="Message"></textarea>
        <button class="cta" id="sendBtn">Send Message</button>
      </div>
    </div>

    <!-- meta bar -->
    <div class="meta" style="margin-top:18px">
      <div style="display:flex;gap:10px;align-items:center">
        <div style="font-family:var(--mono);font-size:11px">[Your Name] • AI Creative</div>
        <div style="font-size:12px;color:var(--muted)">Based in Palermo</div>
      </div>
      <div style="display:flex;gap:10px;align-items:center">
        <a href="#" id="cvLink">Download CV</a>
        <a href="https://linkedin.com/in/yourprofile" target="_blank">LinkedIn</a>
      </div>
    </div>

  </div><!-- end screen -->
</div><!-- end frame -->

<script>
/* ========= SOUNDS ========= */
const sounds = {
  boot: new Howl({ src: ['https://freesound.org/data/previews/524/524913_10382503-lq.mp3'], volume: 0.25 }),
  tick: new Howl({ src: ['https://freesound.org/data/previews/466/466238_10026710-lq.mp3'], volume: 0.18 }),
  click: new Howl({ src: ['https://freesound.org/data/previews/66/66112_634166-lq.mp3'], volume: 0.18 }),
  success: new Howl({ src: ['https://freesound.org/data/previews/331/331912_3248244-lq.mp3'], volume: 0.18 }),
};

/* Toggle sound */
let soundOn = true;
const soundToggle = document.getElementById('soundToggle');
soundToggle.addEventListener('click', ()=> {
  soundOn = !soundOn;
  soundToggle.textContent = soundOn ? 'Sound: ON' : 'Sound: OFF';
});

/* Typed intro */
const typed = new Typed('#typedIntro', {
  strings: [
    'Booting creative engine…',
    'Loading prompt modules and image pipelines…',
    'System ready. Press START to enter the portfolio.'
  ],
  typeSpeed: 35,
  backSpeed: 0,
  startDelay: 300,
  showCursor: false
});

/* Start button and loading */
const startBtn = document.getElementById('startBtn');
const startOverlay = document.getElementById('startOverlay');
const loadingWrap = document.getElementById('loadingWrap');
const barInner = document.getElementById('barInner');
const barPerc = document.getElementById('barPerc');
const mainNav = document.getElementById('mainNav');

startBtn.addEventListener('click', async () => {
  if(soundOn) sounds.click.play();
  // hide typed, show loading
  loadingWrap.style.display = 'flex';
  startBtn.style.display = 'none';

  if(soundOn) sounds.boot.play();

  // animated load values
  let progress = 0;
  const simInterval = setInterval(()=>{
    progress += Math.random()*12;
    if(progress>100) progress = 100;
    barInner.style.width = progress + '%';
    barPerc.textContent = Math.floor(progress) + '%';
    if(progress>=100){
      clearInterval(simInterval);
      setTimeout(()=> enterPortfolio(), 500);
      if(soundOn) sounds.success.play();
    }
  }, 300);
});

/* Enter portfolio */
function enterPortfolio(){
  startOverlay.style.display = 'none';
  mainNav.style.display = 'flex';
  showSection('projects');
  // small nav animation
  document.querySelectorAll('.chip').forEach(c=>{
    c.addEventListener('click', ()=> {
      document.querySelectorAll('.chip').forEach(x=>x.classList.remove('active'));
      c.classList.add('active');
      let t = c.getAttribute('data-target');
      showSection(t);
      if(soundOn) sounds.click.play();
    });
  });
}

/* show section with nice transition */
function showSection(id){
  document.querySelectorAll('.section').forEach(s=>{
    s.classList.remove('active');
    // small exit effect
    s.style.opacity = 0;
    s.style.transform = 'translateY(10px)';
    setTimeout(()=> s.style.display = 'none', 200);
  });
  const target = document.getElementById(id);
  target.style.display = 'block';
  setTimeout(()=> {
    target.classList.add('active');
    window.scrollTo({top:0, behavior:'smooth'});
  }, 40);
}

/* Contact form emulation */
document.getElementById('sendBtn').addEventListener('click', ()=>{
  const name = document.getElementById('name').value || 'Guest';
  if(soundOn) sounds.tick.play();
  alert(`Thanks ${name}! Your message was sent (demo). I'll reply soon.`);
});

/* CV link placeholder */
document.getElementById('cvLink').addEventListener('click',(e)=>{
  e.preventDefault();
  alert('CV download placeholder — replace with your CV file link.');
});

/* small keyboard interaction - press 1/2/3 to jump sections */
document.addEventListener('keydown',(e)=>{
  if(document.getElementById('startOverlay').style.display === 'none'){
    if(e.key === '1') document.querySelector('.chip[data-target="projects"]').click();
    if(e.key === '2') document.querySelector('.chip[data-target="about"]').click();
    if(e.key === '3') document.querySelector('.chip[data-target="contact"]').click();
  }
});
</script>
</body>
</html>
