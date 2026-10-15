import { useEffect, useRef, useState } from "react";
import * as THREE from "three";

const VIDEO =
  "https://videos.pexels.com/video-files/3129671/3129671-hd_1920_1080_25fps.mp4";

const projects = [
  {
    title: "AI Creative Studio",
    category: "ARTIFICIAL INTELLIGENCE",
    description:
      "An experimental concept for AI-powered visual creativity.",
    image:
      "https://images.unsplash.com/photo-1677442136019-21780ecad995?auto=format&fit=crop&w=1000&q=85",
    url: "https://github.com/dineshreddyd22-cyber",
  },
  {
    title: "Interactive Web Experience",
    category: "WEB DEVELOPMENT",
    description:
      "A concept for immersive, responsive digital experiences.",
    image:
      "https://images.unsplash.com/photo-1461749280684-dccba630e2f6?auto=format&fit=crop&w=1000&q=85",
    url: "https://github.com/dineshreddyd22-cyber",
  },
  {
    title: "Digital Dimensions",
    category: "3D AND CREATIVE DESIGN",
    description:
      "Exploring motion, digital environments, and visual design.",
    image:
      "https://images.unsplash.com/photo-1634017839464-5c339ebe3cb4?auto=format&fit=crop&w=1000&q=85",
    url: "https://github.com/dineshreddyd22-cyber",
  },
];

const skills = [
  "HTML",
  "CSS",
  "JavaScript",
  "TypeScript",
  "React",
  "Python",
  "Three.js",
  "Git",
  "AI Creativity",
  "3D Design",
];

function ThreeBackground() {
  const mountRef = useRef<HTMLDivElement>(null);

  useEffect(() => {
    const container = mountRef.current;
    if (!container) return;

    let renderer: THREE.WebGLRenderer;

    try {
      renderer = new THREE.WebGLRenderer({
        alpha: true,
        antialias: false,
        powerPreference: "low-power",
      });
    } catch {
      return;
    }

    renderer.setPixelRatio(Math.min(window.devicePixelRatio, 1.5));
    renderer.setSize(container.clientWidth, container.clientHeight);
    container.appendChild(renderer.domElement);

    const scene = new THREE.Scene();

    const camera = new THREE.PerspectiveCamera(
      55,
      container.clientWidth / container.clientHeight,
      0.1,
      100
    );

    camera.position.z = 12;

    const count = window.innerWidth < 700 ? 450 : 1000;
    const positions = new Float32Array(count * 3);

    for (let i = 0; i < count; i++) {
      positions[i * 3] = (Math.random() - 0.5) * 24;
      positions[i * 3 + 1] = (Math.random() - 0.5) * 16;
      positions[i * 3 + 2] = (Math.random() - 0.5) * 15;
    }

    const geometry = new THREE.BufferGeometry();
    geometry.setAttribute(
      "position",
      new THREE.BufferAttribute(positions, 3)
    );

    const material = new THREE.PointsMaterial({
      color: 0x63ffc2,
      size: 0.035,
      transparent: true,
      opacity: 0.8,
      blending: THREE.AdditiveBlending,
      depthWrite: false,
    });

    const particles = new THREE.Points(geometry, material);
    scene.add(particles);

    const group = new THREE.Group();
    scene.add(group);

    for (let i = 0; i < 3; i++) {
      const shape = new THREE.IcosahedronGeometry(1.3 + i * 0.5, 1);

      const wireframe = new THREE.MeshBasicMaterial({
        color: i % 2 === 0 ? 0x00ff99 : 0x31bfff,
        wireframe: true,
        transparent: true,
        opacity: 0.15 - i * 0.025,
      });

      const mesh = new THREE.Mesh(shape, wireframe);
      mesh.position.set(4.2, 0, -i * 0.8);
      group.add(mesh);
    }

    let frame = 0;
    let animationId = 0;
    let pointerX = 0;
    let pointerY = 0;
    let visible = true;

    const reducedMotion = window.matchMedia(
      "(prefers-reduced-motion: reduce)"
    ).matches;

    const onPointerMove = (event: PointerEvent) => {
      pointerX = (event.clientX / window.innerWidth - 0.5) * 0.6;
      pointerY = (event.clientY / window.innerHeight - 0.5) * 0.4;
    };

    const observer = new IntersectionObserver(([entry]) => {
      visible = entry.isIntersecting;

      if (visible && !reducedMotion && !animationId) {
        animate();
      }
    });

    observer.observe(container);

    function animate() {
      if (!visible || reducedMotion) {
        animationId = 0;
        renderer.render(scene, camera);
        return;
      }

      animationId = requestAnimationFrame(animate);
      frame += 0.003;

      particles.rotation.y = frame * 0.12;
      particles.rotation.x = Math.sin(frame) * 0.08;

      group.rotation.y +=
        (pointerX - group.rotation.y) * 0.015;

      group.rotation.x +=
        (pointerY - group.rotation.x) * 0.015;

      renderer.render(scene, camera);
    }

    const resize = () => {
      if (!container.clientWidth || !container.clientHeight) return;

      camera.aspect =
        container.clientWidth / container.clientHeight;

      camera.updateProjectionMatrix();

      renderer.setSize(
        container.clientWidth,
        container.clientHeight
      );
    };

    window.addEventListener("resize", resize);
    window.addEventListener("pointermove", onPointerMove);

    if (reducedMotion) {
      renderer.render(scene, camera);
    } else {
      animate();
    }

    return () => {
      cancelAnimationFrame(animationId);
      observer.disconnect();

      window.removeEventListener("resize", resize);
      window.removeEventListener("pointermove", onPointerMove);

      geometry.dispose();
      material.dispose();

      group.traverse((object) => {
        if (object instanceof THREE.Mesh) {
          object.geometry.dispose();
          const mat = object.material;
          if (Array.isArray(mat)) mat.forEach((m) => m.dispose());
          else mat.dispose();
        }
      });

      renderer.dispose();
      renderer.domElement.remove();
    };
  }, []);

  return <div ref={mountRef} className="three-background" />;
}

