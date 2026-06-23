---
format: zopack
version: "1.0"
name: zo-space-backup
author: unknown.zo.computer
routes: 132
exported: 2026-06-23
---

# zo-space-backup

## Routes

### `/` (page, public)

```tsx

```

### `/404` (page, public)

```tsx
import { useState, useEffect } from "react";

export default function NotFound() {
  const [glitch, setGlitch] = useState(false);
  const [cmd, setCmd] = useState("");
  const [output, setOutput] = useState<string[]>([]);
  const [blink, setBlink] = useState(true);

  useEffect(() => {
    const iv = setInterval(() => setBlink(v => !v), 530);
    const giv = setInterval(() => { setGlitch(true); setTimeout(() => setGlitch(false), 150); }, 4000);
    return () => { clearInterval(iv); clearInterval(giv); };
  }, []);

  const exec = () => {
    const c = cmd.trim().toLowerCase();
    const o = [...output, "visitor@zos:~$ " + cmd];
    if (c === "help") o.push("Available:", "  home     - Go to ZOS", "  press    - Open the press kit", "  about    - About the build", "  ls       - List available routes", "  whoami   - Identity check");
    else if (c === "home" || c === "cd ~" || c === "cd /") { window.location.href = "/zos"; return; }
    else if (c === "press" || c === "cd /press") { window.location.href = "/press"; return; }
    else if (c === "about" || c === "cd /about-the-build") { window.location.href = "/about-the-build"; return; }
    else if (c === "ls") o.push("/zos", "/press", "/about-the-build", "/secret", "/trivia", "/zo-city");
    else if (c === "whoami") o.push("Lost traveler. But not for long.");
    else if (c) o.push("zos: route not found. Try 'help'.");
    setOutput(o); setCmd("");
  };

  return (
    <div className="nf">
      <style>{NF_CSS}</style>
      <div className="nf-scan" />
      <div className="nf-vig" />
      <div className="nf-content">
        <div className={"nf-code" + (glitch ? " glitch" : "")}>
          <span className="nf-4">4</span>
          <span className="nf-0">0</span>
          <span className="nf-4b">4</span>
        </div>
        <div className="nf-msg">ROUTE NOT FOUND</div>
        <div className="nf-sub">The page you're looking for doesn't exist in this filesystem.</div>
        <div className="nf-terminal">
          <div className="nf-term-hdr">\u2b1b ZOS Recovery Terminal</div>
          <div className="nf-term-body">
            <div className="nf-term-line">ZOS ERROR: Requested path does not match any known route.</div>
            <div className="nf-term-line">Type 'help' for recovery options.</div>
            <div className="nf-term-line"> </div>
            {output.map((l, i) => <div key={i} className="nf-term-line">{l}</div>)}
            <div className="nf-term-input">
              <span className="nf-prompt">visitor@zos:~$</span>
              <input value={cmd} onChange={e => setCmd(e.target.value)} onKeyDown={e => { if (e.key === "Enter") exec(); }} className="nf-inp" autoFocus />
              <span className="nf-cursor" style={blink ? undefined : {opacity:0}}>\u2588</span>
            </div>
          </div>
        </div>
        <div className="nf-links">
          <a href="/zos" className="nf-link">\u26a1 Enter ZOS</a>
          <a href="/press" className="nf-link">\ud83d\udcf0 Press Kit</a>
          <a href="/about-the-build" className="nf-link">\ud83d\udcd6 About the Build</a>
        </div>
      </div>
    </div>
  );
}

const NF_CSS = [
  "@import url('https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;500;700&family=Space+Grotesk:wght@400;500;600;700&display=swap');",
  "*{box-sizing:border-box;margin:0;padding:0}",
  "body{overflow:hidden;background:#0a0a0d;font-family:'JetBrains Mono',monospace;color:#e8e0d4}",
  ".nf{position:fixed;inset:0;display:flex;align-items:center;justify-content:center;background:#0a0a0d}",
  ".nf-scan{position:absolute;inset:0;background:repeating-linear-gradient(0deg,transparent,transparent 2px,rgba(0,0,0,0.1) 2px,rgba(0,0,0,0.1) 4px);pointer-events:none;z-index:2}",
  ".nf-vig{position:absolute;inset:0;background:radial-gradient(ellipse at center,transparent 50%,rgba(0,0,0,0.6));pointer-events:none;z-index:2}",
  ".nf-content{z-index:3;text-align:center;max-width:600px;width:90%;animation:nfFade 0.5s}",
  "@keyframes nfFade{from{opacity:0;transform:translateY(20px)}to{opacity:1;transform:translateY(0)}}",
  ".nf-code{font-family:'Space Grotesk',sans-serif;font-size:clamp(80px,15vw,160px);font-weight:700;line-height:1;margin-bottom:12px;letter-spacing:-4px}",
  ".nf-code.glitch{animation:nfGlitch 0.15s}",
  "@keyframes nfGlitch{0%{transform:translate(0)}25%{transform:translate(-4px,2px)}50%{transform:translate(4px,-2px)}75%{transform:translate(-2px,4px)}100%{transform:translate(0)}}",
  ".nf-4{color:#c08b5c;text-shadow:0 0 40px rgba(192,139,92,0.3)}",
  ".nf-0{color:#e8e0d4;text-shadow:0 0 40px rgba(232,224,212,0.2)}",
  ".nf-4b{color:#c08b5c;text-shadow:0 0 40px rgba(192,139,92,0.3)}",
  ".nf-msg{font-family:'Space Grotesk',sans-serif;font-size:18px;font-weight:600;color:#e8e0d4;letter-spacing:6px;text-transform:uppercase;margin-bottom:8px}",
  ".nf-sub{font-size:13px;color:#6b6b78;margin-bottom:32px}",
  ".nf-terminal{text-align:left;background:#0e0e11;border:1px solid rgba(232,224,212,0.08);border-radius:10px;overflow:hidden;margin-bottom:24px}",
  ".nf-term-hdr{padding:10px 14px;background:#151519;border-bottom:1px solid rgba(232,224,212,0.08);font-size:12px;color:#6b6b78}",
  ".nf-term-body{padding:14px;font-size:12px;max-height:200px;overflow-y:auto}",
  ".nf-term-line{min-height:1.5em;color:#c08b5c;opacity:0.85}",
  ".nf-term-input{display:flex;align-items:center;gap:8px;margin-top:8px}",
  ".nf-prompt{color:#c08b5c;font-weight:600}",
  ".nf-inp{flex:1;background:transparent;border:none;outline:none;color:#e8e0d4;font-family:'JetBrains Mono',monospace;font-size:12px;caret-color:transparent}",
  ".nf-cursor{color:#c08b5c;font-size:12px}",
  ".nf-links{display:flex;gap:12px;justify-content:center;flex-wrap:wrap}",
  ".nf-link{padding:10px 20px;border-radius:8px;border:1px solid rgba(232,224,212,0.1);background:rgba(232,224,212,0.03);color:#e8e0d4;text-decoration:none;font-family:'JetBrains Mono',monospace;font-size:13px;transition:all 0.2s}",
  ".nf-link:hover{border-color:#c08b5c;background:rgba(192,139,92,0.08);color:#c08b5c}",
].join("\n");
```

