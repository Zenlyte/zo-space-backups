---
format: zopack
version: "1.0"
name: zo-space-backup
author: unknown.zo.computer
routes: 2
exported: 2026-06-08
---

# zo-space-backup

## Routes

### `/` (page, public)

```tsx
import { useState, useEffect, useRef } from "react";
import {
  ArrowRight, Github, Twitter, Linkedin, MessageSquare, Send, CheckCircle,
  Database, Bot, Users, Wrench, ExternalLink, Gamepad2, Sparkles, LayoutDashboard,
  ChevronRight, ArrowUpRight, Palette, Layers, Cpu, Code2, Rocket, Globe, Zap,
  Search, Clock, BookOpen, Terminal, FolderKanban, Menu, X, Shield, Lock,
  Zap as ZapIcon, Brain, Briefcase, FileText, Activity
} from "lucide-react";

const COLORS = {
  bg: "#0a0a0f",
  card: "#0f1117",
  cardHover: "#161922",
  cyan: "#06b6d4",
  indigo: "#6366f1",
  slate: "#94a3b8",
  white: "#f8fafc",
  dimmed: "#4b5563",
  border: "rgba(255,255,255,0.06)",
  accent: "#d8a657"
};

export default function Home() {
  const [navOpen, setNavOpen] = useState(false);
  const [mounted, setMounted] = useState(false);
  
  useEffect(() => {
    setMounted(true);
  }, []);

  const PROJECTS = [
    {
      id: "zos",
      name: "ZOS (ZenOS)",
      desc: "A personal site reimagined as a living operating system. Features a window manager, command palette, and real app integrations.",
      tags: ["Zo Computer", "React", "System Design"],
      icon: <Cpu className="w-5 h-5" />,
      link: "/zos",
      status: "active"
    },
    {
      id: "trivia",
      name: "Zo Trivia",
      desc: "Daily trivia engine powered by Bun/SQLite. Track stats, climb the leaderboard, and learn about the Zo ecosystem.",
      tags: ["SQLite", "Game Design", "Automation"],
      icon: <Brain className="w-5 h-5" />,
      link: "/trivia",
      status: "active"
    },
    {
      id: "speech",
      name: "Speech Game",
      desc: "Voice-controlled speech therapy game for kids. Track progress, collect stickers, and play offline (PWA).",
      tags: ["Web Speech API", "PWA", "Education"],
      icon: <Gamepad2 className="w-5 h-5" />,
      link: "/speech-game",
      status: "active"
    },
    {
      id: "career",
      name: "Career Ops",
      desc: "AI-powered job application pipeline. Scan postings, track status, and optimize resumes with agentic help.",
      tags: ["AI Agents", "Career", "Workflow"],
      icon: <Briefcase className="w-5 h-5" />,
      link: "/career-ops",
      status: "active"
    },
    {
      id: "kg",
      name: "Knowledge Graph",
      desc: "Visual exploration of personal memory and entity relationships. Map projects, decisions, and patterns.",
      tags: ["Data Viz", "Graph", "Memory"],
      icon: <Layers className="w-5 h-5" />,
      link: "/knowledge-graph",
      status: "active"
    },
    {
      id: "themes",
      name: "Theme Gallery",
      desc: "A community collection of Zo Space visual themes. Browse, preview, and apply styles instantly.",
      tags: ["Design", "CSS", "Community"],
      icon: <Palette className="w-5 h-5" />,
      link: "/zo-space-theme-gallery",
      status: "active"
    }
  ];

  return (
    <>
      <style>{`
        @import url('https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@400;500;600;700&family=Inter:wght@400;500;600&family=JetBrains+Mono:wght@400;500&display=swap');
        
        :root {
          --space-primary: ${COLORS.cyan};
          --space-primary-muted: rgba(6, 182, 212, 0.2);
        }

        body {
          background: ${COLORS.bg};
          color: ${COLORS.white};
          font-family: 'Inter', sans-serif;
        }

        .font-heading { font-family: 'Space Grotesk', sans-serif; }
        .font-mono { font-family: 'JetBrains Mono', monospace; }

        .hero-gradient {
          background: radial-gradient(circle at top right, rgba(99, 102, 241, 0.1), transparent 40%),
                      radial-gradient(circle at bottom left, rgba(6, 182, 212, 0.1), transparent 40%);
        }

        .glass-card {
          background: ${COLORS.card};
          border: 1px solid ${COLORS.border};
          backdrop-filter: blur(12px);
          transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
        }

        .glass-card:hover {
          border-color: rgba(6, 182, 212, 0.3);
          background: ${COLORS.cardHover};
          transform: translateY(-4px);
          box-shadow: 0 12px 40px -12px rgba(0, 0, 0, 0.5);
        }

        .nav-link {
          color: ${COLORS.slate};
          transition: all 0.2s;
        }

        .nav-link:hover {
          color: ${COLORS.cyan};
        }

        .btn-primary {
          background: ${COLORS.cyan};
          color: #000;
          font-weight: 600;
          transition: all 0.2s;
        }

        .btn-primary:hover {
          transform: translateY(-1px);
          box-shadow: 0 0 20px rgba(6, 182, 212, 0.4);
        }

        .animate-in {
          animation: slideUp 0.6s cubic-bezier(0.16, 1, 0.3, 1) forwards;
        }

        @keyframes slideUp {
          from { opacity: 0; transform: translateY(20px); }
          to { opacity: 1; transform: translateY(0); }
        }
      `}</style>

      <div className="min-h-screen hero-gradient flex flex-col">
        {/* Navigation */}
        <nav className="sticky top-0 z-50 border-b border-white/5 bg-[#0a0a0f]/80 backdrop-blur-md">
          <div className="max-w-7xl mx-auto px-6 h-16 flex items-center justify-between">
            <div className="flex items-center gap-2">
              <div className="w-8 h-8 rounded-lg bg-cyan-500/20 flex items-center justify-center border border-cyan-500/40">
                <Zap className="w-5 h-5 text-cyan-400" />
              </div>
              <span className="font-heading font-bold text-xl tracking-tight">
                zenlyte<span className="text-cyan-400">.</span>
              </span>
            </div>

            {/* Desktop Nav */}
            <div className="hidden md:flex items-center gap-8">
              <a href="/zos" className="nav-link text-sm font-medium">ZOS</a>
              <a href="/projects" className="nav-link text-sm font-medium">Projects</a>
              <a href="/blog" className="nav-link text-sm font-medium">Blog</a>
              <a href="/profile" className="nav-link text-sm font-medium">Profile</a>
              <a 
                href="/career-ops" 
                className="btn-primary px-4 py-2 rounded-lg text-sm"
              >
                Launch App
              </a>
            </div>

            {/* Mobile Nav Toggle */}
            <button 
              className="md:hidden p-2 text-slate-400"
              onClick={() => setNavOpen(!navOpen)}
            >
              {navOpen ? <X /> : <Menu />}
            </button>
          </div>

          {/* Mobile Menu */}
          {navOpen && (
            <div className="md:hidden border-t border-white/5 bg-[#0a0a0f] p-6 flex flex-col gap-4 animate-in">
              <a href="/zos" className="text-lg font-medium">ZOS</a>
              <a href="/projects" className="text-lg font-medium">Projects</a>
              <a href="/blog" className="text-lg font-medium">Blog</a>
              <a href="/profile" className="text-lg font-medium">Profile</a>
              <div className="pt-4">
                <a href="/career-ops" className="btn-primary block text-center py-3 rounded-xl">
                  Launch Career Ops
                </a>
              </div>
            </div>
          )}
        </nav>

        <main className="flex-1 max-w-7xl mx-auto px-6 py-12 md:py-24">
          {/* Hero Section */}
          <header className="max-w-3xl animate-in">
            <div className="inline-flex items-center gap-2 px-3 py-1 rounded-full bg-cyan-500/10 border border-cyan-500/20 text-cyan-400 text-xs font-semibold mb-6">
              <Sparkles className="w-3 h-3" />
              <span>Operating on Zo Computer</span>
            </div>
            <h1 className="font-heading text-5xl md:text-7xl font-bold leading-tight mb-6">
              Building the next generation of <span className="text-transparent bg-clip-text bg-gradient-to-r from-cyan-400 to-indigo-500">Personal OS</span>
            </h1>
            <p className="text-lg md:text-xl text-slate-400 mb-10 leading-relaxed">
              I explore the frontier of AI agents, automation, and distributed systems 
              to build software that acts as leverage for the mind.
            </p>
            <div className="flex wrap gap-4">
              <a 
                href="/zos" 
                className="btn-primary px-8 py-4 rounded-xl flex items-center gap-2 group"
              >
                Boot ZenOS
                <ArrowRight className="w-4 h-4 transition-transform group-hover:translate-x-1" />
              </a>
              <a 
                href="/profile" 
                className="px-8 py-4 rounded-xl glass-card font-semibold flex items-center gap-2"
              >
                View Profile
              </a>
            </div>
          </header>

          {/* Projects Grid */}
          <section className="mt-32">
            <div className="flex items-end justify-between mb-12">
              <div>
                <h2 className="font-heading text-3xl font-bold mb-4">Featured Systems</h2>
                <p className="text-slate-400">A collection of projects built and hosted on Zo.</p>
              </div>
              <a href="/projects" className="hidden md:flex items-center gap-1 text-cyan-400 font-medium hover:underline">
                View all <ChevronRight className="w-4 h-4" />
              </a>
            </div>

            <div className="grid md:grid-cols-2 lg:grid-cols-3 gap-6">
              {PROJECTS.map((project, i) => (
                <a 
                  key={project.id} 
                  href={project.link}
                  className="glass-card p-6 rounded-2xl flex flex-col animate-in"
                  style={{ animationDelay: `${i * 0.1}s` }}
                >
                  <div className="w-10 h-10 rounded-xl bg-cyan-500/10 flex items-center justify-center border border-cyan-500/20 text-cyan-400 mb-6">
                    {project.icon}
                  </div>
                  <h3 className="font-heading text-xl font-bold mb-3">{project.name}</h3>
                  <p className="text-slate-400 text-sm leading-relaxed mb-6 flex-1">
                    {project.desc}
                  </p>
                  <div className="flex flex-wrap gap-2">
                    {project.tags.map(tag => (
                      <span key={tag} className="text-[10px] font-mono px-2 py-1 rounded bg-white/5 text-slate-500 border border-white/5 uppercase">
                        {tag}
                      </span>
                    ))}
                  </div>
                </a>
              ))}
            </div>
            <div className="mt-8 md:hidden">
               <a href="/projects" className="flex items-center justify-center gap-1 py-4 glass-card rounded-xl text-cyan-400 font-medium">
                View all projects <ChevronRight className="w-4 h-4" />
              </a>
            </div>
          </section>

          {/* Stats Bar */}
          <section className="mt-32 grid grid-cols-2 md:grid-cols-4 gap-4 animate-in" style={{ animationDelay: '0.4s' }}>
            <div className="glass-card p-6 rounded-2xl text-center">
              <div className="text-3xl font-bold font-heading text-cyan-400 mb-1">127+</div>
              <div className="text-xs font-mono text-slate-500 uppercase tracking-wider">Active Routes</div>
            </div>
            <div className="glass-card p-6 rounded-2xl text-center">
              <div className="text-3xl font-bold font-heading text-indigo-400 mb-1">10+</div>
              <div className="text-xs font-mono text-slate-500 uppercase tracking-wider">AI Agents</div>
            </div>
            <div className="glass-card p-6 rounded-2xl text-center">
              <div className="text-3xl font-bold font-heading text-amber-400 mb-1">24/7</div>
              <div className="text-xs font-mono text-slate-500 uppercase tracking-wider">Uptime</div>
            </div>
            <div className="glass-card p-6 rounded-2xl text-center">
              <div className="text-3xl font-bold font-heading text-emerald-400 mb-1">100%</div>
              <div className="text-xs font-mono text-slate-500 uppercase tracking-wider">Zo Native</div>
            </div>
          </section>
        </main>

        <footer className="border-t border-white/5 py-12 bg-black/20">
          <div className="max-w-7xl mx-auto px-6 flex flex-col md:flex-row justify-between items-center gap-8">
            <div className="flex items-center gap-2 opacity-50">
              <span className="font-heading font-bold tracking-tight text-slate-400">
                zenlyte<span className="text-cyan-400">.</span>
              </span>
              <span className="text-xs text-slate-600">© 2026</span>
            </div>
            
            <div className="flex items-center gap-6">
              <a href="https://github.com/Zenlyte" target="_blank" rel="noopener" className="text-slate-500 hover:text-white transition-colors">
                <Github className="w-5 h-5" />
              </a>
              <a href="https://x.com/z3nlyte" target="_blank" rel="noopener" className="text-slate-500 hover:text-white transition-colors">
                <Twitter className="w-5 h-5" />
              </a>
              <a href="https://linkedin.com/in/Cbchow" target="_blank" rel="noopener" className="text-slate-500 hover:text-white transition-colors">
                <Linkedin className="w-5 h-5" />
              </a>
            </div>

            <p className="text-xs text-slate-600 flex items-center gap-2">
              Designed for 
              <a href="https://zo.computer" target="_blank" rel="noopener" className="transition-colors hover:text-white" style={{ color: COLORS.cyan }}>
                Zo Computer
              </a>
            </p>
          </div>
        </footer>
      </div>
    </>
  );
}
```

