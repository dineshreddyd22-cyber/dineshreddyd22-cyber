<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<meta name="theme-color" content="#050907">
<meta name="description" content="Dinesh Reddy — Creative Developer, AI Image and Video Creator, Interactive Experience Designer.">
<title>Dinesh Reddy | Creative Portfolio</title>

<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=DM+Mono:wght@400;500&family=Manrope:wght@400;500;600;700;800&display=swap" rel="stylesheet">

<style>
:root {
  --bg: #050907;
  --green: #6cffb9;
  --cyan: #64e7ff;
  --text: #f4fff9;
  --muted: #91a69a;
  --line: rgba(140,255,195,.15);
}

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

html {
  scroll-behavior: smooth;
  scroll-padding-top: 85px;
}

body {
  background: var(--bg);
  color: var(--text);
  font-family: "Manrope", sans-serif;
  overflow-x: hidden;
}

a {
  text-decoration: none;
  color: inherit;
}

button {
  font: inherit;
}

::selection {
  background: var(--green);
  color: #041008;
}

/* BACKGROUND */

.background {
  position: fixed;
  inset: 0;
  z-index: -3;
  overflow: hidden;
  background:
    radial-gradient(ellipse at 80% 30%, #063c2b 0%, transparent 35%),
    radial-gradient(ellipse at 20% 80%, #06202a 0%, transparent 40%),
    #050907;
}

.grid {
  position: absolute;
  inset: 0;
  background-image:
    linear-gradient(rgba(108,255,185,.065) 1px, transparent 1px),
    linear-gradient(90deg, rgba(108,255,185,.065) 1px, transparent 1px);
  background-size: 55px 55px;
  mask-image: linear-gradient(to bottom, black, transparent 90%);
  animation: gridMove 22s linear infinite;
}

.glow {
  position: absolute;
  width: 400px;
  height: 400px;
  border-radius: 50%;
  filter: blur(100px);
  opacity: .17;
  animation: glowMove 12s ease-in-out infinite alternate;
}

.glow.one {
  background: #00ff9d;
  top: 10%;
  right: -180px;
}

.glow.two {
  background: #00c8ff;
  bottom: 5%;
  left: -200px;
  animation-delay: -5s;
}

#particles {
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
}

/* NAVIGATION */

header {
  position: fixed;
  z-index: 100;
  top: 0;
  left: 0;
  width: 100%;
  min-height: 76px;
  padding: 20px 7%;
  display: flex;
  align-items: center;
  justify-content: space-between;
  border-bottom: 1px solid transparent;
  transition: .3s;
}

header.scrolled {
  background: rgba(4,10,7,.88);
  backdrop-filter: blur(18px);
  border-color: var(--line);
}

.logo {
  font-size: 15px;
  font-weight: 800;
  letter-spacing: 2px;
  white-space: nowrap;
}

.logo span {
  color: var(--green);
}

nav {
  display: flex;
  align-items: center;
  gap: 30px;
}

nav a {
  color: #bdcec4;
  font-family: "DM Mono", monospace;
  font-size: 10px;
  letter-spacing: 1.5px;
  transition: .25s;
}

nav a:hover {
  color: var(--green);
}

nav .nav-cta {
  padding: 12px 15px;
  border: 1px solid rgba(108,255,185,.45);
  color: var(--green);
}

.menu {
  display: none;
  color: white;
  background: transparent;
  border: 1px solid var(--line);
  padding: 8px 12px;
  font-size: 20px;
}

/* HERO */

.hero {
  position: relative;
  min-height: 100vh;
  min-height: 100svh;
  display: flex;
  align-items: center;
  padding: 125px 10% 110px;
  isolation: isolate;
}

.hero::before {
  content: "";
  position: absolute;
  inset: 0;
  z-index: -1;
  background:
    linear-gradient(90deg, rgba(3,8,5,.95), rgba(3,8,5,.64) 65%, rgba(3,8,5,.3)),
    linear-gradient(0deg, var(--bg), transparent 30%);
}

.hero-content {
  width: 100%;
  max-width: 900px;
}

.eyebrow {
  display: flex;
  align-items: center;
  gap: 12px;
  margin-bottom: 30px;
  color: #b2c6ba;
  font: 10px "DM Mono", monospace;
  letter-spacing: 2px;
  animation: fadeUp 1s both;
}

.dot {
  width: 7px;
  height: 7px;
  border-radius: 50%;
  background: var(--green);
  box-shadow: 0 0 15px var(--green);
  animation: blink 1.5s infinite;
}

.hero h1 {
  font-size: clamp(65px, 12vw, 150px);
  line-height: .85;
  letter-spacing: -.09em;
  font-weight: 800;
}

.letter {
  display: inline-block;
  opacity: 0;
  animation: letterIn .7s forwards;
}

.gradient-text {
  display: inline-block;
  margin-top: 12px;
  color: transparent;
  background: linear-gradient(100deg, white, var(--green), var(--cyan), white);
  background-size: 250% auto;
  background-clip: text;
  -webkit-background-clip: text;
  animation: gradientFlow 6s linear infinite;
}

.roles {
  margin-top: 30px;
  display: flex;
  flex-wrap: wrap;
  gap: 12px;
  color: #b8c9bf;
  font-size: 12px;
  animation: fadeUp 1s .7s both;
}

.roles span + span::before {
  content: "•";
  color: var(--green);
  margin-right: 12px;
}

.tagline {
  margin-top: 32px;
  font-size: clamp(17px, 2.5vw, 25px);
  font-weight: 700;
  line-height: 1.6;
  letter-spacing: 1px;
  animation: fadeUp 1s .9s both;
}

.tagline span {
  color: var(--green);
}

.actions {
  display: flex;
  flex-wrap: wrap;
  gap: 14px;
  margin-top: 32px;
  animation: fadeUp 1s 1.1s both;
}

.btn {
  min-height: 49px;
  padding: 15px 20px;
  display: inline-flex;
  justify-content: center;
  align-items: center;
  gap: 15px;
  border: 1px solid var(--line);
  font: 10px "DM Mono", monospace;
  letter-spacing: 1px;
  transition: .3s;
}

.btn.primary {
  background: var(--green);
  color: #041109;
  border-color: var(--green);
  font-weight: 500;
}

.btn:hover {
  transform: translateY(-4px);
  box-shadow: 0 8px 30px rgba(108,255,185,.12);
}

.btn.secondary:hover {
  border-color: var(--cyan);
  color: var(--cyan);
}

.scroll-down {
  position: absolute;
  right: 7%;
  bottom: 100px;
  display: flex;
  align-items: center;
  gap: 12px;
  writing-mode: vertical-rl;
  color: var(--muted);
  font: 9px "DM Mono", monospace;
  letter-spacing: 2px;
}

.scroll-down span {
  color: var(--green);
  animation: bounce 1.5s infinite;
}

.hero-footer {
  position: absolute;
  bottom: 28px;
  left: 7%;
  right: 7%;
  display: flex;
  justify-content: space-between;
  color: #788c80;
  font: 9px "DM Mono", monospace;
  letter-spacing: 1px;
}

/* GENERAL SECTIONS */

section.content-section {
  position: relative;
  padding: 110px 10%;
}

.section-label {
  display: flex;
  justify-content: space-between;
  gap: 15px;
  padding-bottom: 17px;
  margin-bottom: 55px;
  border-bottom: 1px solid var(--line);
  color: var(--green);
  font: 10px "DM Mono", monospace;
  letter-spacing: 1.5px;
}

.section-label span:last-child {
  color: #75877c;
  text-align: right;
}

h2 {
  font-size: clamp(43px, 7vw, 82px);
  line-height: 1;
  letter-spacing: -.07em;
}

h2 em {
  color: var(--green);
  font-style: normal;
}

.kicker {
  margin-bottom: 22px;
  color: var(--green);
  font: 10px "DM Mono", monospace;
  letter-spacing: 2px;
}

.description {
  color: var(--muted);
  font-size: 14px;
  line-height: 1.95;
  max-width: 570px;
  margin-top: 25px;
}

.reveal {
  opacity: 0;
  transform: translateY(35px);
  transition: opacity .8s ease, transform .8s ease;
}

.reveal.visible {
  opacity: 1;
  transform: translateY(0);
}

/* ABOUT */

.about-layout {
  display: grid;
  grid-template-columns: 1.1fr .9fr;
  gap: 70px;
  align-items: center;
}

.profile-wrap {
  min-height: 330px;
  display: grid;
  place-items: center;
  position: relative;
}

.profile-ring {
  position: absolute;
  width: min(290px, 75vw);
  aspect-ratio: 1;
  border-radius: 50%;
  border: 1px solid rgba(108,255,185,.35);
  box-shadow: 0 0 45px rgba(0,255,150,.08), inset 0 0 45px rgba(0,255,150,.05);
  animation: rotateRing 15s linear infinite;
}

.profile-ring::before,
.profile-ring::after {
  content: "";
  position: absolute;
  inset: 14px;
  border-radius: 50%;
  border: 1px dashed rgba(100,231,255,.3);
}

.profile-ring::after {
  inset: -13px;
  border: 1px solid rgba(100,231,255,.15);
}

.profile-placeholder {
  width: 185px;
  height: 185px;
  border-radius: 50%;
  background: radial-gradient(circle at 35% 30%, #174a37, #07110c 70%);
  border: 2px solid var(--green);
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 13px;
  color: var(--green);
  box-shadow: 0 0 50px rgba(108,255,185,.15);
  animation: float 5s ease-in-out infinite;
}

.profile-placeholder strong {
  font-size: 25px;
  letter-spacing: -1px;
}

.profile-placeholder small {
  color: #9eb8a8;
  font: 8px "DM Mono", monospace;
  letter-spacing: 1px;
}

/* PROJECTS */

.projects {
  background: rgba(5,12,8,.55);
}

.projects-intro {
  display: flex;
  align-items: end;
  justify-content: space-between;
  gap: 30px;
  margin-bottom: 40px;
}

.project-grid {
  display: grid;
  grid-template-columns: repeat(2, minmax(0,1fr));
  gap: 20px;
}

.project {
  position: relative;
  overflow: hidden;
  padding: 25px;
  min-height: 235px;
  background: rgba(12,24,17,.7);
  border: 1px solid var(--line);
  transition: .35s;
}

.project:hover {
  border-color: rgba(108,255,185,.65);
  transform: translateY(-5px);
  background: rgba(13,34,22,.8);
}

.project-number {
  color: #6e8979;
  font: 10px "DM Mono", monospace;
}

.project-icon {
  position: absolute;
  top: 20px;
  right: 22px;
  color: var(--green);
  font-size: 28px;
}

.project h3 {
  margin-top: 50px;
  font-size: 23px;
  letter-spacing: -.7px;
  text-transform: capitalize;
  overflow-wrap: anywhere;
}

.project p {
  margin-top: 12px;
  color: var(--muted);
  font-size: 12px;
  line-height: 1.8;
}

.project a {
  display: inline-block;
  margin-top: 20px;
  color: var(--green);
  font: 10px "DM Mono", monospace;
  letter-spacing: 1px;
}

.project-note {
  margin-top: 25px;
  color: #7f9487;
  font-size: 11px;
  line-height: 1.8;
}

/* SKILLS */

.skills-layout {
  display: grid;
  grid-template-columns: .8fr 1.2fr;
  gap: 75px;
}

.skill-list {
  border-top: 1px solid var(--line);
}

.skill {
  display: flex;
  align-items: center;
  gap: 18px;
  padding: 18px 5px;
  border-bottom: 1px solid var(--line);
  transition: .3s;
}

.skill:hover {
  padding-left: 14px;
  color: var(--green);
}

.skill span:first-child {
  color: var(--green);
  font: 10px "DM Mono", monospace;
}

.skill strong {
  font-size: 15px;
  font-weight: 600;
}

.skill small {
  margin-left: auto;
  color: #778b7e;
  font: 9px "DM Mono", monospace;
}

/* CONTACT */

.contact {
  overflow: hidden;
}

.contact::before {
  content: "";
  position: absolute;
  width: 500px;
  height: 500px;
  right: -250px;
  top: 0;
  border-radius: 50%;
  background: rgba(0,255,153,.08);
  filter: blur(100px);
  pointer-events: none;
}

.contact-email {
  display: inline-block;
  margin-top: 35px;
  padding-bottom: 12px;
  border-bottom: 1px solid rgba(108,255,185,.5);
  color: var(--green);
  font-size: clamp(14px, 2vw, 21px);
  overflow-wrap: anywhere;
}

.social-links {
  display: flex;
  flex-wrap: wrap;
  gap: 12px;
  margin-top: 55px;
}

.social-links a {
  display: inline-flex;
  gap: 10px;
  align-items: center;
  padding: 14px 17px;
  border: 1px solid var(--line);
  color: #c4d3c9;
  font: 10px "DM Mono", monospace;
  letter-spacing: 1px;
  transition: .3s;
}

.social-links a:hover {
  border-color: var(--green);
  color: var(--green);
}

footer {
  padding: 30px 10%;
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 15px;
  border-top: 1px solid var(--line);
  color: #74877a;
  font: 9px "DM Mono", monospace;
  letter-spacing: 1px;
}

/* ANIMATIONS */

@keyframes letterIn {
  from { opacity: 0; transform: translateY(35px) rotateX(-35deg); }
  to { opacity: 1; transform: translateY(0) rotateX(0); }
}

@keyframes fadeUp {
  from { opacity: 0; transform: translateY(20px); }
  to { opacity: 1; transform: translateY(0); }
}

@keyframes gradientFlow {
  to { background-position: 250% center; }
}

@keyframes gridMove {
  to { background-position: 55px 55px; }
}

@keyframes glowMove {
  to { transform: translate(-70px, 50px) scale(1.2); }
}

@keyframes rotateRing {
  to { transform: rotate(360deg); }
}

@keyframes float {
  0%,100% { transform: translateY(0); }
  50% { transform: translateY(-12px); }
}

@keyframes bounce {
  0%,100% { transform: translateY(0); }
  50% { transform: translateY(7px); }
}

@keyframes blink {
  50% { opacity: .35; }
}

/* MOBILE */

@media(max-width: 850px) {
  header {
    padding: 18px 6%;
    min-height: 68px;
  }

  .menu {
    display: block;
  }

  nav {
    position: absolute;
    top: 68px;
    left: 0;
    width: 100%;
    display: none;
    flex-direction: column;
    align-items: stretch;
    gap: 0;
    padding: 15px 6% 25px;
    background: rgba(4,10,7,.97);
    border-bottom: 1px solid var(--line);
  }

  nav.open {
    display: flex;
  }

  nav a {
    padding: 16px 0;
    border-bottom: 1px solid rgba(255,255,255,.06);
  }

  nav .nav-cta {
    width: fit-content;
    padding: 12px 15px;
    margin-top: 12px;
    border: 1px solid rgba(108,255,185,.45);
  }

  .hero {
    padding: 120px 7% 130px;
  }

  .hero h1 {
    font-size: clamp(64px, 15vw, 115px);
  }

  .scroll-down {
    display: none;
  }

  .about-layout,
  .skills-layout {
    grid-template-columns: 1fr;
    gap: 45px;
  }

  section.content-section {
    padding: 85px 7%;
  }

  .profile-wrap {
    min-height: 300px;
  }

  .hero-footer {
    left: 7%;
    right: 7%;
    font-size: 7px;
    gap: 15px;
  }

  .hero-footer span:last-child {
    text-align: right;
  }

  footer {
    padding: 25px 7%;
    flex-wrap: wrap;
  }
}

@media(max-width: 520px) {
  .hero {
    min-height: 850px;
    min-height: 100svh;
  }

  .hero h1 {
    font-size: clamp(61px, 17vw, 90px);
  }

  .eyebrow {
    font-size: 8px;
    letter-spacing: 1px;
  }

  .roles {
    gap: 9px;
    font-size: 10px;
    line-height: 1.7;
  }

  .tagline {
    font-size: 17px;
  }

  .btn {
    padding: 14px 12px;
    gap: 9px;
    font-size: 9px;
  }

  section.content-section {
    padding: 75px 6%;
  }

  .section-label {
    font-size: 9px;
    margin-bottom: 40px;
  }

  .section-label span:last-child {
    font-size: 7px;
  }

  .projects-intro {
    display: block;
  }

  .project-grid {
    grid-template-columns: 1fr;
  }

  .project {
    min-height: 210px;
    padding: 20px;
  }

  .project h3 {
    font-size: 21px;
  }

  .skill small {
    font-size: 8px;
  }

  .social-links a {
    padding: 12px;
    font-size: 9px;
  }

  footer {
    font-size: 8px;
  }
}

@media(prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: .01ms !important;
    animation-iteration-count: 1 !important;
    scroll-behavior: auto !important;
    transition-duration: .01ms !important;
  }
}
</style>
</head>

<body>

<div class="background">
  <div class="grid"></div>
  <div class="glow one"></div>
  <div class="glow two"></div>
  <canvas id="particles"></canvas>
</div>

<header id="header">
  <a href="#home" class="logo">DINESH<span>.</span>REDDY</a>

  <button class="menu" id="menuButton" aria-label="Toggle navigation"
    aria-expanded="false">☰</button>

  <nav id="navigation" aria-label="Main navigation">
    <a href="#home">HOME</a>
    <a href="#about">ABOUT</a>
    <a href="#projects">PROJECTS</a>
    <a href="#skills">SKILLS</a>
    <a href="#contact">CONTACT</a>
    <a href="#contact" class="nav-cta">LET'S TALK ↗</a>
  </nav>
</header>

<main>

  <!-- HERO -->

  <section class="hero" id="home">
    <div class="hero-content">

      <div class="eyebrow">
        <span class="dot"></span>
        CREATIVE TECHNOLOGY & DIGITAL EXPERIENCES
      </div>

      <h1 id="heroTitle">
        <span class="letter" style="animation-delay:.1s">D</span><span class="letter" style="animation-delay:.16s">I</span><span class="letter" style="animation-delay:.22s">N</span><span class="letter" style="animation-delay:.28s">E</span><span class="letter" style="animation-delay:.34s">S</span><span class="letter" style="animation-delay:.4s">H</span>
        <br>
        <span class="gradient-text">REDDY.</span>
      </h1>

      <div class="roles">
        <span>Creative Developer</span>
        <span>AI Image & Video Creator</span>
        <span>Interactive Experience Designer</span>
      </div>

      <p class="tagline">
        BUILD IDEAS.<br>
        <span>CREATE EXPERIENCES.</span><br>
        EXPLORE THE FUTURE.
      </p>

      <div class="actions">
        <a class="btn primary" href="#projects">EXPLORE MY WORK ↘</a>
        <a class="btn secondary" href="mailto:dineshreddyd22@gmail.com">CONTACT ME ↗</a>
      </div>

    </div>

    <a href="#about" class="scroll-down">SCROLL TO EXPLORE <span>↓</span></a>

    <div class="hero-footer">
      <span>DESIGN / CODE / MOTION</span>
      <span>BUILDING ONE IDEA AT A TIME</span>
    </div>
  </section>

  <!-- ABOUT -->

  <section class="content-section" id="about">
    <div class="section-label">
      <span>01 — ABOUT</span>
      <span>THE PERSON BEHIND THE PIXELS</span>
    </div>

    <div class="about-layout">
      <div class="reveal">
        <p class="kicker">CURIOUS BY NATURE. CREATIVE BY DESIGN.</p>

        <h2>I make digital<br>things feel <em>alive.</em></h2>

        <p class="description">
          I'm Dinesh Reddy — a creative developer interested in web
          development, AI-powered image and video creation, 3D design,
          and interactive digital experiences.
        </p>

        <p class="description">
          I enjoy exploring the intersection of technology and visual
          storytelling to create digital experiences that feel engaging,
          expressive, and thoughtfully designed.
        </p>

        <a class="btn secondary" style="margin-top:28px"
           href="https://github.com/dineshreddyd22-cyber"
           target="_blank" rel="noopener noreferrer">
          EXPLORE MY GITHUB ↗
        </a>
      </div>

      <div class="profile-wrap reveal">
        <div class="profile-ring"></div>
        <div class="profile-placeholder">
          <strong>DR.</strong>
          <small>YOUR PHOTO GOES HERE</small>
        </div>
      </div>
    </div>
  </section>

  <!-- PROJECTS -->

  <section class="content-section projects" id="projects">
    <div class="section-label">
      <span>02 — PROJECTS</span>
      <span>EXPLORATION IN PROGRESS</span>
    </div>

    <div class="projects-intro reveal">
      <div>
        <p class="kicker">MADE WITH CURIOSITY</p>
        <h2>Ideas into<br><em>experiences.</em></h2>
      </div>

      <p class="description">
        Explore my public GitHub repositories. The live list below
        loads actual repository data when the GitHub API is available.
      </p>
    </div>

    <div class="project-grid" id="projectGrid">
      <article class="project">
        <span class="project-number">CONNECTING TO GITHUB...</span>
        <span class="project-icon">↗</span>
        <h3>Loading repositories</h3>
        <p>Fetching publicly available repository information.</p>
      </article>
    </div>

    <p class="project-note" id="projectStatus" aria-live="polite">
      Repository data is retrieved from the public GitHub API.
    </p>

    <a class="btn secondary" style="margin-top:30px"
       href="https://github.com/dineshreddyd22-cyber"
       target="_blank" rel="noopener noreferrer">
      VIEW ALL GITHUB REPOSITORIES ↗
    </a>
  </section>

  <!-- SKILLS -->

  <section class="content-section" id="skills">
    <div class="section-label">
      <span>03 — TOOLKIT</span>
      <span>LEARNING / BUILDING / EXPLORING</span>
    </div>

    <div class="skills-layout">
      <div class="reveal">
        <p class="kicker">TECH MEETS IMAGINATION</p>
        <h2>Tools for<br><em>possibility.</em></h2>
        <p class="description">
          A growing technology toolkit for experimenting with interfaces,
          creative development, and digital experiences. This is not a
          claim of expert proficiency in every listed technology.
        </p>
      </div>

      <div class="skill-list reveal">
        <div class="skill"><span>01</span><strong>HTML & CSS</strong><small>