### `/Zo-Ops` (page, private)

```tsx

```

### `/about-the-build` (page, public)

```tsx
import { useState } from "react";

export default function AboutTheBuild() {
  const [activeSection, setActiveSection] = useState("overview");
  const sections = [
    ["overview", "Overview"],
    ["zo", "Powered by Zo"],
    ["stack", "Tech Stack"],
    ["timeline", "Build Timeline"],
    ["decisions", "Design Decisions"],
    ["challenges", "Challenges"],
    ["credits", "Credits"],
  ];

  const zoFeatures: Array<[string, string, string]> = [
    ["🌐", "zo.space hosting", "Entire ZOS experience hosted on zo.space with instant deploys and rollbacks."],
    ["🗂️", "Space routes", "Every page and API endpoint is a Zo space route. /zos, /trivia, /zo-city, /secret, /about-the-build, /404, plus ~15 API routes."],
    ["⚡", "Live API endpoints", "/api/zos/now, /api/zos/build-log, /api/zos/signals, /api/x-feed, /api/calendar, /api/projects, /api/blog, /api/contact, /api/trivia/*. All Zo-backed."],
    ["🤖", "ask/zo voice agent", "Voi-ZOS uses the Zo ask endpoint as a guarded, homepage-only voice-first assistant."],
    ["💳", "Stripe via Zo", "App Store and Zo Consultation payment links created through Zo's Stripe integration."],
    ["🔄", "Route history + undo", "Leveraged Zo's built-in route versioning to recover and iterate without fear."],
    ["🎨", "Space assets", "ZOS logo and wallpaper served directly from Zo space assets."],
    ["🛠️", "Space settings", "Custom site title, description, favicon, and custom 404 route all configured through Zo."],
    ["📡", "MCP tooling", "Built using Zo's MCP tools for route creation, code edits, diagnostics, and deployment."],
  ];

  const content: Record<string, JSX.Element> = {
    overview: (
      <div className="atb-text">
        <div className="atb-hero">ZOS. A personal site rebuilt as an operating system.</div>
        <h2 className="atb-h2">What is ZOS?</h2>
        <p>ZOS (ZenOS) is a fully interactive desktop experience built entirely on <a href="https://zo.computer" target="_blank" rel="noopener" className="atb-link">Zo Computer</a> for the Zo Computer Challenge.</p>
        <p>The name is a play on my handle (<strong>Zenlyte</strong>) and Zo Computer. Pronounced "Zoh-Ess".</p>
        <p>It's a personal website disguised as an OS. Complete with a boot sequence, role-based access modes, a draggable/resizable window manager, command palette (⌘K), context menus, theme switching, toast notifications, a matrix rain screensaver, multiple easter eggs, mobile responsive design, Stripe payments, live Zo-backed APIs, a voice-first assistant, and 11 fully functional apps.</p>
        <h2 className="atb-h2">Why an OS?</h2>
        <p>Most personal websites are pages. I wanted mine to be an <em>experience</em>. Something you explore, not just scroll through. An OS metaphor gives visitors agency: they choose what to open, how to arrange things, what to discover.</p>
        <p>Every interaction was designed to make you think: \u201cWait, this is a website?\u201d</p>
        <h2 className="atb-h2">Signature moments</h2>
        <ul className="atb-list">
          <li>Press-and-hold anywhere to open a black hole that sucks in floating particles. Release for a big bang.</li>
          <li>Role-based entry modes change the starter prompts and framing across the OS.</li>
          <li>Voi-ZOS. A voice-first assistant grounded to the public homepage.</li>
          <li>Hidden signals, terminal commands, and a secret route for the curious.</li>
        </ul>
      </div>
    ),
    zo: (
      <div className="atb-text">
        <h2 className="atb-h2">Powered by Zo Computer</h2>
        <p>ZOS isn't just <em>hosted</em> on Zo. It's built end-to-end on Zo's primitives. Here's exactly what was used:</p>
        <div className="atb-stack-grid">
          {zoFeatures.map(([icon, name, desc], i) => (
            <div key={i} className="atb-stack-item">
              <span className="atb-stack-icon">{icon}</span>
              <div><div className="atb-stack-name">{name}</div><div className="atb-stack-desc">{desc}</div></div>
            </div>
          ))}
        </div>
        <h2 className="atb-h2">Why this matters</h2>
        <p>Zo collapses the usual web stack. Hosting, routing, serverless APIs, static assets, payments, and an AI endpoint. Into a single coherent surface. ZOS leans on that: every feature you interact with, from the window manager down to the voice agent, runs through a Zo primitive.</p>
      </div>
    ),
    stack: (
      <div className="atb-text">
        <h2 className="atb-h2">Technology</h2>
        <div className="atb-stack-grid">
          {[["⚡", "Zo Computer", "Hosting, space routes, APIs, Stripe, ask endpoint, MCP tooling"],
            ["⚛️", "React + TypeScript", "Component architecture, type safety, hooks-based state"],
            ["🎨", "Custom CSS-in-JS", "Hand-crafted styles with CSS custom properties for theming"],
            ["🧠", "AI-assisted workflow", "AI-driven planning, code generation, and rapid iteration"],
            ["💳", "Stripe", "Payment links for Zo Consultation and App Store goods"],
            ["🔍", "Custom APIs", "Projects, blog, calendar, contact, trivia, X feed, signals"],
          ].map(([icon, name, desc], i) => (
            <div key={i} className="atb-stack-item">
              <span className="atb-stack-icon">{icon}</span>
              <div><div className="atb-stack-name">{name}</div><div className="atb-stack-desc">{desc}</div></div>
            </div>
          ))}
        </div>
        <h2 className="atb-h2">Architecture</h2>
        <p>ZOS is a single-page React application rendered as a Zo space route. The entire OS. Boot sequence, window manager, all 11 apps, theming, particle system, cursor effects. Lives in one route file.</p>
        <p>State management uses React hooks only. No external state libraries. The window manager tracks position, size, z-index, and minimized/maximized state per window.</p>
      </div>
    ),
    timeline: (
      <div className="atb-text">
        <h2 className="atb-h2">Build Timeline</h2>
        <div className="atb-timeline">
          {[["Phase 1", "Foundation", "Boot sequence, role selection, window manager, taskbar, desktop, particles, cursor halo"],
            ["Phase 2", "Core Apps", "About, Terminal, Projects, Settings (themes + roles)"],
            ["Phase 3", "Advanced Apps", "Command Centre, Lab (Recruiter Decoder + Signal Hunt), Games"],
            ["Phase 4", "Polish", "Context menu, command palette, Konami code, window animations, desktop widgets"],
            ["Phase 5", "Full Suite", "X Feed (Briefings), Book Time, App Store with Stripe"],
            ["Phase 6", "Screensaver & APIs", "Matrix rain screensaver with idle timer, 3 ZOS API routes"],
            ["Phase 7", "Easter Eggs", "Hidden /secret route, watermark easter egg, expanded terminal"],
            ["Phase 8", "Polish", "Toast system, mobile responsive CSS, /about-the-build, custom /404"],
            ["Phase 9", "Interaction Deepening", "Click-hold black hole + big bang particle physics, larger default windows, doubled particle count"],
            ["Phase 10", "Voice-First", "Voi-ZOS becomes a real voice agent via ask/zo, strictly scoped to public homepage content"],
            ["Phase 11", "Presentation", "Powered-by-Zo credits, refreshed branding, favicon/title, submission polish"],
          ].map(([phase, title, desc], i) => (
            <div key={i} className="atb-tl-item">
              <div className="atb-tl-marker"><div className="atb-tl-dot" /><div className="atb-tl-phase">{phase}</div></div>
              <div className="atb-tl-content"><div className="atb-tl-title">{title}</div><div className="atb-tl-desc">{desc}</div></div>
            </div>
          ))}
        </div>
      </div>
    ),
    decisions: (
      <div className="atb-text">
        <h2 className="atb-h2">Design Decisions</h2>
        <div className="atb-decision">
          <h3 className="atb-h3">🎨 "Oxidized Future" palette</h3>
          <p>Warm copper and bone on deep midnight. Inspired by aged metal, weathered leather, and machines that have stories to tell. Avoids the typical "dark mode equals blue" trap.</p>
        </div>
        <div className="atb-decision">
          <h3 className="atb-h3">🖥️ OS metaphor</h3>
          <p>An OS provides natural affordances. Windows, menus, files. Visitors already understand them. The boot sequence sets expectations. The role selector personalizes the experience.</p>
        </div>
        <div className="atb-decision">
          <h3 className="atb-h3">🎯 Role-based modes</h3>
          <p>Visitor, Recruiter, Collaborator, Curious Human. Each tailors Voi-ZOS starter prompts and framing without fragmenting the product.</p>
        </div>
        <div className="atb-decision">
          <h3 className="atb-h3">🥚 Easter eggs everywhere</h3>
          <p>Konami code, secret terminal commands, hidden routes, watermark clicks. Discovery mechanics reward curiosity and make people want to come back.</p>
        </div>
        <div className="atb-decision">
          <h3 className="atb-h3">🔒 Guardrailed voice agent</h3>
          <p>Voi-ZOS is voice-first, but strictly scoped to public homepage content with server-side rate limits, refusal paths, and structured outputs. Low-cost and safe by default.</p>
        </div>
      </div>
    ),
    challenges: (
      <div className="atb-text">
        <h2 className="atb-h2">Challenges & lessons</h2>
        <div className="atb-challenge">
          <h3 className="atb-h3">Dynamic inline styles</h3>
          <p>Double curly braces were interpreted as template variables in certain contexts. All dynamic positioning moved to refs + effects or CSS classes with data attributes.</p>
        </div>
        <div className="atb-challenge">
          <h3 className="atb-h3">Single-file architecture</h3>
          <p>The entire OS lives in one route file. Managing 11+ app components, a window manager, and hundreds of CSS rules required disciplined naming and section markers.</p>
        </div>
        <div className="atb-challenge">
          <h3 className="atb-h3">Incremental edits vs. CSS arrays</h3>
          <p>Incremental code edits tended to corrupt the CSS array. The fix: prefer focused full rewrites for routes with large stylesheet arrays.</p>
        </div>
        <div className="atb-challenge">
          <h3 className="atb-h3">Voice on a budget</h3>
          <p>Real voice interaction is expensive fast. ZOS uses browser STT + TTS, a tiny curated homepage corpus, a single guarded ask/zo call per finalized question, and cached common answers to stay cheap and safe.</p>
        </div>
      </div>
    ),
    credits: (
      <div className="atb-text">
        <h2 className="atb-h2">Credits</h2>
        <p><strong>Built by:</strong> Zenlyte (<a href="https://github.com/Zenlyte" target="_blank" rel="noopener" className="atb-link">@Zenlyte</a>)</p>
        <p><strong>Contact:</strong> <a href="mailto:info@zenlytics.net" className="atb-link">info@zenlytics.net</a></p>
        <p><strong>Platform:</strong> <a href="https://zo.computer" target="_blank" rel="noopener" className="atb-link">Zo Computer</a></p>
        <p><strong>Fonts:</strong> Inter, JetBrains Mono, Playfair Display, Space Grotesk</p>
        <p><strong>Contest:</strong> <a href="https://contra.com/community/topic/zocomputerchallenge/guidelines" target="_blank" rel="noopener" className="atb-link">Zo Computer Challenge</a></p>
        <div className="atb-thanks">Thanks for exploring ZOS. ❤️</div>
      </div>
    ),
  };

  return (
    <div className="atb">
      <style>{ATB_CSS}</style>
      <div className="atb-nav">
        <a href="/zos" className="atb-back">← Back to ZOS</a>
        <a href="/press" className="atb-back">📰 Press Kit</a>
        <div className="atb-logo">⚡ About the Build</div>
        <div className="atb-tabs">
          {sections.map(([id, label]) => (
            <button key={id} className={"atb-tab" + (activeSection === id ? " active" : "")} onClick={() => setActiveSection(id)}>{label}</button>
          ))}
        </div>
      </div>
      <div className="atb-content">
        <div className="atb-inner">{content[activeSection]}</div>
      </div>
    </div>
  );
}

const ATB_CSS = [
  "@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&family=JetBrains+Mono:wght@400;500;700&family=Playfair+Display:ital,wght@0,400;0,700;1,400&family=Space+Grotesk:wght@400;500;600;700&display=swap');",
  "*{box-sizing:border-box;margin:0;padding:0}",
  "body{background:#0e0e11;font-family:'Inter',sans-serif;color:#e8e0d4;overflow-x:hidden}",
  ".atb{min-height:100vh;display:flex}",
  ".atb-nav{width:260px;min-height:100vh;background:#151519;border-right:1px solid rgba(232,224,212,0.08);padding:24px 16px;display:flex;flex-direction:column;gap:16px;position:fixed;top:0;left:0}",
  ".atb-back{font-family:'JetBrains Mono',monospace;font-size:12px;color:#c08b5c;text-decoration:none;transition:opacity 0.15s}",
  ".atb-back:hover{opacity:0.7}",
  ".atb-logo{font-family:'Space Grotesk',sans-serif;font-size:18px;font-weight:700;color:#e8e0d4;padding-bottom:16px;border-bottom:1px solid rgba(232,224,212,0.08)}",
  ".atb-tabs{display:flex;flex-direction:column;gap:4px}",
  ".atb-tab{padding:10px 14px;border-radius:6px;border:none;background:transparent;color:#6b6b78;cursor:pointer;font-family:'Inter',sans-serif;font-size:13px;text-align:left;transition:all 0.15s}",
  ".atb-tab:hover{color:#e8e0d4;background:rgba(232,224,212,0.04)}",
  ".atb-tab.active{color:#c08b5c;background:rgba(192,139,92,0.1)}",
  ".atb-content{margin-left:260px;flex:1;padding:48px;max-width:860px}",
  ".atb-inner{animation:atbFade 0.3s ease}",
  "@keyframes atbFade{from{opacity:0;transform:translateY(8px)}to{opacity:1;transform:translateY(0)}}",
  ".atb-hero{font-family:'Playfair Display',serif;font-style:italic;font-size:22px;color:#c08b5c;margin-bottom:24px;padding:16px 18px;border-left:3px solid #c08b5c;background:rgba(192,139,92,0.06);border-radius:0 8px 8px 0}",
  ".atb-text p{font-size:15px;line-height:1.8;color:#94938e;margin-bottom:14px}",
  ".atb-text strong{color:#e8e0d4}",
  ".atb-text em{color:#c08b5c;font-style:italic}",
  ".atb-list{list-style:none;padding:0;margin:8px 0 18px}",
  ".atb-list li{padding:8px 0 8px 22px;position:relative;color:#94938e;font-size:14px;line-height:1.7}",
  ".atb-list li::before{content:'\u25B8';position:absolute;left:0;color:#c08b5c}",
  ".atb-link{color:#c08b5c;text-decoration:none;border-bottom:1px solid rgba(192,139,92,0.3);transition:border-color 0.15s}",
  ".atb-link:hover{border-color:#c08b5c}",
  ".atb-h2{font-family:'Playfair Display',serif;font-size:24px;color:#e8e0d4;margin:32px 0 16px;padding-bottom:8px;border-bottom:1px solid rgba(232,224,212,0.08)}",
  ".atb-h2:first-child{margin-top:0}",
  ".atb-h3{font-family:'Space Grotesk',sans-serif;font-size:16px;color:#e8e0d4;margin-bottom:8px}",
  ".atb-stack-grid{display:flex;flex-direction:column;gap:10px;margin-bottom:24px}",
  ".atb-stack-item{display:flex;align-items:flex-start;gap:14px;padding:14px;border-radius:8px;border:1px solid rgba(232,224,212,0.08);background:rgba(232,224,212,0.02);transition:all 0.2s}",
  ".atb-stack-item:hover{border-color:rgba(192,139,92,0.3);background:rgba(192,139,92,0.04)}",
  ".atb-stack-icon{font-size:22px;width:32px;text-align:center;flex-shrink:0;padding-top:2px}",
  ".atb-stack-name{font-family:'Space Grotesk',sans-serif;font-size:14px;font-weight:600;color:#e8e0d4;margin-bottom:3px}",
  ".atb-stack-desc{font-size:12px;color:#6b6b78;line-height:1.5}",
  ".atb-timeline{display:flex;flex-direction:column;gap:0;padding-left:20px;border-left:2px solid rgba(232,224,212,0.08)}",
  ".atb-tl-item{display:flex;gap:16px;padding:16px 0}",
  ".atb-tl-marker{display:flex;flex-direction:column;align-items:center;min-width:60px;position:relative}",
  ".atb-tl-dot{width:12px;height:12px;border-radius:50%;background:#c08b5c;border:2px solid #151519;position:absolute;left:-27px;top:4px;box-shadow:0 0 8px rgba(192,139,92,0.4)}",
  ".atb-tl-phase{font-family:'JetBrains Mono',monospace;font-size:10px;color:#6b6b78;text-transform:uppercase;letter-spacing:1px}",
  ".atb-tl-content{flex:1}",
  ".atb-tl-title{font-family:'Space Grotesk',sans-serif;font-size:16px;font-weight:600;color:#e8e0d4;margin-bottom:4px}",
  ".atb-tl-desc{font-size:13px;color:#94938e;line-height:1.6}",
  ".atb-decision,.atb-challenge{padding:16px;border-radius:8px;border:1px solid rgba(232,224,212,0.08);background:rgba(232,224,212,0.02);margin-bottom:14px}",
  ".atb-thanks{margin-top:32px;padding:20px;border-radius:10px;background:rgba(192,139,92,0.08);border:1px solid rgba(192,139,92,0.2);text-align:center;font-family:'Playfair Display',serif;font-size:18px;color:#c08b5c}",
  "@media(max-width:768px){.atb-nav{width:100%;min-height:auto;position:static;border-right:none;border-bottom:1px solid rgba(232,224,212,0.08)}.atb-tabs{flex-direction:row;flex-wrap:wrap}.atb-content{margin-left:0;padding:24px}}",
].join("\n");
```

