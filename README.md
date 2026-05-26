<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width,initial-scale=1.0"/>
<title>Ruhani Afroz — Data Analyst</title>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,700;0,900;1,400;1,700&family=Outfit:wght@300;400;500;600&family=JetBrains+Mono:wght@300;400;500&display=swap" rel="stylesheet"/>
<style>
*,*::before,*::after{box-sizing:border-box;margin:0;padding:0}
:root{
  --gold:#c9a84c;
  --gold-light:#e8c97a;
  --gold-dim:#7a6130;
  --ink:#0d0c0a;
  --ink2:#1a1815;
  --paper:#f5f0e8;
  --paper2:#ede7d9;
  --cream:#faf7f2;
  --text:#2a251e;
  --muted:#7a7268;
  --border:#d4c9b0;
  --white:#ffffff;
}
html{scroll-behavior:smooth}
body{
  background:var(--ink);
  color:var(--paper);
  font-family:'Outfit',sans-serif;
  font-weight:400;
  line-height:1.6;
  overflow-x:hidden;
  cursor:none;
}

/* ── CURSOR ── */
.cursor{position:fixed;pointer-events:none;z-index:9999;mix-blend-mode:difference}
.cursor-dot{width:8px;height:8px;background:var(--gold);border-radius:50%;transform:translate(-50%,-50%);transition:transform 0.1s}
.cursor-ring{width:36px;height:36px;border:1.5px solid var(--gold);border-radius:50%;transform:translate(-50%,-50%);transition:transform 0.12s,width 0.2s,height 0.2s,opacity 0.2s;opacity:0.5}
body:has(a:hover) .cursor-ring,body:has(button:hover) .cursor-ring{width:56px;height:56px;opacity:1}

/* ── CANVAS BG ── */
canvas#bg{position:fixed;inset:0;z-index:0;opacity:0.18}

/* ── NAV ── */
nav{
  position:fixed;top:0;left:0;right:0;z-index:200;
  display:flex;justify-content:space-between;align-items:center;
  padding:1.4rem 5rem;
  border-bottom:1px solid rgba(201,168,76,0.15);
  background:rgba(13,12,10,0.8);
  backdrop-filter:blur(20px);
}
.nav-brand{
  font-family:'Playfair Display',serif;
  font-size:1.1rem;
  font-weight:700;
  color:var(--gold);
  letter-spacing:0.05em;
}
.nav-links{display:flex;gap:2.5rem;align-items:center}
.nav-links a{
  font-size:0.72rem;font-weight:500;letter-spacing:0.18em;
  text-transform:uppercase;text-decoration:none;
  color:rgba(245,240,232,0.5);
  transition:color 0.2s;
}
.nav-links a:hover{color:var(--gold)}
.nav-cta{
  padding:0.5rem 1.2rem;
  border:1px solid var(--gold);
  color:var(--gold)!important;
  font-size:0.72rem!important;
}
.nav-cta:hover{background:var(--gold);color:var(--ink)!important}

/* ── HERO ── */
.hero{
  min-height:100vh;
  display:grid;
  grid-template-columns:1fr 480px;
  align-items:center;
  padding:7rem 5rem 5rem;
  position:relative;
  z-index:1;
  gap:4rem;
}
.hero-eyebrow{
  display:flex;align-items:center;gap:0.8rem;
  margin-bottom:2rem;
  opacity:0;animation:rise 0.8s ease 0.1s forwards;
}
.eyebrow-line{width:40px;height:1px;background:var(--gold)}
.eyebrow-text{
  font-size:0.68rem;font-weight:500;letter-spacing:0.25em;
  text-transform:uppercase;color:var(--gold);
}
.hero-name{
  font-family:'Playfair Display',serif;
  font-size:clamp(3.5rem,6vw,6rem);
  font-weight:900;
  line-height:0.95;
  color:var(--paper);
  margin-bottom:0.2rem;
  opacity:0;animation:rise 0.9s ease 0.2s forwards;
}
.hero-name-last{
  font-style:italic;
  -webkit-text-stroke:1px var(--gold);
  color:transparent;
}
.hero-title{
  font-size:0.8rem;font-weight:500;letter-spacing:0.3em;
  text-transform:uppercase;color:var(--muted);
  margin-bottom:2.5rem;
  opacity:0;animation:rise 0.9s ease 0.3s forwards;
}
.hero-bio{
  font-size:1rem;font-weight:300;line-height:1.85;
  color:rgba(245,240,232,0.65);
  max-width:520px;
  margin-bottom:3rem;
  opacity:0;animation:rise 0.9s ease 0.4s forwards;
}
.hero-actions{
  display:flex;gap:1rem;flex-wrap:wrap;
  opacity:0;animation:rise 0.9s ease 0.5s forwards;
}
.btn{
  display:inline-flex;align-items:center;gap:0.6rem;
  padding:0.75rem 1.8rem;
  font-family:'Outfit',sans-serif;
  font-size:0.78rem;font-weight:500;
  letter-spacing:0.1em;text-transform:uppercase;
  text-decoration:none;border-radius:0;
  transition:all 0.25s;cursor:none;
}
.btn-gold{background:var(--gold);color:var(--ink)}
.btn-gold:hover{background:var(--gold-light);transform:translateY(-3px)}
.btn-outline{border:1px solid rgba(201,168,76,0.4);color:var(--paper)}
.btn-outline:hover{border-color:var(--gold);color:var(--gold);transform:translateY(-3px)}
.btn svg{width:14px;height:14px;flex-shrink:0}