export default function App() {
  const [menuOpen, setMenuOpen] = useState(false);
  const [videoFailed, setVideoFailed] = useState(false);

  useEffect(() => {
    document.title = "Dinesh Reddy — Creative Developer";
  }, []);

  return (
    <main>
      <style>{`
        @import url('https://fonts.googleapis.com/css2?family=DM+Mono:wght@400;500&family=Space+Grotesk:wght@400;500;600;700&display=swap');

        :root {
          color-scheme: dark;
          --bg: #070a09;
          --green: #63ffc2;
          --muted: #9ba7a2;
          --line: rgba(255,255,255,.12);
        }

        * { box-sizing: border-box; }

        html {
          scroll-behavior: smooth;
          scroll-padding-top: 85px;
          background: var(--bg);
        }

        body {
          margin: 0;
          color: #f5f7f6;
          font-family: 'Space Grotesk', sans-serif;
          background: var(--bg);
        }

        a { color: inherit; text-decoration: none; }

        button { font: inherit; }

        .nav {
          position: fixed;
          z-index: 20;
          top: 0;
          left: 0;
          width: 100%;
          display: flex;
          justify-content: space-between;
          align-items: center;
          padding: 22px 7%;
          background: rgba(7,10,9,.76);
          backdrop-filter: blur(18px);
          border-bottom: 1px solid var(--line);
        }

        .logo {
          font-size: 18px;
          font-weight: 700;
          letter-spacing: -1px;
        }

        .logo span { color: var(--green); }

        .nav-links {
          display: flex;
          gap: 26px;
          align-items: center;
          font: 11px 'DM Mono', monospace;
          color: #c1cbc6;
        }

        .nav-links a:hover { color: var(--green); }

        .menu-btn {
          display: none;
          background: transparent;
          border: 1px solid var(--line);
          color: white;
          padding: 8px 12px;
        }

        .hero {
          min-height: 100svh;
          position: relative;
          display: flex;
          align-items: center;
          padding: 145px 9% 90px;
          overflow: hidden;
          isolation: isolate;
        }

        .hero-video, .video-shade, .three-background {
          position: absolute;
          inset: 0;
          width: 100%;
          height: 100%;
          pointer-events: none;
        }

        .hero-video {
          z-index: -3;
          object-fit: cover;
          opacity: .48;
        }

        .video-shade {
          z-index: -2;
          background:
            linear-gradient(90deg,rgba(7,10,9,.97),rgba(7,10,9,.68) 58%,rgba(7,10,9,.4)),
            linear-gradient(0deg,#070a09,transparent 35%,rgba(7,10,9,.15));
        }

        .three-background { z-index: -1; }

        .three-background canvas {
          width: 100%;
          height: 100%;
          display: block;
        }

        .hero-content {
          width: 100%;
          max-width: 900px;
          animation: rise .9s ease both;
        }

        .eyebrow {
          display: flex;
          gap: 12px;
          align-items: center;
          color: var(--green);
          font: 11px 'DM Mono', monospace;
          letter-spacing: 2px;
          text-transform: uppercase;
        }

        .dot {
          width: 7px;
          height: 7px;
          background: var(--green);
          border-radius: 50%;
          box-shadow: 0 0 16px var(--green);
          animation: pulse 1.8s infinite;
        }

        h1 {
          margin: 30px 0 20px;
          font-size: clamp(52px,10vw,120px);
          line-height: .88;
          letter-spacing: -.085em;
          font-weight: 600;
        }

        h1 .accent {
          display: block;
          color: var(--green);
          text-shadow: 0 0 55px rgba(99,255,194,.12);
        }

        .intro {
          max-width: 520px;
          color: #c1cbc6;
          font-size: clamp(15px,2vw,18px);
          line-height: 1.8;
        }

        .actions {
          display: flex;
          flex-wrap: wrap;
          gap: 12px;
          margin-top: 32px;
        }

        .button {
          display: inline-flex;
          align-items: center;
          justify-content: center;
          min-height: 48px;
          padding: 0 22px;
          border: 1px solid var(--line);
          font: 11px 'DM Mono', monospace;
          letter-spacing: 1px;
          transition: .25s;
        }

        .button.primary {
          background: var(--green);
          color: #06100c;
          border-color: var(--green);
          font-weight: 500;
        }

        .button:hover {
          transform: translateY(-3px);
          border-color: var(--green);
        }

        .section {
          padding: 110px 9%;
          border-top: 1px solid var(--line);
        }

        .section-label {
          color: var(--green);
          font: 11px 'DM Mono', monospace;
          letter-spacing: 2px;
        }

        h2 {
          font-size: clamp(36px,6vw,68px);
          letter-spacing: -.06em;
          line-height: 1.05;
          margin: 18px 0 24px;
        }

        .muted {
          color: var(--muted);
          line-height: 1.8;
          max-width: 680px;
        }

        .about-grid {
          display: grid;
          grid-template-columns: 1.1fr .9fr;
          gap: 50px;
          align-items: center;
        }

        .portrait {
          position: relative;
          min-height: 350px;
          overflow: hidden;
          border: 1px solid rgba(99,255,194,.28);
          background: #101714;
          animation: float 6s ease-in-out infinite;
        }

        .portrait img {
          width: 100%;
          height: 390px;
          object-fit: cover;
          opacity: .8;
          display: block;
        }

        .portrait-label {
          position: absolute;
          bottom: 18px;
          left: 18px;
          right: 18px;
          padding: 15px;
          background: rgba(7,10,9,.78);
          backdrop-filter: blur(10px);
          font: 11px 'DM Mono', monospace;
          color: var(--green);
        }

        .project-grid {
          display: grid;
          grid-template-columns: repeat(3,minmax(0,1fr));
          gap: 18px;
          margin-top: 42px;
        }

        .project {
          display: block;
          border: 1px solid var(--line);
          background: #0c100e;
          transition: transform .3s,border-color .3s;
          overflow: hidden;
        }

        .project:hover {
          transform: translateY(-8px);
          border-color: var(--green);
        }

        .project img {
          display: block;
          width: 100%;
          aspect-ratio: 4/3;
          object-fit: cover;
          transition: transform .6s;
        }

        .project:hover img { transform: scale(1.05); }

        .project-body { padding: 22px; }

        .category {
          color: var(--green);
          font: 10px 'DM Mono', monospace;
          letter-spacing: 1px;
        }

        .project h3 {
          font-size: 21px;
          margin: 12px 0;
        }

        .project p {
          color: var(--muted);
          font-size: 13px;
          line-height: 1.7;
        }

        .skills {
          display: flex;
          flex-wrap: wrap;
          gap: 12px;
          margin-top: 30px;
        }

        .skill {
          border: 1px solid var(--line);
          padding: 14px 18px;
          font: 12px 'DM Mono', monospace;
          transition: .25s;
        }

        .skill:hover {
          color: var(--green);
          border-color: var(--green);
          transform: translateY(-4px);
        }

        .contact-box {
          padding: clamp(28px,6vw,65px);
          border: 1px solid rgba(99,255,194,.25);
          background: linear-gradient(130deg,#101a15,#090d0b);
        }

        footer {
          padding: 30px 9%;
          display: flex;
          justify-content: space-between;
          gap: 20px;
          flex-wrap: wrap;
          border-top: 1px solid var(--line);
          color: var(--muted);
          font: 11px 'DM Mono', monospace;
        }

        @keyframes rise {
          from { opacity: 0; transform: translateY(24px); }
          to { opacity: 1; transform: translateY(0); }
        }

        @keyframes pulse {
          50% { opacity: .45; box-shadow: 0 0 4px var(--green); }
        }

        @keyframes float {
          0%,100% { transform: translateY(0); }
          50% { transform: translateY(-8px); }
        }

        @media (max-width: 760px) {
          .nav { padding: 18px 5%; }
          .menu-btn { display: block; }

          .nav-links {
            display: none;
            position: absolute;
            top: 67px;
            left: 0;
            right: 0;
            padding: 22px;
            background: rgba(7,10,9,.97);
            border-bottom: 1px solid var(--line);
            flex-direction: column;
            align-items: flex-start;
          }

          .nav-links.open { display: flex; }

          .hero { padding: 130px 6% 80px; }
          .video-shade {
            background: linear-gradient(90deg,rgba(7,10,9,.91),rgba(7,10,9,.65)),
                        linear-gradient(0deg,#070a09,transparent);
          }

          .section { padding: 75px 6%; }

          .about-grid { grid-template-columns: 1fr; gap: 28px; }

          .portrait img { height: 300px; }

          .project-grid { grid-template-columns: 1fr; }

          .project-body { padding: 20px; }

          footer { padding: 25px 6%; }
        }

        @media (prefers-reduced-motion: reduce) {
          *, *::before, *::after {
            animation-duration: .01ms !important;
            animation-iteration-count: 1 !important;
            scroll-behavior: auto !important;
            transition-duration: .01ms !important;
          }
        }
      `}</style>

      <nav className="nav">
        <a href="#home" className="logo">
          DINESH<span>.</span>REDDY
        </a>

        <button
          className="menu-btn"
          onClick={() => setMenuOpen(!menuOpen)}
          aria-label="Toggle navigation"
          aria-expanded={menuOpen}
        >
          {menuOpen ? "CLOSE" : "MENU"}
        </button>

        <div className={`nav-links ${menuOpen ? "open" : ""}`}>
          {["HOME", "ABOUT", "PROJECTS", "SKILLS", "CONTACT"].map(
            (item) => (
              <a
                key={item}
                href={`#${item.toLowerCase()}`}
                onClick={() => setMenuOpen(false)}
              >
                {item}
              </a>
            )
          )}
        </div>
      </nav>

      <section className="hero" id="home">
        {!videoFailed && (
          <video
            className="hero-video"
            autoPlay
            muted
            loop
            playsInline
            preload="metadata"
            poster="https://images.unsplash.com/photo-1451187580459-43490279c0fa?auto=format&fit=crop&w=1600&q=80"
            onError={() => setVideoFailed(true)}
          >
            <source src={VIDEO} type="video/mp4" />
          </video>
        )}

        <div className="video-shade" />
        <ThreeBackground />

        <div className="hero-content">
          <div className="eyebrow">
            <span className="dot" />
            CREATIVE TECHNOLOGIST · PORTFOLIO 2026
          </div>

          <h1>
            DINESH
            <span className="accent">REDDY.</span>
          </h1>

          <p className="intro">
            I explore the intersection of web development,
            artificial intelligence, creative visuals and
            interactive digital experiences.
          </p>

          <div className="actions">
            <a className="button primary" href="#projects">
              EXPLORE MY WORK ↗
            </a>
            <a className="button" href="#contact">
              LET'S CONNECT
            </a>
          </div>

          <p className="eyebrow" style={{ marginTop: 42 }}>
            WEB DEVELOPER / AI CREATOR / 3D ENTHUSIAST
          </p>
        </div>
      </section>

      <section className="section" id="about">
        <div className="about-grid">
          <div>
            <div className="section-label">01 / ABOUT ME</div>
            <h2>
              BEYOND
              <br />
              THE ORDINARY.
            </h2>

            <p className="muted">
              I'm Dinesh Reddy, a creative developer interested
              in modern web experiences, AI-assisted creativity,
              animation, and interactive design.
            </p>

            <p className="muted">
              I enjoy experimenting with technologies and
              transforming ideas into engaging digital experiences.
            </p>

            <a
              className="button"
              href="https://github.com/dineshreddyd22-cyber"
              target="_blank"
              rel="noreferrer"
            >
              EXPLORE MY GITHUB ↗
            </a>
          </div>

          <div className="portrait">
            <img
              src="https://images.unsplash.com/photo-1634017839464-5c339ebe3cb4?auto=format&fit=crop&w=1000&q=85"
              alt="Abstract digital art portrait placeholder"
              loading="lazy"
            />
            <div className="portrait-label">
              DINESH REDDY — CREATIVE TECHNOLOGIST
            </div>
          </div>
        </div>
      </section>

      <section className="section" id="projects">
        <div className="section-label">02 / SELECTED WORK</div>
        <h2>IDEAS INTO<br />EXPERIENCES.</h2>
        <p className="muted">
          Explore my development and creative interests.
          Replace these concept cards with your actual projects.
        </p>

        <div className="project-grid">
          {projects.map((project, index) => (
            <a
              href={project.url}
              target="_blank"
              rel="noreferrer"
              className="project"
              key={project.title}
            >
              <img
                src={project.image}
                alt={project.title}
          