### `/api/agents` (api, public)

```typescript

```

### `/api/audit` (api, public)

```typescript

```

### `/api/auth-status` (api, public)

```typescript

```

### `/api/benchmarks` (api, public)

```typescript

```

### `/api/benchmarks/refresh` (api, public)

```typescript
import type { Context } from "hono";
import { spawn } from "child_process";

export default async (c: Context) => {
  const secret = c.req.header("Authorization")?.replace("Bearer ", "");
  if (secret !== process.env.BEARER_SECRET) {
    return c.json({ error: "Unauthorized" }, 401);
  }

  // Spawn refresh script non-blocking
  spawn("python3", ["/home/workspace/Scripts/fetch_aa_benchmarks.py"], {
    detached: true,
    stdio: "ignore",
  }).unref();

  return c.json({ status: "refresh started" });
};
```

### `/api/billing` (api, public)

```typescript
import type { Context } from "hono";
import { timingSafeEqual } from "node:crypto";

// Session-based authentication per AGENTS.md security policy
async function validateSession(c: Context): Promise<boolean> {
  const authHeader = c.req.header("Authorization");
  if (authHeader?.startsWith("Bearer ")) {
    const token = authHeader.slice(7);
    const apiKey = process.env.ZO_API_KEY;
    if (apiKey && token.length === apiKey.length && timingSafeEqual(Buffer.from(token), Buffer.from(apiKey))) {
      return true;
    }
  }
  const cookieHeader = c.req.header("Cookie") || "";
  const hasSession = cookieHeader.includes("zo_session") || cookieHeader.includes("auth_token");
  const zoUser = c.req.header("X-Zo-User");
  if (zoUser === "curtastrophe") return true;
  const host = c.req.header("Host") || "";
  if (host.includes("localhost")) return true;
  const referer = c.req.header("Referer") || "";
  if (referer.includes("curtastrophe.zo.space")) return true;
  return hasSession;
}

export default async (c: Context) => {
  if (!await validateSession(c)) {
    return c.json({ error: "Unauthorized" }, 401);
  }
  
  return c.json({
    plan: "Pro",
    credits: { balance: 3852, used: 6148 },
    billing: {
      cycle_start: "2026-03-01",
      cycle_end: "2026-03-31",
      estimated_bill: 0,
    },
    data_source: "STATIC_MOCK",
    note: "Billing data is mocked. Check Zo Billing page for real invoices.",
    last_updated: new Date().toISOString(),
  });
};
```