### `/404` (page, public)

```tsx
import { useState, useEffect } from "react";

export default function NotFound() {
  const [glitch, setGlitch] = useState(false);
  const [cmd, setCmd] = useState("");
  const [output, setOutput] = useState([]);

  useEffect(() => {
    const iv = setInterval(() => setGlitch(v => !v), 3000);
    return () => clearInterval(iv);
  }, []);

  const handleKey = (e) => {
    if (e.key === "Enter") {
      const c = cmd.toLowerCase().trim();
      let out = `zos: command not found: ${cmd}`;
      if (c === "help") out = "Available commands: ls, cd, clear, home, reboot";
      if (c === "ls") out = "about.md  projects/  skills/  secret_key.enc";
      if (c === "home") window.location.href = "/";
      if (c === "reboot") window.location.reload();
      if (c === "clear") {
        setOutput([]);
        setCmd("");
        return;
      }
      setOutput(prev => [...prev, `zenlyte@zos:~$ ${cmd}`, out]);
      setCmd("");
    }
  };

  return (
    <div className="nf-wrap">
      <style>{CSS}</style>
      <div className="nf-container">
        <div className={`nf-code ${glitch ? "glitch" : ""}`} data-text="404">
          404
        </div>
        <div className="nf-title">ROUTE NOT FOUND</div>
        <p className="nf-desc">
          The requested module could not be initialized. The path may have moved 
          to a different memory address or has been purged from the kernel.
        </p>

        <div className="nf-terminal">
          <div className="nf-term-body">
            {output.map((line, i) => (
              <div key={i} className="nf-term-line">{line}</div>
            ))}
            <div className="nf-term-input-row">
              <span className="nf-prompt">zenlyte@zos:~$</span>
              <input 
                className="nf-term-input"
                value={cmd}
                onChange={e => setCmd(e.target.value)}
                onKeyDown={handleKey}
                autoFocus
              />
            </div>
          </div>
        </div>

        <div className="nf-nav">
          <a href="/" className="nf-link">[ RETURN HOME ]</a>
          <a href="/zos" className="nf-link">[ REBOOT ZOS ]</a>
        </div>
      </div>
    </div>
  );
}

const CSS = [
  "@import url('https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;700&family=Space+Grotesk:wght@700&display=swap');",
  ".nf-wrap{min-height:100vh;background:#0a0a0f;color:#e8e0d4;display:flex;align-items:center;justify-content:center;font-family:'JetBrains Mono',monospace;padding:24px;overflow:hidden}",
  ".nf-container{max-width:600px;width:100%;text-align:center}",
  ".nf-code{font-size:120px;font-weight:900;line-height:1;margin-bottom:8px;color:#c08b5c;position:relative;font-family:'Space Grotesk',sans-serif}",
  ".nf-code.glitch::before,.nf-code.glitch::after{content:attr(data-text);position:absolute;top:0;left:0;width:100%;height:100%;opacity:0.8}",
  ".nf-code.glitch::before{left:2px;text-shadow:-2px 0 #5daa96;clip:rect(44px,450px,56px,0);animation:glitch-anim 5s infinite linear alternate-reverse}",
  ".nf-code.glitch::after{left:-2px;text-shadow:-2px 0 #e87171;clip:rect(44px,450px,56px,0);animation:glitch-anim2 5s infinite linear alternate-reverse}",
  "@keyframes glitch-anim{0%{clip:rect(31px,9999px,94px,0)}5%{clip:rect(70px,9999px,71px,0)}...100%{clip:rect(67px,9999px,62px,0)}}",
  ".nf-title{font-size:18px;font-weight:700;letter-spacing:4px;margin-bottom:24px;color:#5daa96}",
  ".nf-desc{font-size:14px;color:#94938e;line-height:1.6;margin-bottom:40px}",
  ".nf-terminal{background:rgba(21,21,25,0.8);border:1px solid rgba(232,224,212,0.1);border-radius:12px;text-align:left;margin-bottom:40px;box-shadow:0 20px 50px rgba(0,0,0,0.3)}",
  ".nf-term-body{padding:16px;height:180px;overflow-y:auto;font-size:13px}",
  ".nf-term-line{color:#94938e;margin-bottom:4px}",
  ".nf-term-input-row{display:flex;gap:8px;align-items:center}",
  ".nf-prompt{color:#c08b5c;font-weight:700}",
  ".nf-term-input{background:transparent;border:none;outline:none;color:#e8e0d4;flex:1;font-family:inherit;font-size:inherit}",
  ".nf-nav{display:flex;gap:20px;justify-content:center}",
  ".nf-link{padding:10px 20px;border:1px solid rgba(232,224,212,0.2);border-radius:8px;color:#e8e0d4;text-decoration:none;font-family:'JetBrains Mono',monospace;font-size:13px;transition:all 0.2s}",
  ".nf-link:hover{border-color:#c08b5c;background:rgba(192,139,92,0.08);color:#c08b5c}",
].join("\n");
```

