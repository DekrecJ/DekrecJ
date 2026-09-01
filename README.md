<!doctype html>
<html lang="es">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <meta name="description" content="DANTE//BUILD — Software, inteligencia artificial, automatización y mecatrónica.">
  <title>DANTE//BUILD</title>
  <style>
    :root {
      --ink: #111;
      --paper: #f4f1e8;
      --muted: #77746d;
      --line: 2px;
      --cell: 8px;
      --max: 1120px;
    }

    * { box-sizing: border-box; }
    html { scroll-behavior: smooth; }
    body {
      margin: 0;
      color: var(--ink);
      background-color: var(--paper);
      background-image:
        linear-gradient(rgba(17,17,17,.045) 1px, transparent 1px),
        linear-gradient(90deg, rgba(17,17,17,.045) 1px, transparent 1px);
      background-size: var(--cell) var(--cell);
      font-family: "Courier New", Courier, monospace;
      font-weight: 700;
      image-rendering: pixelated;
    }

    a { color: inherit; text-decoration-thickness: 2px; text-underline-offset: 4px; }
    button, a { -webkit-tap-highlight-color: transparent; }
    ::selection { color: var(--paper); background: var(--ink); }

    .shell { width: min(calc(100% - 32px), var(--max)); margin: 16px auto 48px; }
    .frame { border: var(--line) solid var(--ink); background: var(--paper); box-shadow: 8px 8px 0 var(--ink); }

    .topbar {
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 16px;
      padding: 12px 16px;
      border-bottom: var(--line) solid var(--ink);
      font-size: 13px;
    }

    .lights { display: flex; gap: 8px; }
    .light { width: 10px; height: 10px; border: var(--line) solid var(--ink); }
    .light:first-child { background: var(--ink); }

    nav { display: flex; flex-wrap: wrap; gap: 16px; }
    nav a { text-decoration: none; }
    nav a:hover, nav a:focus-visible { color: var(--paper); background: var(--ink); outline: 4px solid var(--ink); }

    .hero {
      display: grid;
      grid-template-columns: 1.45fr .75fr;
      min-height: 520px;
      border-bottom: var(--line) solid var(--ink);
    }

    .hero-copy { display: flex; flex-direction: column; justify-content: center; padding: clamp(28px, 6vw, 72px); }
    .eyebrow { margin: 0 0 20px; font-size: 13px; letter-spacing: .12em; }
    h1 { margin: 0; font-size: clamp(54px, 10vw, 126px); line-height: .8; letter-spacing: -.09em; }
    h1 span { display: block; margin-left: .48em; -webkit-text-stroke: 2px var(--ink); color: transparent; }
    .lead { max-width: 640px; margin: 32px 0 0; font-size: clamp(16px, 2vw, 21px); line-height: 1.5; }
    .actions { display: flex; flex-wrap: wrap; gap: 12px; margin-top: 32px; }

    .button {
      display: inline-block;
      padding: 12px 16px;
      border: var(--line) solid var(--ink);
      background: var(--paper);
      text-decoration: none;
      box-shadow: 4px 4px 0 var(--ink);
    }
    .button.primary { color: var(--paper); background: var(--ink); box-shadow: 4px 4px 0 var(--muted); }
    .button:hover { transform: translate(4px, 4px); box-shadow: none; }

    .hero-art { position: relative; overflow: hidden; border-left: var(--line) solid var(--ink); background: var(--ink); color: var(--paper); }
    .mountain { position: absolute; bottom: 0; width: 0; height: 0; border-left: 170px solid transparent; border-right: 170px solid transparent; border-bottom: 260px solid var(--paper); }
    .mountain.one { left: -95px; }
    .mountain.two { right: -100px; transform: scale(.82); transform-origin: bottom; opacity: .72; }
    .sun { position: absolute; top: 78px; left: 50%; width: 88px; height: 88px; transform: translateX(-50%); border: 12px solid var(--paper); }
    .pixel-path { position: absolute; bottom: 0; left: 50%; width: 50px; height: 190px; transform: translateX(-50%); background: var(--ink); clip-path: polygon(42% 0,58% 0,100% 100%,0 100%); }
    .coordinates { position: absolute; right: 16px; bottom: 16px; font-size: 11px; writing-mode: vertical-rl; }

    .ticker { overflow: hidden; border-bottom: var(--line) solid var(--ink); white-space: nowrap; }
    .ticker-track { display: inline-block; padding: 12px 0; animation: scroll 22s linear infinite; }
    .ticker span { margin-right: 28px; }
    @keyframes scroll { to { transform: translateX(-50%); } }
    @media (prefers-reduced-motion: reduce) { html { scroll-behavior: auto; } .ticker-track { animation: none; } }

    section { padding: clamp(28px, 5vw, 56px); border-bottom: var(--line) solid var(--ink); }
    .section-head { display: flex; align-items: flex-end; justify-content: space-between; gap: 20px; margin-bottom: 28px; }
    h2 { margin: 0; font-size: clamp(30px, 5vw, 54px); letter-spacing: -.07em; }
    .index { font-size: 13px; }

    .project-grid { display: grid; grid-template-columns: repeat(2, 1fr); border-top: var(--line) solid var(--ink); border-left: var(--line) solid var(--ink); }
    .project { min-height: 280px; padding: 24px; border-right: var(--line) solid var(--ink); border-bottom: var(--line) solid var(--ink); transition: background .12s, color .12s; }
    .project:hover { color: var(--paper); background: var(--ink); }
    .project-number { display: block; margin-bottom: 40px; font-size: 12px; }
    .project h3 { margin: 0 0 14px; font-size: clamp(22px, 3vw, 32px); }
    .project p { min-height: 72px; margin: 0 0 24px; line-height: 1.5; }
    .tags { display: flex; flex-wrap: wrap; gap: 7px; }
    .tag { padding: 5px 7px; border: var(--line) solid currentColor; font-size: 11px; }

    .stack-grid { display: grid; grid-template-columns: repeat(3, 1fr); border-top: var(--line) solid var(--ink); }
    .stack-group { padding: 22px; border-right: var(--line) solid var(--ink); border-bottom: var(--line) solid var(--ink); }
    .stack-group:nth-child(3n) { border-right: 0; }
    .stack-group h3 { margin: 0 0 18px; font-size: 13px; }
    .stack-group ul { margin: 0; padding: 0; list-style: square inside; line-height: 1.8; }

    .protocol { display: grid; grid-template-columns: repeat(5, 1fr); }
    .protocol div { position: relative; min-height: 140px; padding: 20px; border: var(--line) solid var(--ink); border-right: 0; }
    .protocol div:last-child { border-right: var(--line) solid var(--ink); }
    .protocol strong { display: block; margin-bottom: 42px; font-size: 28px; }

    footer { display: grid; grid-template-columns: 1fr auto; align-items: flex-end; gap: 24px; padding: 32px; }
    footer p { margin: 6px 0 0; }
    .status { display: inline-flex; align-items: center; gap: 9px; padding: 8px 10px; border: var(--line) solid var(--ink); }
    .status::before { content: ""; width: 10px; height: 10px; background: var(--ink); animation: blink 1.4s steps(1) infinite; }
    @keyframes blink { 50% { opacity: 0; } }

    @media (max-width: 760px) {
      .shell { width: min(calc(100% - 20px), var(--max)); margin-top: 10px; }
      .frame { box-shadow: 5px 5px 0 var(--ink); }
      .topbar { align-items: flex-start; flex-direction: column; }
      .hero { grid-template-columns: 1fr; }
      .hero-art { min-height: 330px; border-top: var(--line) solid var(--ink); border-left: 0; }
      .project-grid, .stack-grid { grid-template-columns: 1fr; }
      .stack-group, .stack-group:nth-child(3n) { border-right: var(--line) solid var(--ink); }
      .protocol { grid-template-columns: 1fr; }
      .protocol div { min-height: auto; border-right: var(--line) solid var(--ink); border-bottom: 0; }
      .protocol div:last-child { border-bottom: var(--line) solid var(--ink); }
      footer { grid-template-columns: 1fr; }
    }
  </style>