### `/api/blog` (api, public)

```typescript

```

### `/api/blog/:slug` (api, public)

```typescript

```

### `/api/buildin/callback` (api, public)

```typescript

```

### `/api/buildin/disconnect` (api, public)

```typescript

```

### `/api/buildin/status` (api, public)

```typescript
import type { Context } from "hono";

export default async (c: Context) => {
  const tokenFile = "/home/workspace/Data/buildin/token.json";
  const { readFileSync, existsSync } = await import("fs");
  
  if (!existsSync(tokenFile)) {
    return c.json({ connected: false });
  }
  
  try {
    const tokenData = JSON.parse(readFileSync(tokenFile, "utf-8"));
    const now = Date.now();
    
    // Check if token is expired (with 5 min buffer)
    if (tokenData.expires_at && tokenData.expires_at < now - 300000) {
      return c.json({ connected: false, reason: "expired" });
    }
    
    // Get accessible spaces
    const res = await fetch("https://api.buildin.ai/api/v1/spaces", {
      headers: { Authorization: `Bearer ${tokenData.access_token}` }
    });
    
    const spaces = res.ok ? (await res.json()).data || [] : [];
    
    return c.json({ connected: true, spaces });
  } catch {
    return c.json({ connected: false });
  }
}
```

### `/api/calendar` (api, public)