/* ── HERO RIGHT: ORBIT CARD ── */
.hero-right{
  position:relative;
  opacity:0;animation:rise 1s ease 0.4s forwards;
}
.profile-orb{
  position:relative;
  width:360px;height:360px;
  margin:0 auto;
}
.orb-outer{
  position:absolute;inset:0;
  border:1px solid rgba(201,168,76,0.2);
  border-radius:50%;
  animation:spin 20s linear infinite;
}
.orb-outer::before{
  content:'';position:absolute;
  top:-4px;left:50%;
  width:8px;height:8px;
  background:var(--gold);
  border-radius:50%;
  transform:translateX(-50%);
}
.orb-mid{
  position:absolute;inset:30px;
  border:1px dashed rgba(201,168,76,0.15);
  border-radius:50%;
  animation:spin 12s linear infinite reverse;
}
.orb-inner{
  position:absolute;inset:70px;
  background:var(--ink2);
  border:1px solid rgba(201,168,76,0.25);
  border-radius:50%;
  display:flex;flex-direction:column;
  align-items:center;justify-content:center;
  gap:0.5rem;
}
.orb-initials{
  font-family:'Playfair Display',serif;
  font-size:3.5rem;font-weight:900;
  color:var(--gold);
  line-height:1;
}
.orb-tag{
  font-size:0.6rem;font-weight:500;letter-spacing:0.25em;
  text-transform:uppercase;color:var(--muted);
}
/* floating stat pills around orb */
.orb-pill{
  position:absolute;
  background:var(--ink2);
  border:1px solid rgba(201,168,76,0.3);
  padding:0.5rem 0.9rem;
  font-size:0.72rem;
  white-space:nowrap;
}
.orb-pill .pill-val{
  font-family:'JetBrains Mono',monospace;
  font-size:1rem;font-weight:500;
  color:var(--gold);
  display:block;
}
.orb-pill .pill-lbl{
  font-size:0.6rem;font-weight:500;
  letter-spacing:0.15em;text-transform:uppercase;
  color:var(--muted);
}
.pill-1{top:10px;right:-20px;animation:float1 4s ease-in-out infinite}
.pill-2{bottom:30px;right:-30px;animation:float2 5s ease-in-out infinite}
.pill-3{bottom:10px;left:-20px;animation:float1 4.5s ease-in-out 1s infinite}

/* ── DIVIDER ── */
.divider{
  position:relative;z-index:1;
  display:flex;align-items:center;gap:1.5rem;
  padding:0 5rem;
}
.divider-line{flex:1;height:1px;background:linear-gradient(90deg,transparent,rgba(201,168,76,0.3),transparent)}
.divider-diamond{
  width:8px;height:8px;
  background:var(--gold);
  transform:rotate(45deg);
  flex-shrink:0;
}

/* ── SECTION ── */
.section{
  padding:7rem 5rem;
  position:relative;z-index:1;
}
.section-label{
  display:flex;align-items:center;gap:1rem;
  margin-bottom:1rem;
}
.label-num{
  font-family:'JetBrains Mono',monospace;
  font-size:0.65rem;color:var(--gold);letter-spacing:0.1em;
}
.label-dash{width:30px;height:1px;background:var(--gold)}
.label-text{
  font-size:0.65rem;font-weight:500;letter-spacing:0.2em;
  text-transform:uppercase;color:var(--muted);
}
.section-heading{
  font-family:'Playfair Display',serif;
  font-size:clamp(2.2rem,4vw,3.5rem);
  font-weight:900;color:var(--paper);
  margin-bottom:3.5rem;
  line-height:1.1;
}
.section-heading em{font-style:italic;color:var(--gold)}

/* ── SKILLS ── */
.skills-section{background:var(--ink2)}
.skills-wrap{
  display:grid;
  grid-template-columns:1fr 1fr;
  gap:5rem;
  align-items:start;
}
.skills-left{}
.skills-right{
  display:grid;
  grid-template-columns:repeat(3,1fr);
  gap:1px;
  background:rgba(201,168,76,0.1);
  border:1px solid rgba(201,168,76,0.15);
}
.skill-item{
  background:var(--ink2);
  padding:1.2rem;
  text-align:center;
  font-size:0.78rem;
  font-weight:500;
  color:rgba(245,240,232,0.6);
  transition:all 0.25s;
  cursor:default;
}
.skill-item:hover{background:rgba(201,168,76,0.08);color:var(--gold)}
.skill-icon{font-size:1.4rem;display:block;margin-bottom:0.4rem}
.skill-bar-wrap{margin-top:2rem}
.skill-bar-item{margin-bottom:1.2rem}
.skill-bar-label{
  display:flex;justify-content:space-between;
  font-size:0.75rem;font-weight:500;
  color:rgba(245,240,232,0.7);
  margin-bottom:0.4rem;
}
.skill-bar-track{
  height:2px;background:rgba(201,168,76,0.15);
  overflow:hidden;
}
.skill-bar-fill{
  height:100%;background:var(--gold);
  transform:scaleX(0);transform-origin:left;
  animation:barFill 1.5s ease forwards;
  animation-play-state:paused;
}
.skill-bar-fill.visible{animation-play-state:running}
@keyframes barFill{to{transform:scaleX(1)}}