</head>
<body>
  <main class="shell">
    <div class="frame">
      <header class="topbar">
        <div class="lights" aria-hidden="true"><i class="light"></i><i class="light"></i><i class="light"></i></div>
        <nav aria-label="Navegación principal">
          <a href="#projects">[01] PROYECTOS</a>
          <a href="#stack">[02] STACK</a>
          <a href="#process">[03] PROCESO</a>
          <a href="#contact">[04] CONTACTO</a>
        </nav>
      </header>

      <div class="hero">
        <div class="hero-copy">
          <p class="eyebrow">SOFTWARE × AI × AUTOMATION × ENGINEERING</p>
          <h1>DANTE<span>BUILD</span></h1>
          <p class="lead">Construyo sistemas útiles donde el software se conecta con procesos reales. Ideas en bloques, seguridad desde el inicio y pruebas antes de publicar.</p>
          <div class="actions">
            <a class="button primary" href="#projects">VER PROYECTOS ↓</a>
            <a class="button" href="https://github.com/TU_USUARIO">GITHUB ↗</a>
          </div>
        </div>
        <div class="hero-art" aria-label="Paisaje pixel monocromático">
          <i class="sun"></i><i class="mountain one"></i><i class="mountain two"></i><i class="pixel-path"></i>
          <span class="coordinates">-2.1709 / -79.9224 / ECUADOR</span>
        </div>
      </div>

      <div class="ticker" aria-hidden="true"><div class="ticker-track">
        <span>VIBE CODING // BUILD FAST</span><span>AI ORCHESTRATION</span><span>DENTAL TECHNOLOGY</span><span>MECHATRONICS</span><span>SECURE BY DESIGN</span>
        <span>VIBE CODING // BUILD FAST</span><span>AI ORCHESTRATION</span><span>DENTAL TECHNOLOGY</span><span>MECHATRONICS</span><span>SECURE BY DESIGN</span>
      </div></div>

      <section id="projects">
        <div class="section-head"><h2>SELECTED BUILDS</h2><span class="index">01/04</span></div>
        <div class="project-grid">
          <article class="project"><span class="project-number">PROJECT_01</span><h3>AI ORCHESTRATOR</h3><p>Orquesta multiagente que coordina modelos locales y remotos para programar, probar y automatizar.</p><div class="tags"><span class="tag">FASTAPI</span><span class="tag">TEMPORAL</span><span class="tag">OLLAMA</span><span class="tag">DOCKER</span></div></article>
          <article class="project"><span class="project-number">PROJECT_02</span><h3>DENTAL LAB ERP/CRM</h3><p>Gestión de clientes, casos, producción, inventario, finanzas, entregas y trazabilidad.</p><div class="tags"><span class="tag">TYPESCRIPT</span><span class="tag">POSTGRESQL</span><span class="tag">TAILWIND</span></div></article>
          <article class="project"><span class="project-number">PROJECT_03</span><h3>ODONTOFLOW MOBILE</h3><p>Aplicación móvil clínica con acceso protegido, flujos por roles y datos reales del backend.</p><div class="tags"><span class="tag">FLUTTER</span><span class="tag">SUPABASE</span><span class="tag">RLS</span></div></article>
          <article class="project"><span class="project-number">PROJECT_04</span><h3>ENGINEERING SIMULATOR</h3><p>Simulación accesible de motores, servos, barras, uniones, materiales y niveles de riesgo.</p><div class="tags"><span class="tag">3D</span><span class="tag">MECHANICS</span><span class="tag">FEA</span></div></article>
          <article class="project"><span class="project-number">PROJECT_05</span><h3>AUTOMATION LAB</h3><p>Agentes y flujos para soporte, agenda y operaciones conectados mediante APIs reutilizables.</p><div class="tags"><span class="tag">N8N</span><span class="tag">APIs</span><span class="tag">AI AGENTS</span></div></article>
          <article class="project"><span class="project-number">PROJECT_06</span><h3>INDUSTRIAL CONTROL</h3><p>Automatización PLC con sensores, actuadores, HMI, recetas y regulación PID.</p><div class="tags"><span class="tag">S7-1500</span><span class="tag">IEC 61131-3</span><span class="tag">HMI</span></div></article>
        </div>
      </section>

      <section id="stack">
        <div class="section-head"><h2>TOOLBOX</h2><span class="index">02/04</span></div>
        <div class="stack-grid">
          <div class="stack-group"><h3>// LANGUAGES</h3><ul><li>Dart</li><li>Python</li><li>TypeScript</li><li>SQL</li></ul></div>
          <div class="stack-group"><h3>// INTERFACES</h3><ul><li>Flutter</li><li>React</li><li>Tailwind</li><li>shadcn/ui</li></ul></div>
          <div class="stack-group"><h3>// BACKEND</h3><ul><li>FastAPI</li><li>PostgreSQL</li><li>Supabase</li><li>REST APIs</li></ul></div>
          <div class="stack-group"><h3>// AI</h3><ul><li>Ollama</li><li>Multi-agent</li><li>RAG</li><li>Automation</li></ul></div>
          <div class="stack-group"><h3>// OPERATIONS</h3><ul><li>Linux</li><li>Docker</li><li>Temporal</li><li>n8n</li></ul></div>
          <div class="stack-group"><h3>// ENGINEERING</h3><ul><li>PLC / HMI</li><li>PID</li><li>CAD/CAM</li><li>3D Printing</li></ul></div>
        </div>
      </section>

      <section id="process">
        <div class="section-head"><h2>BUILD PROTOCOL</h2><span class="index">03/04</span></div>
        <div class="protocol"><div><strong>01</strong>DEFINE</div><div><strong>02</strong>DESIGN</div><div><strong>03</strong>BUILD</div><div><strong>04</strong>TEST</div><div><strong>05</strong>SHIP</div></div>
      </section>

      <footer id="contact">
        <div><strong>DANTE//BUILD</strong><p>IDEAS EN BLOQUES. · ECUADOR · 2026</p></div>
        <a class="status" href="mailto:TU_CORREO">DISPONIBLE PARA CREAR</a>
      </footer>
    </div>
  </main>
</body>
</html>