```typescript

```

### `/api/career-ops` (api, public)

```typescript

```

### `/api/career-ops/applications` (api, public)

```typescript

```

### `/api/career-ops/batch` (api, public)

```typescript

```

### `/api/career-ops/pipeline` (api, public)

```typescript

```

### `/api/career-ops/scan` (api, public)

```typescript

```

### `/api/career-ops/scan-history` (api, public)

```typescript

```

### `/api/contact` (api, public)

```typescript

```

### `/api/credits` (api, public)

```typescript

```

### `/api/datasets/list` (api, public)

```typescript

```

### `/api/datasets/proxy/*` (api, public)

```typescript

```

### `/api/datasets/start` (api, public)

```typescript

```

### `/api/datasets/viewer` (api, public)

```typescript

```

### `/api/diagnose` (api, public)

```typescript

```

### `/api/extension-save` (api, public)

```typescript

```

### `/api/failures` (api, public)

```typescript

```

### `/api/family-log` (api, public)

```typescript

```

### `/api/files` (api, public)

```typescript

```

### `/api/flowpulse` (api, public)

```typescript

```

### `/api/generate-icon` (api, public)

```typescript

```

### `/api/health-check` (api, public)

```typescript

```

### `/api/logs` (api, public)

```typescript

```

### `/api/models` (api, public)