/* ── EXPERIENCE ── */
.exp-wrap{display:grid;grid-template-columns:1fr 1fr;gap:2px;background:rgba(201,168,76,0.08)}
.exp-card{
  background:var(--ink);
  padding:2.5rem;
  position:relative;
  overflow:hidden;
  transition:background 0.3s;
}
.exp-card:hover{background:var(--ink2)}
.exp-card::after{
  content:'';position:absolute;
  top:0;left:0;bottom:0;width:2px;
  background:linear-gradient(180deg,var(--gold),transparent);
  opacity:0;transition:opacity 0.3s;
}
.exp-card:hover::after{opacity:1}
.exp-date-badge{
  display:inline-block;
  font-family:'JetBrains Mono',monospace;
  font-size:0.65rem;font-weight:500;
  color:var(--gold);
  border:1px solid rgba(201,168,76,0.3);
  padding:0.2rem 0.6rem;
  margin-bottom:1rem;
  letter-spacing:0.1em;
}
.exp-role{
  font-family:'Playfair Display',serif;
  font-size:1.4rem;font-weight:700;
  color:var(--paper);
  margin-bottom:0.3rem;
}
.exp-company{
  font-size:0.78rem;font-weight:500;
  color:var(--gold-dim);letter-spacing:0.08em;
  margin-bottom:1.5rem;
}
.exp-bullets{list-style:none;display:flex;flex-direction:column;gap:0.7rem}
.exp-bullets li{
  font-size:0.82rem;font-weight:300;
  color:rgba(245,240,232,0.55);
  padding-left:1.2rem;
  position:relative;line-height:1.7;
}
.exp-bullets li::before{
  content:'◆';position:absolute;left:0;
  color:var(--gold);font-size:0.45rem;
  top:0.45rem;
}