```typescript

```

### `/api/my-models` (api, public)

```typescript

```

### `/api/nav-links` (api, public)

```typescript

```

### `/api/projects` (api, public)

```typescript

```

### `/api/projects-conversations` (api, public)

```typescript

```

### `/api/puzzle-callback` (page, public)

```tsx

```

### `/api/receipt-images` (api, public)

```typescript

```

### `/api/receipts` (api, public)

```typescript

```

### `/api/security` (api, public)

```typescript

```

### `/api/services` (api, public)

```typescript

```

### `/api/share` (api, public)

```typescript

```

### `/api/share/:id` (api, public)

```typescript

```

### `/api/share/:id/download` (api, public)

```typescript

```

### `/api/sites` (api, public)

```typescript

```

### `/api/skills-gallery` (api, public)

```typescript

```

### `/api/speech-game-auth` (api, public)

```typescript

```

### `/api/speech-game-data` (api, public)

```typescript

```

### `/api/system-stats` (api, public)

```typescript

```

### `/api/telemetry-data` (api, public)

```typescript

```

### `/api/temporal-auth-check` (api, public)

```typescript

```

### `/api/temporal/*` (api, public)

```typescript

```

### `/api/test-deps` (api, public)

```typescript

```

### `/api/test-env` (api, public)

```typescript

```

### `/api/test-exec` (api, public)

```typescript

```

### `/api/test-write` (api, public)

```typescript

```

### `/api/trivia` (api, public)

```typescript

```

### `/api/trivia/by-date` (api, public)

```typescript

```

### `/api/trivia/dates` (api, public)

```typescript

```

### `/api/trivia/leaderboard` (api, public)

```typescript

```

### `/api/trivia/random` (api, public)

```typescript

```

### `/api/trivia/subscribe` (api, public)

```typescript

```

### `/api/trivia/unsubscribe` (api, public)

```typescript

```

### `/api/trivia/user-stats` (api, public)

```typescript

```

### `/api/twinmind` (api, public)

```typescript

```

### `/api/twinmind-callback` (api, public)

```typescript

```

### `/api/updates` (api, public)

```typescript

```

### `/api/voi-zos` (api, public)

```typescript

```

### `/api/x-feed` (api, public)

```typescript

```

### `/api/zo-city-data` (api, public)

```typescript

```

### `/api/zo-space-theme-gallery` (api, public)

```typescript

```

### `/api/zo-space-theme-gallery/:id` (api, public)

```typescript

```

### `/api/zo-space-theme-gallery/skill` (api, public)

```typescript

```

### `/api/zoboard/*` (api, public)