/* ── PROJECTS ── */
.projects-section{background:var(--ink2)}
.projects-grid{
  display:grid;
  grid-template-columns:1fr 1fr;
  gap:2px;
  background:rgba(201,168,76,0.08);
}
.proj-card{
  background:var(--ink2);
  padding:3rem;
  position:relative;
  overflow:hidden;
  transition:background 0.3s;
  group:true;
}
.proj-card:hover{background:#1e1c18}
.proj-num{
  font-family:'Playfair Display',serif;
  font-size:5rem;font-weight:900;
  color:rgba(201,168,76,0.06);
  line-height:1;
  position:absolute;top:1.5rem;right:2rem;
  transition:color 0.3s;
  user-select:none;
}
.proj-card:hover .proj-num{color:rgba(201,168,76,0.12)}
.proj-tags{display:flex;gap:0.5rem;flex-wrap:wrap;margin-bottom:1.2rem}
.proj-tag{
  font-family:'JetBrains Mono',monospace;
  font-size:0.62rem;font-weight:500;letter-spacing:0.12em;
  color:var(--gold);
  border:1px solid rgba(201,168,76,0.3);
  padding:0.15rem 0.55rem;
}
.proj-name{
  font-family:'Playfair Display',serif;
  font-size:1.5rem;font-weight:700;
  color:var(--paper);
  margin-bottom:1rem;
  position:relative;z-index:1;
}
.proj-desc{
  font-size:0.82rem;font-weight:300;
  color:rgba(245,240,232,0.5);
  line-height:1.8;
  position:relative;z-index:1;
}
.proj-arrow{
  display:inline-flex;align-items:center;gap:0.4rem;
  margin-top:1.5rem;
  font-size:0.72rem;font-weight:500;
  letter-spacing:0.1em;text-transform:uppercase;
  color:var(--gold);opacity:0;
  transform:translateX(-8px);
  transition:all 0.3s;
}
.proj-card:hover .proj-arrow{opacity:1;transform:translateX(0)}

/* ── EDUCATION ── */
.edu-timeline{
  display:grid;
  grid-template-columns:1fr;
  gap:0;
  border-left:1px solid rgba(201,168,76,0.2);
  padding-left:2rem;
  margin-left:1rem;
}
.edu-item{
  position:relative;
  padding:1.5rem 0;
  border-bottom:1px solid rgba(201,168,76,0.08);
  transition:padding-left 0.25s;
}
.edu-item:last-child{border-bottom:none}
.edu-item::before{
  content:'';
  position:absolute;
  left:-2.38rem;top:2rem;
  width:10px;height:10px;
  background:var(--ink);
  border:2px solid rgba(201,168,76,0.4);
  border-radius:50%;
  transition:border-color 0.25s,background 0.25s;
}
.edu-item:hover::before{border-color:var(--gold);background:var(--gold)}
.edu-item:hover{padding-left:0.5rem}
.edu-degree{
  font-family:'Playfair Display',serif;
  font-size:1.05rem;font-weight:700;
  color:var(--paper);margin-bottom:0.3rem;
}
.edu-inst{
  font-size:0.78rem;font-weight:400;
  color:var(--gold-dim);
}

/* ── ACHIEVEMENTS ── */
.ach-section{background:var(--ink2)}
.ach-grid{
  display:grid;
  grid-template-columns:repeat(2,1fr);
  gap:2px;background:rgba(201,168,76,0.08);
}
.ach-item{
  background:var(--ink2);
  padding:2rem 2.5rem;
  display:flex;gap:1.2rem;align-items:flex-start;
  transition:background 0.25s;
}
.ach-item:hover{background:#1e1c18}
.ach-diamond{
  width:24px;height:24px;
  background:rgba(201,168,76,0.1);
  border:1px solid rgba(201,168,76,0.4);
  transform:rotate(45deg);
  flex-shrink:0;
  margin-top:0.1rem;
  display:flex;align-items:center;justify-content:center;
}
.ach-diamond-inner{
  width:8px;height:8px;
  background:var(--gold);
  transform:rotate(0deg);
}
.ach-text{
  font-size:0.85rem;font-weight:300;
  color:rgba(245,240,232,0.6);
  line-height:1.75;
}

/* ── CONTACT ── */
.contact-section{
  padding:7rem 5rem;
  position:relative;z-index:1;
  overflow:hidden;
}
.contact-section::before{
  content:'CONNECT';
  position:absolute;
  font-family:'Playfair Display',serif;
  font-size:14vw;font-weight:900;
  color:rgba(201,168,76,0.03);
  bottom:-2rem;right:-1rem;
  line-height:1;
  pointer-events:none;user-select:none;
  white-space:nowrap;
}
.contact-grid{
  display:grid;
  grid-template-columns:1fr 1fr;
  gap:5rem;
  align-items:start;
}
.contact-intro{
  font-family:'Playfair Display',serif;
  font-size:2.2rem;font-weight:700;
  color:var(--paper);
  line-height:1.2;
  margin-bottom:1.5rem;
}
.contact-intro em{font-style:italic;color:var(--gold)}
.contact-sub{
  font-size:0.9rem;font-weight:300;
  color:rgba(245,240,232,0.5);
  line-height:1.8;
  margin-bottom:2rem;
}
.contact-items{display:flex;flex-direction:column;gap:1.5rem}
.contact-link{
  display:flex;align-items:center;gap:1.2rem;
  text-decoration:none;
  padding:1.2rem 1.5rem;
  border:1px solid rgba(201,168,76,0.12);
  transition:all 0.25s;
  group:true;
}
.contact-link:hover{border-color:var(--gold);background:rgba(201,168,76,0.04);transform:translateX(4px)}
.contact-link-icon{
  width:36px;height:36px;
  background:rgba(201,168,76,0.1);
  display:flex;align-items:center;justify-content:center;
  flex-shrink:0;
}
.contact-link-icon svg{width:16px;height:16px;stroke:var(--gold)}
.contact-link-body{}
.contact-link-lbl{
  font-size:0.62rem;font-weight:500;letter-spacing:0.2em;
  text-transform:uppercase;color:var(--muted);
  display:block;margin-bottom:0.15rem;
}
.contact-link-val{
  font-size:0.9rem;font-weight:400;
  color:var(--paper);
}
.contact-link:hover .contact-link-val{color:var(--gold)}
.contact-link-arrow{
  margin-left:auto;
  opacity:0;transform:translateX(-6px);
  transition:all 0.25s;
  color:var(--gold);font-size:1.2rem;
}
.contact-link:hover .contact-link-arrow{opacity:1;transform:translateX(0)}

/* ── FOOTER ── */
footer{
  position:relative;z-index:1;
  border-top:1px solid rgba(201,168,76,0.1);
  padding:2rem 5rem;
  display:flex;justify-content:space-between;align-items:center;
}
.footer-copy{
  font-size:0.7rem;font-weight:300;
  color:var(--muted);letter-spacing:0.08em;
}
.footer-brand{
  font-family:'Playfair Display',serif;
  font-size:0.9rem;font-weight:700;
  color:var(--gold);
}

/* ── ANIMATIONS ── */
@keyframes rise{
  from{opacity:0;transform:translateY(24px)}
  to{opacity:1;transform:translateY(0)}
}
@keyframes spin{to{transform:rotate(360deg)}}
@keyframes float1{
  0%,100%{transform:translateY(0)}
  50%{transform:translateY(-10px)}
}
@keyframes float2{
  0%,100%{transform:translateY(0)}
  50%{transform:translateY(8px)}
}

/* ── SCROLL REVEAL ── */
.reveal{opacity:0;transform:translateY(28px);transition:opacity 0.7s ease,transform 0.7s ease}
.reveal.in{opacity:1;transform:translateY(0)}

/* ── RESPONSIVE ── */
@media(max-width:900px){
  nav{padding:1rem 1.5rem}
  .nav-links{display:none}
  .hero{grid-template-columns:1fr;padding:7rem 1.5rem 3rem;gap:2rem}
  .hero-right{display:none}
  .section{padding:4rem 1.5rem}
  .skills-wrap,.exp-wrap,.projects-grid,.ach-grid,.contact-grid{grid-template-columns:1fr}
  .skills-right{grid-template-columns:repeat(2,1fr)}
  .divider{padding:0 1.5rem}
  footer{padding:2rem 1.5rem;flex-direction:column;gap:1rem;text-align:center}
  .contact-section{padding:4rem 1.5rem}
  body{cursor:auto}
}
</style>
</head>
<body>

<!-- CURSOR -->
<div class="cursor" id="cursorDot" style="position:fixed;top:0;left:0;pointer-events:none;z-index:9999">
  <div class="cursor-dot" style="width:8px;height:8px;background:#c9a84c;border-radius:50%;transform:translate(-50%,-50%)"></div>
</div>
<div class="cursor" id="cursorRing" style="position:fixed;top:0;left:0;pointer-events:none;z-index:9998;transition:transform 0.1s">
  <div class="cursor-ring" style="width:36px;height:36px;border:1.5px solid #c9a84c;border-radius:50%;transform:translate(-50%,-50%);opacity:0.4"></div>
</div>

<!-- CANVAS BACKGROUND -->
<canvas id="bg"></canvas>

<!-- NAV -->
<nav>
  <div class="nav-brand">Ruhani Afroz</div>
  <div class="nav-links">
    <a href="#skills">Skills</a>
    <a href="#experience">Experience</a>
    <a href="#projects">Projects</a>
    <a href="#education">Education</a>
    <a href="#contact" class="nav-cta">Contact</a>
  </div>
</nav>

<!-- HERO -->
<section class="hero" id="home">
  <div class="hero-left">
    <div class="hero-eyebrow">
      <div class="eyebrow-line"></div>
      <span class="eyebrow-text">Data Analyst · Dhaka, Bangladesh</span>
    </div>
    <h1 class="hero-name">
      Ruhani<br/>
      <span class="hero-name-last">Afroz</span>
    </h1>
    <p class="hero-title">Turning Raw Data Into Strategic Clarity</p>
    <p class="hero-bio">
      Detail-oriented Data Analyst with proven expertise in SQL, Python, and Power BI.
      Experienced in transforming complex datasets into evidence-based recommendations
      that drive faster, better decisions for cross-functional stakeholders.
    </p>
    <div class="hero-actions">
      <a href="https://linkedin.com/in/ruhaniafroz" target="_blank" class="btn btn-gold">
        <svg viewBox="0 0 24 24" fill="currentColor"><path d="M16 8a6 6 0 016 6v7h-4v-7a2 2 0 00-4 0v7h-4v-7a6 6 0 016-6zM2 9h4v12H2z"/><circle cx="4" cy="4" r="2"/></svg>
        LinkedIn
      </a>
      <a href="https://github.com/afrozruhani-lab" target="_blank" class="btn btn-outline">
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M9 19c-5 1.5-5-2.5-7-3m14 6v-3.87a3.37 3.37 0 00-.94-2.61c3.14-.35 6.44-1.54 6.44-7A5.44 5.44 0 0020 4.77 5.07 5.07 0 0019.91 1S18.73.65 16 2.48a13.38 13.38 0 00-7 0C6.27.65 5.09 1 5.09 1A5.07 5.07 0 005 4.77a5.44 5.44 0 00-1.5 3.78c0 5.42 3.3 6.61 6.44 7A3.37 3.37 0 009 18.13V22"/></svg>
        GitHub
      </a>
      <a href="mailto:afrozruhani@gmail.com" class="btn btn-outline">
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"/><polyline points="22,6 12,13 2,6"/></svg>
        Email
      </a>
    </div>
  </div>

  <div class="hero-right">
    <div class="profile-orb">
      <div class="orb-outer"></div>
      <div class="orb-mid"></div>
      <div class="orb-inner">
        <div class="orb-initials">RA</div>
        <div class="orb-tag">Data Analyst</div>
      </div>
      <div class="orb-pill pill-1">
        <span class="pill-val">2023</span>
        <span class="pill-lbl">Active since</span>
      </div>
      <div class="orb-pill pill-2">
        <span class="pill-val">Power BI</span>
        <span class="pill-lbl">Primary Tool</span>
      </div>
      <div class="orb-pill pill-3">
        <span class="pill-val">4+</span>
        <span class="pill-lbl">Certifications</span>
      </div>
    </div>
  </div>
</section>

<div class="divider"><div class="divider-line"></div><div class="divider-diamond"></div><div class="divider-line"></div></div>

<!-- SKILLS -->
<section class="section skills-section" id="skills">
  <div class="skills-wrap">
    <div class="skills-left reveal">
      <div class="section-label">
        <span class="label-num">01</span>
        <div class="label-dash"></div>
        <span class="label-text">Capabilities</span>
      </div>
      <h2 class="section-heading">Technical<br/><em>Mastery</em></h2>
      <div class="skill-bar-wrap">
        <div class="skill-bar-item">
          <div class="skill-bar-label"><span>SQL</span><span>95%</span></div>
          <div class="skill-bar-track"><div class="skill-bar-fill" style="animation-delay:0s;width:95%"></div></div>
        </div>
        <div class="skill-bar-item">
          <div class="skill-bar-label"><span>Python / Pandas</span><span>88%</span></div>
          <div class="skill-bar-track"><div class="skill-bar-fill" style="animation-delay:0.15s;width:88%"></div></div>
        </div>
        <div class="skill-bar-item">
          <div class="skill-bar-label"><span>Power BI</span><span>92%</span></div>
          <div class="skill-bar-track"><div class="skill-bar-fill" style="animation-delay:0.3s;width:92%"></div></div>
        </div>
        <div class="skill-bar-item">
          <div class="skill-bar-label"><span>Machine Learning</span><span>75%</span></div>
          <div class="skill-bar-track"><div class="skill-bar-fill" style="animation-delay:0.45s;width:75%"></div></div>
        </div>
        <div class="skill-bar-item">
          <div class="skill-bar-label"><span>EDA &amp; Visualization</span><span>90%</span></div>
          <div class="skill-bar-track"><div class="skill-bar-fill" style="animation-delay:0.6s;width:90%"></div></div>
        </div>
      </div>
    </div>
    <div class="skills-right reveal" style="transition-delay:0.2s">
      <div class="skill-item"><span class="skill-icon">🗄</span>SQL</div>
      <div class="skill-item"><span class="skill-icon">🐍</span>Python</div>
      <div class="skill-item"><span class="skill-icon">📊</span>Power BI</div>
      <div class="skill-item"><span class="skill-icon">🐼</span>Pandas</div>
      <div class="skill-item"><span class="skill-icon">📈</span>EDA</div>
      <div class="skill-item"><span class="skill-icon">🤖</span>ML</div>
      <div class="skill-item"><span class="skill-icon">🌐</span>Django</div>
      <div class="skill-item"><span class="skill-icon">🎯</span>BI</div>
      <div class="skill-item"><span class="skill-icon">🔍</span>Root Cause</div>
      <div class="skill-item"><span class="skill-icon">🧹</span>Data Cleaning</div>
      <div class="skill-item"><span class="skill-icon">📋</span>Reporting</div>
      <div class="skill-item"><span class="skill-icon">💡</span>Storytelling</div>
    </div>
  </div>
</section>

<div class="divider"><div class="divider-line"></div><div class="divider-diamond"></div><div class="divider-line"></div></div>

<!-- EXPERIENCE -->
<section class="section" id="experience">
  <div class="section-label reveal">
    <span class="label-num">02</span>
    <div class="label-dash"></div>
    <span class="label-text">Career</span>
  </div>
  <h2 class="section-heading reveal">Work<br/><em>Experience</em></h2>
  <div class="exp-wrap reveal">
    <div class="exp-card">
      <div class="exp-date-badge">2023 – Present</div>
      <div class="exp-role">Data Analyst</div>
      <div class="exp-company">Electro Globe · Dhaka, Bangladesh</div>
      <ul class="exp-bullets">
        <li>Designed and maintained weekly Power BI dashboards improving executive visibility across sales, operations, and customer performance metrics.</li>
        <li>Cleaned and transformed raw datasets using SQL and Python, reducing manual reporting errors and cutting rework cycles significantly.</li>
        <li>Conducted root-cause and trend analyses, delivering concise stakeholder reports with actionable recommendations.</li>
        <li>Standardized data definitions, validation checks, and reusable report templates, improving organization-wide reporting accuracy.</li>
      </ul>
    </div>
    <div class="exp-card" style="display:flex;flex-direction:column;justify-content:center;align-items:center;text-align:center;padding:3rem;gap:1rem">
      <div style="font-family:'Playfair Display',serif;font-size:4rem;font-weight:900;color:rgba(201,168,76,0.15);line-height:1">01</div>
      <div style="font-size:0.78rem;font-weight:500;letter-spacing:0.15em;text-transform:uppercase;color:var(--muted)">Role Held</div>
      <div style="height:1px;width:40px;background:rgba(201,168,76,0.3)"></div>
      <div style="font-size:0.82rem;font-weight:300;color:rgba(245,240,232,0.4);line-height:1.8;max-width:220px">
        Converted complex operational data into weekly business-review dashboards used by senior management.
      </div>
      <a href="mailto:afrozruhani@gmail.com" class="btn btn-outline" style="margin-top:1rem;font-size:0.7rem">Get in touch →</a>
    </div>
  </div>
</section>

<div class="divider"><div class="divider-line"></div><div class="divider-diamond"></div><div class="divider-line"></div></div>

<!-- PROJECTS -->
<section class="section projects-section" id="projects">
  <div class="section-label reveal">
    <span class="label-num">03</span>
    <div class="label-dash"></div>
    <span class="label-text">Portfolio</span>
  </div>
  <h2 class="section-heading reveal">Selected<br/><em>Projects</em></h2>
  <div class="projects-grid reveal">
    <div class="proj-card">
      <div class="proj-num">01</div>
      <div class="proj-tags">
        <span class="proj-tag">SQL</span>
        <span class="proj-tag">Power BI</span>
        <span class="proj-tag">Dashboard</span>
      </div>
      <div class="proj-name">Sales Performance Dashboard</div>
      <p class="proj-desc">Analyzed sales data segmented by region, product, and month. Built interactive filters in Power BI highlighting revenue growth trends, margin changes, and underperforming product categories — enabling targeted corrective actions.</p>
      <div class="proj-arrow">
        <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><line x1="5" y1="12" x2="19" y2="12"/><polyline points="12 5 19 12 12 19"/></svg>
        View on GitHub
      </div>
    </div>
    <div class="proj-card">
      <div class="proj-num">02</div>
      <div class="proj-tags">
        <span class="proj-tag">Python</span>
        <span class="proj-tag">Pandas</span>
        <span class="proj-tag">Analytics</span>
      </div>
      <div class="proj-name">Customer Churn &amp; Retention Analysis</div>
      <p class="proj-desc">Used Python to clean customer datasets, calculate churn indicators, and identify behavioral patterns. Delivered retention strategy recommendations focused on high-risk customer segments with measurable impact.</p>
      <div class="proj-arrow">
        <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><line x1="5" y1="12" x2="19" y2="12"/><polyline points="12 5 19 12 12 19"/></svg>
        View on GitHub
      </div>
    </div>
  </div>
</section>

<div class="divider"><div class="divider-line"></div><div class="divider-diamond"></div><div class="divider-line"></div></div>

<!-- EDUCATION -->
<section class="section" id="education">
  <div class="section-label reveal">
    <span class="label-num">04</span>
    <div class="label-dash"></div>
    <span class="label-text">Qualifications</span>
  </div>
  <h2 class="section-heading reveal">Education &amp;<br/><em>Certifications</em></h2>
  <div class="edu-timeline reveal">
    <div class="edu-item">
      <div class="edu-degree">Master of Business Administration (MBA)</div>
      <div class="edu-inst">Bangladesh University of Business &amp; Technology (BUBT) · Dhaka</div>
    </div>
    <div class="edu-item">
      <div class="edu-degree">Bachelor of Business Administration (BBA)</div>
      <div class="edu-inst">Bangladesh University of Business &amp; Technology (BUBT) · Dhaka</div>
    </div>
    <div class="edu-item">
      <div class="edu-degree">PGD — Data Science &amp; ML Using Python</div>
      <div class="edu-inst">Daffodil International Professional Training Institute (DIPTI)</div>
    </div>
    <div class="edu-item">
      <div class="edu-degree">IT Specialist — Artificial Intelligence</div>
      <div class="edu-inst">Certiport / Pearson VUE</div>
    </div>
    <div class="edu-item">
      <div class="edu-degree">Python &amp; Data Specialist</div>
      <div class="edu-inst">BUET · DU · DIPTI · Creative IT</div>
    </div>
    <div class="edu-item">
      <div class="edu-degree">Python Programming</div>
      <div class="edu-inst">Bangladesh University of Engineering and Technology (BUET)</div>
    </div>
  </div>
</section>

<div class="divider"><div class="divider-line"></div><div class="divider-diamond"></div><div class="divider-line"></div></div>

<!-- ACHIEVEMENTS -->
<section class="section ach-section" id="achievements" style="background:var(--ink2)">
  <div class="section-label reveal">
    <span class="label-num">05</span>
    <div class="label-dash"></div>
    <span class="label-text">Impact</span>
  </div>
  <h2 class="section-heading reveal">Key<br/><em>Achievements</em></h2>
  <div class="ach-grid reveal">
    <div class="ach-item">
      <div class="ach-diamond"><div class="ach-diamond-inner"></div></div>
      <div class="ach-text">Recognized for clear communication, fast learning, and reliable delivery under tight deadlines across all stakeholder levels.</div>
    </div>
    <div class="ach-item">
      <div class="ach-diamond"><div class="ach-diamond-inner"></div></div>
      <div class="ach-text">Improved organization-wide reporting accuracy by standardizing definitions, validation checks, and reusable templates.</div>
    </div>
    <div class="ach-item">
      <div class="ach-diamond"><div class="ach-diamond-inner"></div></div>
      <div class="ach-text">Successfully converted complex operational data into weekly business-review dashboards adopted by senior management.</div>
    </div>
    <div class="ach-item">
      <div class="ach-diamond"><div class="ach-diamond-inner"></div></div>
      <div class="ach-text">Earned multiple certifications across AI, Python, and data science from nationally and internationally accredited institutions.</div>
    </div>
  </div>
</section>

<!-- CONTACT -->
<section class="contact-section" id="contact">
  <div class="contact-grid">
    <div class="reveal">
      <div class="section-label">
        <span class="label-num">06</span>
        <div class="label-dash"></div>
        <span class="label-text">Connect</span>
      </div>
      <div class="contact-intro">Let's work<br/><em>together.</em></div>
      <p class="contact-sub">
        Open to new opportunities, collaborations, and interesting data challenges.
        Reach out through any channel below.
      </p>
      <div style="display:flex;gap:0.8rem;flex-wrap:wrap">
        <span style="font-size:0.72rem;font-weight:500;letter-spacing:0.12em;color:var(--muted)">Bangla (Native)</span>
        <span style="color:rgba(201,168,76,0.3)">·</span>
        <span style="font-size:0.72rem;font-weight:500;letter-spacing:0.12em;color:var(--muted)">English (Professional)</span>
      </div>
    </div>
    <div class="contact-items reveal" style="transition-delay:0.2s">
      <a href="https://linkedin.com/in/ruhaniafroz" target="_blank" class="contact-link">
        <div class="contact-link-icon">
          <svg viewBox="0 0 24 24" fill="none" stroke="#c9a84c" stroke-width="2"><path d="M16 8a6 6 0 016 6v7h-4v-7a2 2 0 00-4 0v7h-4v-7a6 6 0 016-6zM2 9h4v12H2z"/><circle cx="4" cy="4" r="2"/></svg>
        </div>
        <div class="contact-link-body">
          <span class="contact-link-lbl">LinkedIn</span>
          <span class="contact-link-val">linkedin.com/in/ruhaniafroz</span>
        </div>
        <div class="contact-link-arrow">→</div>
      </a>
      <a href="https://github.com/afrozruhani-lab" target="_blank" class="contact-link">
        <div class="contact-link-icon">
          <svg viewBox="0 0 24 24" fill="none" stroke="#c9a84c" stroke-width="2"><path d="M9 19c-5 1.5-5-2.5-7-3m14 6v-3.87a3.37 3.37 0 00-.94-2.61c3.14-.35 6.44-1.54 6.44-7A5.44 5.44 0 0020 4.77 5.07 5.07 0 0019.91 1S18.73.65 16 2.48a13.38 13.38 0 00-7 0C6.27.65 5.09 1 5.09 1A5.07 5.07 0 005 4.77a5.44 5.44 0 00-1.5 3.78c0 5.42 3.3 6.61 6.44 7A3.37 3.37 0 009 18.13V22"/></svg>
        </div>
        <div class="contact-link-body">
          <span class="contact-link-lbl">GitHub</span>
          <span class="contact-link-val">github.com/afrozruhani-lab</span>
        </div>
        <div class="contact-link-arrow">→</div>
      </a>
      <a href="mailto:afrozruhani@gmail.com" class="contact-link">
        <div class="contact-link-icon">
          <svg viewBox="0 0 24 24" fill="none" stroke="#c9a84c" stroke-width="2"><path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"/><polyline points="22,6 12,13 2,6"/></svg>
        </div>
        <div class="contact-link-body">
          <span class="contact-link-lbl">Email</span>
          <span class="contact-link-val">afrozruhani@gmail.com</span>
        </div>
        <div class="contact-link-arrow">→</div>
      </a>
      <a href="tel:+8801729994045" class="contact-link">
        <div class="contact-link-icon">
          <svg viewBox="0 0 24 24" fill="none" stroke="#c9a84c" stroke-width="2"><path d="M22 16.92v3a2 2 0 01-2.18 2 19.79 19.79 0 01-8.63-3.07A19.5 19.5 0 013.07 8.81 19.79 19.79 0 01.1 2.18 2 2 0 012.08 0h3a2 2 0 012 1.72c.127.96.361 1.903.7 2.81a2 2 0 01-.45 2.11L6.91 7.09a16 16 0 006 6l.46-.46a2 2 0 012.1-.45c.907.339 1.85.573 2.81.7A2 2 0 0122 14.92z"/></svg>
        </div>
        <div class="contact-link-body">
          <span class="contact-link-lbl">Phone</span>
          <span class="contact-link-val">+880 1729 994 045</span>
        </div>
        <div class="contact-link-arrow">→</div>
      </a>
    </div>
  </div>
</section>

<footer>
  <span class="footer-copy">© 2025 · Dhaka, Bangladesh · All rights reserved</span>
  <span class="footer-brand">Ruhani Afroz</span>
</footer>

<script>
// ── CURSOR
const dot = document.getElementById('cursorDot');
const ring = document.getElementById('cursorRing');
let mx=0,my=0,rx=0,ry=0;
document.addEventListener('mousemove',e=>{
  mx=e.clientX;my=e.clientY;
  dot.style.left=mx+'px';dot.style.top=my+'px';
});
function animRing(){
  rx+=(mx-rx)*0.12;ry+=(my-ry)*0.12;
  ring.style.left=rx+'px';ring.style.top=ry+'px';
  requestAnimationFrame(animRing);
}
animRing();

// ── CANVAS PARTICLES
const canvas=document.getElementById('bg');
const ctx=canvas.getContext('2d');
let W,H,pts=[];
function resize(){W=canvas.width=innerWidth;H=canvas.height=innerHeight}
resize();addEventListener('resize',resize);
function mkPt(){return{x:Math.random()*W,y:Math.random()*H,vx:(Math.random()-0.5)*0.3,vy:(Math.random()-0.5)*0.3,r:Math.random()*1.5+0.3}}
for(let i=0;i<80;i++)pts.push(mkPt());
function draw(){
  ctx.clearRect(0,0,W,H);
  pts.forEach(p=>{
    p.x+=p.vx;p.y+=p.vy;
    if(p.x<0)p.x=W;if(p.x>W)p.x=0;
    if(p.y<0)p.y=H;if(p.y>H)p.y=0;
    ctx.beginPath();ctx.arc(p.x,p.y,p.r,0,Math.PI*2);
    ctx.fillStyle='rgba(201,168,76,0.6)';ctx.fill();
  });
  pts.forEach((a,i)=>{
    pts.slice(i+1).forEach(b=>{
      const d=Math.hypot(a.x-b.x,a.y-b.y);
      if(d<120){
        ctx.beginPath();ctx.moveTo(a.x,a.y);ctx.lineTo(b.x,b.y);
        ctx.strokeStyle=`rgba(201,168,76,${0.12*(1-d/120)})`;
        ctx.lineWidth=0.5;ctx.stroke();
      }
    });
  });
  requestAnimationFrame(draw);
}
draw();

// ── SCROLL REVEAL
const reveals=document.querySelectorAll('.reveal');
const io=new IntersectionObserver(entries=>{
  entries.forEach(e=>{if(e.isIntersecting){e.target.classList.add('in');io.unobserve(e.target)}});
},{threshold:0.15});
reveals.forEach(el=>io.observe(el));

// ── SKILL BARS
const bars=document.querySelectorAll('.skill-bar-fill');
const barIO=new IntersectionObserver(entries=>{
  entries.forEach(e=>{if(e.isIntersecting){e.target.classList.add('visible');barIO.unobserve(e.target)}});
},{threshold:0.5});
bars.forEach(b=>barIO.observe(b));
</script>
</body>
</html>