```typescript

```

### `/api/zos/build-log` (api, public)

```typescript

```

### `/api/zos/now` (api, public)

```typescript

```

### `/api/zos/signals` (api, public)

```typescript

```

### `/blog` (page, public)

```tsx

```

### `/blog/:slug` (page, public)

```tsx

```

### `/buildin-auth` (page, private)

```tsx

```

### `/career-ops` (page, private)

```tsx

```

### `/dashboard` (page, private)

```tsx

```

### `/data-explorer` (page, private)

```tsx

```

### `/data/zo-trivia/` (page, private)

```tsx

```

### `/data/zo-trivia/api/query` (api, public)

```typescript

```

### `/docs` (api, public)

```typescript

```

### `/icon-configurator` (page, public)

```tsx

```

### `/job-ops` (page, private)

```tsx

```

### `/kg-browse` (api, public)

```typescript

```

### `/kg-by-type` (api, public)

```typescript

```

### `/kg-entity` (api, public)

```typescript

```

### `/kg-graph` (api, public)

```typescript

```

### `/kg-recall` (api, public)

```typescript

```

### `/kg-search` (api, public)

```typescript

```

### `/kg-stats` (api, public)

```typescript

```

### `/knowledge-graph` (page, private)

```tsx

```

### `/model-advisor` (page, public)

```tsx

```

### `/openclaw-dashboard` (page, private)

```tsx

```

### `/press` (page, public)

```tsx

```

### `/profile` (page, public)

```tsx

```

### `/receipts` (page, public)

```tsx

```

### `/repurpose` (page, private)

```tsx

```

### `/s/:id` (page, public)

```tsx

```

### `/secret` (page, public)

```tsx

```

### `/share` (page, private)

```tsx

```

### `/skills-gallery` (page, private)

```tsx

```

### `/speech-game` (page, public)

```tsx

```

### `/speech-game-manifest.json` (api, public)

```typescript

```

### `/speech-game-sw.js` (api, public)

```typescript

```

### `/speech-game/stats` (page, public)

```tsx

```

### `/speech-game/stickers` (page, public)

```tsx

```

### `/telemetry` (page, private)

```tsx

```

### `/temporal` (page, private)

```tsx

```

### `/trivia` (page, public)

```tsx

```

### `/trivia/archive` (page, private)

```tsx

```

### `/trivia/leaderboard` (page, private)

```tsx

```

### `/zo-city` (page, public)

```tsx

```

### `/zo-city-three-test` (page, public)

```tsx

```

### `/zo-control-deck` (page, private)

```tsx

```

### `/zo-space-theme-gallery` (page, public)

```tsx

```

### `/zo-space-theme-gallery/:id` (page, public)

```tsx

```

### `/zo-status` (page, public)

```tsx

```

### `/zoboard` (page, private)

```tsx

```

### `/zoboard/:slug` (page, private)

```tsx

```

### `/zos` (page, public)

```tsx

```

### `/zos-lite` (page, public)

```tsx

```

## Setup

**Directories to create:**
- `Data/buildin`

**Files to initialize:**
- `Data/buildin/token.json` with content: `[]`

**Secrets required** (configure in [Settings > Advanced](/?t=settings&s=advanced)):
- `BEARER_SECRET`
- `ZO_API_KEY`

