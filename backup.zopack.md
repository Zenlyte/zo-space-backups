---
format: zopack
version: "1.0"
name: zo-space-backup
author: unknown.zo.computer
routes: 132
exported: 2026-06-05
---

# zo-space-backup

## Routes

### `/` (page, public)

```tsx
import { useState, useEffect, useRef } from "react";
import {
  ArrowRight, Github, Twitter, Linkedin, MessageSquare, Send, CheckCircle,
  Database, Bot, Users, Wrench, ExternalLink, Gamepad2, Sparkles, Clock,
  Tag, ChevronDown, Menu, X,
  LayoutDashboard, Palette, Settings, Share2, Briefcase, PenLine, Lock
} from "lucide-react";

const COLORS = {
  bg: "#0a0a0f",
  card: "#0f1117",
  cardHover: "#141420",
  cyan: "#06b6d4",
  cyanLight: "#22d3ee",
  indigo: "#6366f1",
  indigoLight: "#818cf8",
  muted: "#94a3b8",
  dimmed: "#64748b",
  border: "rgba(255,255,255,0.08)",
  borderHover: "rgba(6,182,212,0.4)",
};

const PROJECTS = [
  { name: "Canadian Daycare Finder", desc: "A web service for Canadian parents to find, filter, and evaluate daycares using provincial data enriched with Google Maps and news.", status: "planned", tags: ["Web", "Data", "Maps"], link: null },
  { name: "Theme Gallery", desc: "30+ design system themes for Zo Space with one-click application and live preview.", status: "completed", tags: ["Zo Space", "React", "Design"], link: "/zo-space-theme-gallery" },
  { name: "Mengram", desc: "Local-first memory system with knowledge graph, proactive environmental anchoring, and failure-driven procedural extraction.", status: "completed", tags: ["Python", "SQLite", "AI"], link: "/blog/memory-implementation" },
  { name: "Zo Icon Configurator", desc: "Custom Zo Computer logo generator with AI enhancement, theme presets, and canvas rendering.", status: "completed", tags: ["React", "AI", "Canvas"], link: "/icon-configurator" },
  { name: "JobOps", desc: "Advanced job search orchestration platform with automated scraping, AI scoring, and resume tailoring.", status: "in-progress", tags: ["TypeScript", "AI", "Automation"], link: null },
  { name: "Straico Rust Proxy", desc: "High-performance Rust-based proxy for Straico and Ollama model orchestration with streaming support.", status: "completed", tags: ["Rust", "API", "AI"], link: null },
  { name: "Zo Discord Bot", desc: "Discord integration for Zo Computer with thread management, model overrides, and persistent memory.", status: "completed", tags: ["Python", "Discord", "AI"], link: null },
  { name: "Temporal Dashboard", desc: "Temporal development server and workflow orchestration dashboard for complex distributed systems.", status: "in-progress", tags: ["Infra", "Workflow", "Orchestration"], link: null },
  { name: "OpenClaw Dashboard", desc: "Management interface for OpenClaw multi-machine agent orchestration and distributed AI workloads.", status: "in-progress", tags: ["Python", "Agents", "Infra"], link: null },
  { name: "Skill Gallery", desc: "Browsable gallery of Zo Computer skills with search, filtering, and easy installation.", status: "in-progress", tags: ["Zo Space", "Community"], link: null },
  { name: "Zo Status", desc: "System health and service monitoring dashboard for tracking Zo Computer performance and availability.", status: "completed", tags: ["Monitoring", "Dashboard"], link: null },
  { name: "Published Skills & PRs", desc: "Community contributions to the Zo skills ecosystem, open-source tools and integrations.", status: "completed", tags: ["TypeScript", "Open Source"], link: null },
  { name: "Automations", desc: "Scheduled agents, notifications, digests, and workflow automation on Zo Computer.", status: "completed", tags: ["Agents", "Integrations"], link: null },
  { name: "Receipts", desc: "Shared household expense tracker for tracking receipts and spending.", status: "completed", tags: ["Finance", "Zo Space"], link: null },
  { name: "Dashboard", desc: "Shared hub for schedules, tasks, and household information management.", status: "in-progress", tags: ["React", "Zo Space"], link: null },
  { name: "Personal OS", desc: "Task management and personal productivity system built on Zo.", status: "in-progress", tags: ["Productivity", "Zo Space"], link: null },
  { name: "Docs", desc: "Project documentation and knowledge base for the entire personal Zo ecosystem.", status: "in-progress", tags: ["Documentation", "Wiki"], link: "/docs" },
  { name: "Prompt Gallery", desc: "Template library for curated and saved prompts across various AI use cases.", status: "in-progress", tags: ["Productivity", "AI"], link: null },
  { name: "MCP Staging", desc: "Staging environment for developing and testing Model Context Protocol (MCP) servers.", status: "in-progress", tags: ["MCP", "Development"], link: null },
];

const SOCIAL_LINKS = [
  { name: "X / Twitter", icon: Twitter, url: "https://x.com/curtastrophe_", color: "#1da1f2" },
  { name: "LinkedIn", icon: Linkedin, url: "https://linkedin.com/in/curtischow", color: "#0a66c2" },
  { name: "GitHub", icon: Github, url: "https://github.com/curtastrophe", color: "#f0f6fc" },
  { name: "Reddit", icon: MessageSquare, url: "https://reddit.com/user/GoomiBare", color: "#ff4500" },
];

const NAV_ITEMS = ["About", "Projects", "Blog", "Social", "Contact"];

const ZENNY_IDLE = "/pets/zenny-idle-v2.png";
const ZENNY_RUN_RIGHT = "/pets/zenny-running-right-v2.png";
const ZENNY_RUN_LEFT = "/pets/zenny-running-left-v2.png";

const ZENNY_STATES = {
  idle: { src: ZENNY_IDLE, frames: 6 },
  left: { src: ZENNY_RUN_LEFT, frames: 8 },
  right: { src: ZENNY_RUN_RIGHT, frames: 8 },
} as const;

function DraggableZenny() {
  const [position, setPosition] = useState({ x: 24, y: 120 });
  const [mode, setMode] = useState<keyof typeof ZENNY_STATES>("idle");
  const [frame, setFrame] = useState(0);
  const dragRef = useRef({ active: false, pointerId: -1, offsetX: 0, offsetY: 0, lastX: 0 });
  const width = 96;
  const height = 104;
  const pet = ZENNY_STATES[mode];

  useEffect(() => {
    const placeZenny = () => {
      setPosition({
        x: Math.max(8, window.innerWidth - width - 32),
        y: window.innerWidth < 768 ? 96 : 132,
      });
    };
    placeZenny();
    window.addEventListener("resize", placeZenny);
    return () => window.removeEventListener("resize", placeZenny);
  }, []);

  useEffect(() => {
    setFrame(0);
    const id = window.setInterval(() => {
      setFrame((current) => (current + 1) % ZENNY_STATES[mode].frames);
    }, mode === "idle" ? 180 : 95);
    return () => window.clearInterval(id);
  }, [mode]);

  const clamp = (x: number, y: number) => ({
    x: Math.max(8, Math.min(window.innerWidth - width - 8, x)),
    y: Math.max(84, Math.min(window.innerHeight - height - 8, y)),
  });

  const onPointerDown = (event: React.PointerEvent<HTMLDivElement>) => {
    event.currentTarget.setPointerCapture(event.pointerId);
    dragRef.current = {
      active: true,
      pointerId: event.pointerId,
      offsetX: event.clientX - position.x,
      offsetY: event.clientY - position.y,
      lastX: event.clientX,
    };
  };

  const onPointerMove = (event: React.PointerEvent<HTMLDivElement>) => {
    const drag = dragRef.current;
    if (!drag.active || drag.pointerId !== event.pointerId) return;
    const dx = event.clientX - drag.lastX;
    if (dx > 1) setMode("right");
    if (dx < -1) setMode("left");
    drag.lastX = event.clientX;
    setPosition(clamp(event.clientX - drag.offsetX, event.clientY - drag.offsetY));
  };

  const stopDragging = (event: React.PointerEvent<HTMLDivElement>) => {
    if (!dragRef.current.active || dragRef.current.pointerId !== event.pointerId) return;
    dragRef.current.active = false;
    setMode("idle");
  };

  return (
    <div
      role="button"
      aria-label="Drag Zenny"
      title="Drag Zenny"
      onPointerDown={onPointerDown}
      onPointerMove={onPointerMove}
      onPointerUp={stopDragging}
      onPointerCancel={stopDragging}
      className="fixed z-[60] cursor-grab active:cursor-grabbing select-none touch-none"
      style={{
        left: position.x,
        top: position.y,
        width,
        height,
        imageRendering: "pixelated",
        backgroundImage: `url(${pet.src})`,
        backgroundRepeat: "no-repeat",
        backgroundSize: `${8 * width}px ${height}px`,
        backgroundPosition: `-${frame * width}px 0px`,
        filter: "drop-shadow(0 10px 18px rgba(0,0,0,0.35))",
      }}
    />
  );
}

function HexAvatar({ size = 140 }: { size?: number }) {
  const r = size / 2;
  const points = Array.from({ length: 6 }, (_, i) => {
    const angle = (Math.PI / 3) * i - Math.PI / 2;
    return `${r + r * 0.92 * Math.cos(angle)},${r + r * 0.92 * Math.sin(angle)}`;
  }).join(" ");
  const outerPoints = Array.from({ length: 6 }, (_, i) => {
    const angle = (Math.PI / 3) * i - Math.PI / 2;
    return `${r + r * Math.cos(angle)},${r + r * Math.sin(angle)}`;
  }).join(" ");

  return (
    <div className="relative" style={{ width: size, height: size }}>
      <svg width={size} height={size} viewBox={`0 0 ${size} ${size}`}>
        <defs>
          <linearGradient id="hex-grad" x1="0%" y1="0%" x2="100%" y2="100%">
            <stop offset="0%" stopColor={COLORS.cyan} />
            <stop offset="100%" stopColor={COLORS.indigo} />
          </linearGradient>
          <clipPath id="hex-clip">
            <polygon points={points} />
          </clipPath>
        </defs>
        <polygon points={outerPoints} fill="none" stroke="url(#hex-grad)" strokeWidth="2.5" />
        <polygon points={points} fill={COLORS.card} />
        <image
          href="/images/avatar.png"
          x="0"
          y="0"
          width={size}
          height={size}
          clipPath="url(#hex-clip)"
          preserveAspectRatio="xMidYMid slice"
        />
      </svg>
      <div className="absolute inset-0 opacity-30" style={{
        background: `radial-gradient(circle at 30% 30%, ${COLORS.cyan}33, transparent 60%)`,
        clipPath: "polygon(50% 0%, 100% 25%, 100% 75%, 50% 100%, 0% 75%, 0% 25%)",
      }} />
    </div>
  );
}

function SectionHeader({ label, title, highlight }: { label: string; title: string; highlight: string }) {
  return (
    <div className="text-center mb-16">
      <span className="text-xs font-mono tracking-widest uppercase" style={{ color: COLORS.cyan }}>{label}</span>
      <h2 className="font-heading text-3xl md:text-5xl font-bold mt-3">
        {title}{" "}
        <span style={{
          background: `linear-gradient(135deg, ${COLORS.cyan}, ${COLORS.indigo})`,
          WebkitBackgroundClip: "text",
          WebkitTextFillColor: "transparent",
        }}>{highlight}</span>
      </h2>
    </div>
  );
}

function StatusBadge({ status }: { status: string }) {
  const config: Record<string, { bg: string; text: string; label: string }> = {
    completed: { bg: "rgba(34,197,94,0.15)", text: "#4ade80", label: "Completed" },
    "in-progress": { bg: `${COLORS.cyan}20`, text: COLORS.cyanLight, label: "In Progress" },
    planned: { bg: `${COLORS.indigo}20`, text: COLORS.indigoLight, label: "Planned" },
  };
  const c = config[status] || config.planned;
  return (
    <span className="inline-flex items-center px-2.5 py-1 rounded-full text-xs font-mono tracking-wider uppercase"
      style={{ background: c.bg, color: c.text, border: `1px solid ${c.text}30` }}>
      {c.label}
    </span>
  );
}

interface PostMeta { slug: string; title: string; excerpt: string; date: string; tags: string[]; readTime: string; }

export default function Home() {
  const [mounted, setMounted] = useState(false);
  const [activeFilter, setActiveFilter] = useState("all");
  const [posts, setPosts] = useState<PostMeta[]>([]);
  const [formState, setFormState] = useState({ name: "", email: "", message: "" });
  const [sending, setSending] = useState(false);
  const [sent, setSent] = useState(false);
  const [formError, setFormError] = useState("");
  const [mobileNav, setMobileNav] = useState(false);
  const [scrolled, setScrolled] = useState(false);
  const [navLinks, setNavLinks] = useState<any[]>([]);
  const [navAuth, setNavAuth] = useState(false);
  const [pagesOpen, setPagesOpen] = useState(false);
  const pagesRef = useRef<HTMLDivElement>(null);

  useEffect(() => {
    setMounted(true);
    fetch("/api/blog", { headers: { Accept: "application/json" } })
      .then(r => r.json())
      .then(d => setPosts((d.posts || []).slice(0, 3)))
      .catch(() => {});
    fetch("/api/nav-links", { headers: { Accept: "application/json" } })
      .then(r => r.json())
      .then(d => { setNavLinks(d.links || []); setNavAuth(d.authenticated); })
      .catch(() => {});
    const onScroll = () => setScrolled(window.scrollY > 40);
    window.addEventListener("scroll", onScroll);
    const onClickOutside = (e: MouseEvent) => {
      if (pagesRef.current && !pagesRef.current.contains(e.target as Node)) {
        setPagesOpen(false);
      }
    };
    document.addEventListener("mousedown", onClickOutside);
    return () => {
      window.removeEventListener("scroll", onScroll);
      document.removeEventListener("mousedown", onClickOutside);
    };
  }, []);

  const handleSubmit = async (e: React.FormEvent) => {
    e.preventDefault();
    setSending(true);
    setFormError("");
    try {
      const res = await fetch("/api/contact", {
        method: "POST",
        headers: { "Content-Type": "application/json", Accept: "application/json" },
        body: JSON.stringify(formState),
      });
      const data = await res.json();
      if (!res.ok) throw new Error(data.error || "Something went wrong");
      setSent(true);
      setFormState({ name: "", email: "", message: "" });
    } catch (err: any) {
      setFormError(err.message || "Something went wrong");
    } finally {
      setSending(false);
    }
  };

  const filteredProjects = activeFilter === "all" ? PROJECTS : PROJECTS.filter(p => p.status === activeFilter);

  const scrollToSection = (id: string) => {
    const el = document.getElementById(id);
    if (el) {
      const navHeight = 80;
      const targetY = el.getBoundingClientRect().top + window.scrollY - navHeight;
      window.scrollTo({ top: targetY, behavior: "smooth" });
    } else {
      window.scrollTo({ top: 0, behavior: "smooth" });
    }
  };

  const ICON_MAP: Record<string, any> = {
    "pencil": PenLine,
    "palette": Palette,
    "settings": Settings,
    "layout-dashboard": LayoutDashboard,
    "sparkles": Sparkles,
    "share-2": Share2,
    "clock": Clock,
    "briefcase": Briefcase,
  };

  const filteredNavLinks = navLinks.filter((link: any) => link.path !== "/blog");

  return (
    <>
      <style>{`
        @import url('https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@400;500;600;700&family=Inter:wght@400;500;600&family=JetBrains+Mono:wght@400;500&display=swap');
        * { box-sizing: border-box; }
        html { scroll-behavior: smooth; }
        .font-heading { font-family: 'Space Grotesk', sans-serif; }
        .font-body { font-family: 'Inter', sans-serif; }
        .font-mono { font-family: 'JetBrains Mono', monospace; }
        .bg-grid {
          background-size: 60px 60px;
          background-image:
            linear-gradient(to right, rgba(99,102,241,0.06) 1px, transparent 1px),
            linear-gradient(to bottom, rgba(6,182,212,0.06) 1px, transparent 1px);
        }
        @keyframes float { 0%,100%{transform:translateY(0)} 50%{transform:translateY(-12px)} }
        @keyframes glow-pulse { 0%,100%{opacity:0.4} 50%{opacity:0.8} }
        .animate-float { animation: float 6s ease-in-out infinite; }
        .animate-glow { animation: glow-pulse 4s ease-in-out infinite; }
        .glass { background: rgba(15,17,23,0.7); backdrop-filter: blur(16px); border: 1px solid rgba(255,255,255,0.08); }
        .card-hover { transition: all 0.3s ease; }
        .card-hover:hover { border-color: rgba(6,182,212,0.4); box-shadow: 0 0 30px -10px rgba(6,182,212,0.15); transform: translateY(-2px); }
      `}</style>

      <div className="min-h-screen text-white font-body relative overflow-hidden" style={{ background: COLORS.bg }}>
        <DraggableZenny />
        {/* Background effects */}
        <div className="absolute inset-0 bg-grid pointer-events-none" />
        <div className="absolute pointer-events-none" style={{ top: -200, left: "30%", width: 500, height: 500, background: COLORS.cyan, borderRadius: "50%", opacity: 0.04, filter: "blur(150px)" }} />
        <div className="absolute pointer-events-none" style={{ bottom: -200, right: "10%", width: 400, height: 400, background: COLORS.indigo, borderRadius: "50%", opacity: 0.05, filter: "blur(120px)" }} />

        {/* NAV */}
        <nav className={`fixed top-0 left-0 right-0 z-50 transition-all duration-300 ${scrolled ? "glass shadow-lg" : ""}`}>
          <div className="max-w-7xl mx-auto px-6 py-4 flex items-center justify-between">
            <a href="/" className="flex items-center gap-2.5">
              <div className="w-8 h-8 rounded-lg flex items-center justify-center" style={{
                background: `linear-gradient(135deg, ${COLORS.cyan}, ${COLORS.indigo})`,
                boxShadow: `0 0 20px -5px ${COLORS.cyan}80`,
              }}>
                <span className="text-white font-bold text-sm font-heading">C</span>
              </div>
              <span className="font-heading font-semibold text-lg">curtastrophe</span>
            </a>
            <div className="hidden md:flex items-center gap-6">
              {NAV_ITEMS.map(item => (
                item === "Blog" ? (
                  <a key={item} href="/blog"
                    className="text-xs font-mono tracking-widest uppercase transition-colors hover:text-white" style={{ color: COLORS.muted }}>
                    {item}
                  </a>
                ) : (
                  <button key={item} onClick={() => scrollToSection(item.toLowerCase())}
                    className="text-xs font-mono tracking-widest uppercase transition-colors hover:text-white bg-transparent border-none cursor-pointer" style={{ color: COLORS.muted }}>
                    {item}
                  </button>
                )
              ))}
              {filteredNavLinks.length > 0 && (
                <div className="relative" ref={pagesRef}>
                  <button
                    onClick={() => setPagesOpen(!pagesOpen)}
                    className="flex items-center gap-1.5 text-xs font-mono tracking-widest uppercase transition-colors hover:text-white"
                    style={{ color: COLORS.muted }}
                  >
                    Pages <ChevronDown className={`w-3 h-3 transition-transform duration-200 ${pagesOpen ? "rotate-180" : ""}`} />
                  </button>
                  {pagesOpen && (
                    <div className="absolute right-0 top-full mt-2 w-64 glass rounded-xl p-3 z-50" style={{ border: `1px solid ${COLORS.border}` }}>
                      <div className="flex flex-col gap-1">
                        {filteredNavLinks.map((link: any) => {
                          const IconComp = ICON_MAP[link.icon] || ExternalLink;
                          return (
                            <a key={link.path} href={link.path}
                              className="flex items-start gap-3 p-2.5 rounded-lg transition-colors hover:bg-white/5">
                              <IconComp className="w-4 h-4 mt-0.5" style={{ color: link.category === "private" ? COLORS.indigoLight : COLORS.cyan }} />
                              <div className="flex-1 min-w-0">
                                <div className="flex items-center gap-2">
                                  <span className="text-sm font-medium truncate">{link.name}</span>
                                  {link.category === "private" && (
                                    <span className="px-1.5 py-0.5 rounded text-[10px] font-mono uppercase tracking-wider"
                                      style={{ background: `${COLORS.indigo}20`, color: COLORS.indigoLight }}>
                                      Private
                                    </span>
                                  )}
                                </div>
                                <p className="text-xs mt-0.5 truncate" style={{ color: COLORS.dimmed }}>{link.description}</p>
                              </div>
                            </a>
                          );
                        })}
                      </div>
                    </div>
                  )}
                </div>
              )}
            </div>
            <button className="md:hidden" onClick={() => setMobileNav(!mobileNav)}>
              {mobileNav ? <X className="w-5 h-5" /> : <Menu className="w-5 h-5" />}
            </button>
          </div>
          {mobileNav && (
            <div className="md:hidden glass border-t" style={{ borderColor: COLORS.border }}>
              <div className="px-6 py-4 flex flex-col gap-3">
                {NAV_ITEMS.map(item => (
                  item === "Blog" ? (
                    <a key={item} href="/blog"
                      onClick={() => setMobileNav(false)}
                      className="text-sm font-mono tracking-wider uppercase py-2" style={{ color: COLORS.muted }}>
                      {item}
                    </a>
                  ) : (
                    <button key={item} onClick={() => { scrollToSection(item.toLowerCase()); setMobileNav(false); }}
                      className="text-sm font-mono tracking-wider uppercase py-2 text-left bg-transparent border-none cursor-pointer" style={{ color: COLORS.muted }}>
                      {item}
                    </button>
                  )
                ))}
                {filteredNavLinks.length > 0 && (
                  <>
                    <div className="h-px my-1" style={{ background: COLORS.border }} />
                    <span className="text-xs font-mono tracking-widest uppercase pt-1" style={{ color: COLORS.dimmed }}>
                      Pages {navAuth && <Lock className="w-3 h-3 inline ml-1" style={{ color: COLORS.cyan }} />}
                    </span>
                    {filteredNavLinks.map((link: any) => {
                      const IconComp = ICON_MAP[link.icon] || ExternalLink;
                      return (
                        <a key={link.path} href={link.path}
                          onClick={() => setMobileNav(false)}
                          className="flex items-center gap-3 py-2">
                          <IconComp className="w-4 h-4" style={{ color: link.category === "private" ? COLORS.indigoLight : COLORS.cyan }} />
                          <span className="text-sm" style={{ color: COLORS.muted }}>{link.name}</span>
                          {link.category === "private" && (
                            <span className="px-1.5 py-0.5 rounded text-[10px] font-mono uppercase" style={{ background: `${COLORS.indigo}20`, color: COLORS.indigoLight }}>
                              Private
                            </span>
                          )}
                        </a>
                      );
                    })}
                  </>
                )}
              </div>
            </div>
          )}
        </nav>

        {/* HERO */}
        <section className="relative z-10 max-w-7xl mx-auto px-6 pt-28 pb-20 md:pt-36 md:pb-28">
          <div className="grid md:grid-cols-2 gap-12 items-center">
            <div>
              <div className="inline-flex items-center gap-2 px-3 py-1.5 rounded-full mb-6" style={{ background: "rgba(255,255,255,0.05)", border: `1px solid ${COLORS.border}` }}>
                <span className="w-2 h-2 rounded-full animate-pulse" style={{ background: COLORS.cyan }} />
                <span className="text-xs font-mono tracking-wider uppercase" style={{ color: COLORS.muted }}>Building things on Zo Space</span>
              </div>

              <h1 className="font-heading text-4xl sm:text-5xl md:text-6xl font-bold leading-tight mb-4">
                Zenlyte
              </h1>
              <p className="font-mono text-sm mb-6" style={{ color: COLORS.cyan }}>@curtastrophe</p>
              <p className="text-lg md:text-xl leading-relaxed mb-8 max-w-lg" style={{ color: COLORS.muted }}>
                Data & Analytics professional and AI builder. Turning raw data into decisions, and exploring the frontier of AI on Zo Computer.
              </p>

              <div className="flex flex-wrap gap-4">
                <button onClick={() => scrollToSection("projects")} className="inline-flex items-center gap-2 px-6 py-3 rounded-full text-white font-semibold text-sm tracking-wider uppercase transition-all duration-300 hover:scale-105" style={{
                  background: `linear-gradient(135deg, ${COLORS.cyan}, ${COLORS.indigo})`,
                  boxShadow: `0 0 25px -5px ${COLORS.cyan}60`,
                  border: "none", cursor: "pointer",
                }}>
                  View Projects <ArrowRight className="w-4 h-4" />
                </button>
                <a href="/blog" className="inline-flex items-center gap-2 px-6 py-3 rounded-full font-semibold text-sm tracking-wider uppercase transition-all duration-300 hover:bg-white/10" style={{
                  border: "2px solid rgba(255,255,255,0.2)",
                }}>
                  Read Blog
                </a>
              </div>
            </div>

            <div className="flex items-center justify-center">
              <div className="animate-float relative">
                <HexAvatar size={180} />
                <div className="absolute -top-2 -right-8 px-3 py-1.5 rounded-lg glass text-xs font-mono animate-bounce" style={{ animationDuration: "3s", color: COLORS.cyanLight }}>
                  Data & AI
                </div>
                <div className="absolute -bottom-2 -left-8 px-3 py-1.5 rounded-lg glass text-xs font-mono animate-bounce" style={{ animationDuration: "4s", animationDelay: "1s", color: COLORS.indigoLight }}>
                  Builder
                </div>
              </div>
            </div>
          </div>
        </section>

        {/* ABOUT */}
        <section id="about" className="relative z-10 max-w-7xl mx-auto px-6 py-24">
          <SectionHeader label="About" title="Who I" highlight="am" />
          <div className="grid md:grid-cols-5 gap-8">
            <div className="md:col-span-2">
              <p className="text-lg leading-relaxed mb-4" style={{ color: COLORS.muted }}>
                Data & Analytics professional by day, AI tinkerer by night. Building tools, agents, and dashboards on Zo Computer while exploring what's possible at the intersection of data and artificial intelligence.
              </p>
              <p className="text-sm leading-relaxed" style={{ color: COLORS.muted }}>
                Somewhere between a beginner software dev and a power user who ships. Interested in the intersection of data, AI, and productivity systems.
              </p>
            </div>
            <div className="md:col-span-3 grid sm:grid-cols-2 gap-4">
              {[
                { icon: Database, title: "Data & Analytics", desc: "Turning raw data into decisions and insights that drive impact." },
                { icon: Bot, title: "AI & Automation", desc: "Agents, LLMs, memory systems, and intelligent workflows." },
                { icon: Users, title: "Community", desc: "Leading EDBA and contributing to the Zo Computer community." },
                { icon: Wrench, title: "Building", desc: "Shipping skills, tools, dashboards, and open-source projects." },
              ].map(card => (
                <div key={card.title} className="p-6 rounded-xl card-hover" style={{ background: COLORS.card, border: `1px solid ${COLORS.border}` }}>
                  <div className="w-10 h-10 rounded-lg flex items-center justify-center mb-4" style={{ background: `${COLORS.cyan}15`, border: `1px solid ${COLORS.cyan}30` }}>
                    <card.icon className="w-5 h-5" style={{ color: COLORS.cyan }} />
                  </div>
                  <h3 className="font-heading font-semibold text-lg mb-2">{card.title}</h3>
                  <p className="text-sm leading-relaxed" style={{ color: COLORS.muted }}>{card.desc}</p>
                </div>
              ))}
            </div>
          </div>
        </section>

        {/* PROJECTS */}
        <section id="projects" className="relative z-10 py-24" style={{ background: COLORS.card }}>
          <div className="max-w-7xl mx-auto px-6">
            <SectionHeader label="Projects" title="What I'm" highlight="building" />
            <div className="flex flex-wrap justify-center gap-3 mb-12">
              {[
                { key: "all", label: "All" },
                { key: "completed", label: "Completed" },
                { key: "in-progress", label: "In Progress" },
                { key: "planned", label: "Planned" },
              ].map(f => (
                <button key={f.key} onClick={() => setActiveFilter(f.key)}
                  className="px-4 py-2 rounded-full text-xs font-mono tracking-wider uppercase transition-all duration-200"
                  style={{
                    background: activeFilter === f.key ? `linear-gradient(135deg, ${COLORS.cyan}, ${COLORS.indigo})` : "rgba(255,255,255,0.05)",
                    color: activeFilter === f.key ? "white" : COLORS.muted,
                    border: `1px solid ${activeFilter === f.key ? "transparent" : COLORS.border}`,
                  }}>
                  {f.label}
                </button>
              ))}
            </div>
            <div className="grid md:grid-cols-2 lg:grid-cols-3 gap-6">
              {filteredProjects.map(p => (
                <div key={p.name} className="p-6 rounded-xl card-hover flex flex-col" style={{ background: COLORS.bg, border: `1px solid ${COLORS.border}` }}>
                  <div className="flex items-start justify-between mb-4">
                    <StatusBadge status={p.status} />
                    {p.link && (
                      <a href={p.link} className="transition-colors hover:opacity-80" style={{ color: COLORS.cyan }}>
                        <ExternalLink className="w-4 h-4" />
                      </a>
                    )}
                  </div>
                  <h3 className="font-heading font-semibold text-lg mb-2">{p.name}</h3>
                  <p className="text-sm leading-relaxed mb-4 flex-grow" style={{ color: COLORS.muted }}>{p.desc}</p>
                  <div className="flex flex-wrap gap-1.5">
                    {p.tags.map(t => (
                      <span key={t} className="px-2 py-0.5 rounded text-xs font-mono" style={{ background: `${COLORS.indigo}15`, color: COLORS.indigoLight }}>
                        {t}
                      </span>
                    ))}
                  </div>
                </div>
              ))}
            </div>
          </div>
        </section>

        {/* BLOG PREVIEW */}
        <section id="blog" className="relative z-10 max-w-7xl mx-auto px-6 py-24">
          <SectionHeader label="Blog" title="Latest" highlight="posts" />
          {posts.length > 0 ? (
            <div className="grid md:grid-cols-3 gap-6 mb-10">
              {posts.map(post => {
                const d = new Date(post.date + "T00:00:00").toLocaleDateString("en-CA", { month: "short", day: "numeric", year: "numeric" });
                return (
                  <a key={post.slug} href={`/blog/${post.slug}`} className="block p-6 rounded-xl card-hover" style={{ background: COLORS.card, border: `1px solid ${COLORS.border}` }}>
                    <div className="h-1 w-12 rounded-full mb-5" style={{ background: `linear-gradient(135deg, ${COLORS.cyan}, ${COLORS.indigo})` }} />
                    <div className="flex flex-wrap gap-1.5 mb-3">
                      {post.tags.slice(0, 2).map(t => (
                        <span key={t} className="flex items-center gap-1 px-2 py-0.5 rounded-full text-xs font-mono" style={{ background: `${COLORS.cyan}15`, color: COLORS.cyan, border: `1px solid ${COLORS.cyan}25` }}>
                          <Tag className="w-2.5 h-2.5" />{t}
                        </span>
                      ))}
                    </div>
                    <h3 className="font-heading font-semibold text-lg mb-2 leading-tight">{post.title}</h3>
                    <p className="text-sm leading-relaxed mb-4 line-clamp-2" style={{ color: COLORS.muted }}>{post.excerpt}</p>
                    <div className="flex items-center gap-3 text-xs font-mono" style={{ color: COLORS.dimmed }}>
                      <span>{d}</span>
                      <span className="flex items-center gap-1"><Clock className="w-3 h-3" />{post.readTime}</span>
                    </div>
                  </a>
                );
              })}
            </div>
          ) : (
            <div className="text-center py-12">
              <p className="font-mono text-sm" style={{ color: COLORS.dimmed }}>No posts yet. Check back soon.</p>
            </div>
          )}
          <div className="text-center">
            <a href="/blog" className="inline-flex items-center gap-2 text-sm font-mono tracking-wider uppercase transition-colors" style={{ color: COLORS.cyan }}>
              View all posts <ArrowRight className="w-4 h-4" />
            </a>
          </div>
        </section>

        {/* SOCIAL */}
        <section id="social" className="relative z-10 py-24" style={{ background: COLORS.card }}>
          <div className="max-w-7xl mx-auto px-6">
            <SectionHeader label="Social" title="Find me" highlight="online" />
            <div className="grid sm:grid-cols-2 md:grid-cols-4 gap-6">
              {SOCIAL_LINKS.map(s => (
                <a key={s.name} href={s.url} target="_blank" rel="noopener noreferrer"
                  className="group p-6 rounded-xl card-hover text-center" style={{ background: COLORS.bg, border: `1px solid ${COLORS.border}` }}>
                  <div className="w-12 h-12 rounded-full mx-auto mb-4 flex items-center justify-center transition-all duration-300 group-hover:scale-110" style={{ background: `${s.color}15`, border: `1px solid ${s.color}30` }}>
                    <s.icon className="w-5 h-5" style={{ color: s.color }} />
                  </div>
                  <h3 className="font-heading font-semibold text-sm mb-1">{s.name}</h3>
                  <p className="text-xs font-mono" style={{ color: COLORS.dimmed }}>
                    {s.url.replace("https://", "").split("/").slice(0, 2).join("/")}
                  </p>
                </a>
              ))}
            </div>
          </div>
        </section>

        {/* INTERACTIVE */}
        <section className="relative z-10 max-w-7xl mx-auto px-6 py-24">
          <SectionHeader label="Play" title="Interactive" highlight="zone" />
          <div className="grid md:grid-cols-2 gap-6">
            <div className="p-8 rounded-xl card-hover relative overflow-hidden" style={{ background: COLORS.card, border: `1px solid ${COLORS.border}` }}>
              <div className="absolute top-4 right-4 px-2.5 py-1 rounded-full text-xs font-mono" style={{ background: `${COLORS.cyan}15`, color: COLORS.cyan }}>Coming Soon</div>
              <Sparkles className="w-10 h-10 mb-4" style={{ color: COLORS.cyan }} />
              <h3 className="font-heading font-semibold text-xl mb-2">Zo Trivia</h3>
              <p className="text-sm leading-relaxed" style={{ color: COLORS.muted }}>
                Daily trivia questions about Zo Computer features, tips, and hidden gems. Test your knowledge and learn something new.
              </p>
            </div>
            <a href="/icon-configurator" className="block p-8 rounded-xl card-hover relative overflow-hidden group" style={{ background: COLORS.card, border: `1px solid ${COLORS.border}` }}>
              <div className="absolute top-4 right-4 opacity-0 group-hover:opacity-100 transition-opacity">
                <ArrowRight className="w-5 h-5" style={{ color: COLORS.indigoLight }} />
              </div>
              <Gamepad2 className="w-10 h-10 mb-4" style={{ color: COLORS.indigo }} />
              <h3 className="font-heading font-semibold text-xl mb-2 group-hover:text-indigo-400 transition-colors">Zo Icon Configurator</h3>
              <p className="text-sm leading-relaxed" style={{ color: COLORS.muted }}>
                Choose a black or white Zo Computer logo, describe your modifications, and generate a custom version to download.
              </p>
            </a>
          </div>
        </section>

        {/* CONTACT */}
        <section id="contact" className="relative z-10 py-24" style={{ background: COLORS.card }}>
          <div className="max-w-7xl mx-auto px-6">
            <SectionHeader label="Contact" title="Get in" highlight="touch" />
            <div className="max-w-xl mx-auto">
              {sent ? (
                <div className="text-center p-12 rounded-xl" style={{ background: COLORS.bg, border: `1px solid ${COLORS.cyan}40` }}>
                  <CheckCircle className="w-12 h-12 mx-auto mb-4" style={{ color: COLORS.cyan }} />
                  <h3 className="font-heading text-xl font-semibold mb-2">Message sent!</h3>
                  <p className="text-sm mb-6" style={{ color: COLORS.muted }}>Thanks for reaching out. I'll get back to you soon.</p>
                  <button onClick={() => setSent(false)} className="text-sm font-mono tracking-wider uppercase transition-colors" style={{ color: COLORS.cyan }}>
                    Send another
                  </button>
                </div>
              ) : (
                <form onSubmit={handleSubmit} className="space-y-5">
                  {[
                    { name: "name", label: "Name", type: "text", placeholder: "Your name" },
                    { name: "email", label: "Email", type: "email", placeholder: "you@example.com" },
                  ].map(field => (
                    <div key={field.name}>
                      <label className="block text-xs font-mono tracking-wider uppercase mb-2" style={{ color: COLORS.muted }}>{field.label}</label>
                      <input type={field.type} required
                        value={(formState as any)[field.name]}
                        onChange={e => setFormState(s => ({ ...s, [field.name]: e.target.value }))}
                        className="w-full px-4 py-3 rounded-xl font-body transition-all outline-none"
                        style={{ background: COLORS.bg, border: `1px solid ${COLORS.border}`, color: "white" }}
                        onFocus={e => e.target.style.borderColor = `${COLORS.cyan}50`}
                        onBlur={e => e.target.style.borderColor = COLORS.border}
                        placeholder={field.placeholder} />
                    </div>
                  ))}
                  <div>
                    <label className="block text-xs font-mono tracking-wider uppercase mb-2" style={{ color: COLORS.muted }}>Message</label>
                    <textarea required rows={5} maxLength={2000}
                      value={formState.message}
                      onChange={e => setFormState(s => ({ ...s, message: e.target.value }))}
                      className="w-full px-4 py-3 rounded-xl font-body transition-all outline-none resize-none"
                      style={{ background: COLORS.bg, border: `1px solid ${COLORS.border}`, color: "white" }}
                      onFocus={e => (e.target as HTMLTextAreaElement).style.borderColor = `${COLORS.cyan}50`}
                      onBlur={e => (e.target as HTMLTextAreaElement).style.borderColor = COLORS.border}
                      placeholder="What's on your mind?" />
                  </div>
                  {formError && <p className="text-red-400 text-sm font-mono">{formError}</p>}
                  <button type="submit" disabled={sending}
                    className="w-full flex items-center justify-center gap-2 px-6 py-3.5 rounded-full text-white font-semibold text-sm tracking-wider uppercase transition-all duration-300 hover:scale-[1.02] disabled:opacity-50 disabled:cursor-not-allowed"
                    style={{
                      background: `linear-gradient(135deg, ${COLORS.cyan}, ${COLORS.indigo})`,
                      boxShadow: `0 0 25px -5px ${COLORS.cyan}50`,
                    }}>
                    {sending ? "Sending..." : <><span>Send message</span><Send className="w-4 h-4" /></>}
                  </button>
                </form>
              )}
            </div>
          </div>
        </section>

        {/* FOOTER */}
        <footer className="relative z-10 py-8" style={{ borderTop: `1px solid ${COLORS.border}` }}>
          <div className="max-w-7xl mx-auto px-6 flex flex-wrap items-center justify-between gap-4">
            <p className="text-xs font-mono tracking-wider" style={{ color: COLORS.dimmed }}>&copy; 2026 Zenlyte</p>
            <div className="flex items-center gap-4">
              {SOCIAL_LINKS.map(s => (
                <a key={s.name} href={s.url} target="_blank" rel="noopener noreferrer" className="transition-colors hover:opacity-80" style={{ color: COLORS.dimmed }}>
                  <s.icon className="w-4 h-4" />
                </a>
              ))}
            </div>
            <p className="text-xs" style={{ color: COLORS.dimmed }}>
              Built on{" "}
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
          <div className="nf-term-hdr">⬛ ZOS Recovery Terminal</div>
          <div className="nf-term-body">
            <div className="nf-term-line">ZOS ERROR: Requested path does not match any known route.</div>
            <div className="nf-term-line">Type 'help' for recovery options.</div>
            <div className="nf-term-line"> </div>
            {output.map((l, i) => <div key={i} className="nf-term-line">{l}</div>)}
            <div className="nf-term-input">
              <span className="nf-prompt">visitor@zos:~$</span>
              <input value={cmd} onChange={e => setCmd(e.target.value)} onKeyDown={e => { if (e.key === "Enter") exec(); }} className="nf-inp" autoFocus />
              <span className="nf-cursor" style={blink ? undefined : {opacity:0}}>█</span>
            </div>
          </div>
        </div>
        <div className="nf-links">
          <a href="/zos" className="nf-link">⚡ Enter ZOS</a>
          <a href="/press" className="nf-link">📰 Press Kit</a>
          <a href="/about-the-build" className="nf-link">📖 About the Build</a>
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

```

### `/api/agents` (api, public)

```typescript

```

### `/api/audit` (api, public)

```typescript

```

### `/api/auth-status` (api, public)

```typescript
import type { Context } from "hono";

export default (c: Context) => {
  const cookieHeader = c.req.header("cookie") || "";
  const hasZoSession =
    cookieHeader.includes("zo_session") ||
    cookieHeader.includes("auth_token") ||
    cookieHeader.includes("x-zo-session") ||
    cookieHeader.includes("__session");

  const zoUser = c.req.header("x-zo-user") || "";
  const isAuthenticated = hasZoSession || zoUser.length > 0;

  return c.json({ authenticated: isAuthenticated });
};
```

### `/api/benchmarks` (api, public)

```typescript

```

### `/api/benchmarks/refresh` (api, public)

```typescript

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
import type { Context } from "hono";
import { readdirSync, readFileSync, statSync, existsSync } from "node:fs";
import { join } from "node:path";

export interface BlogPost {
  slug: string;
  title: string;
  excerpt: string;
  date: string;
  tags: string[];
  readTime: string;
  content: string;
  coverGradient: string;
  type?: string;
}

// Simple frontmatter parser
function parseMarkdown(filePath: string): { data: any; content: string } {
  const fileContent = readFileSync(filePath, "utf-8");
  const frontmatterRegex = /^---\n([\s\S]*?)\n---\n([\s\S]*)$/;
  const match = fileContent.match(frontmatterRegex);
  
  if (!match) {
    return { data: {}, content: fileContent };
  }
  
  const frontmatterString = match[1];
  const content = match[2];
  
  const data: any = {};
  frontmatterString.split("\n").forEach((line) => {
    const colonIndex = line.indexOf(":");
    if (colonIndex === -1) return;
    const key = line.slice(0, colonIndex).trim();
    let value = line.slice(colonIndex + 1).trim();
    
    // Parse arrays
    if (value.startsWith("[") && value.endsWith("]")) {
      try {
        value = JSON.parse(value.replace(/\'/g, '\"'));
      } catch (e) {
        value = value.slice(1, -1).split(",").map((s) => s.trim().replace(/^["\']|["\']$/g, ""));
      }
    } else {
      // Remove quotes from string
      value = value.replace(/^["\']|["\']$/g, "");
    }
    data[key] = value;
  });
  
  return { data, content: content.trim() };
}

function getPostsFromDir(dirPath: string, type: string): BlogPost[] {
  if (!existsSync(dirPath)) return [];
  
  const posts: BlogPost[] = [];
  const files = readdirSync(dirPath);
  
  for (const file of files) {
    if (!file.endsWith(".md")) continue;
    
    const fullPath = join(dirPath, file);
    if (!statSync(fullPath).isFile()) continue;
    
    const slug = file.replace(/\.md$/, "");
    const { data, content } = parseMarkdown(fullPath);
    
    posts.push({
      slug,
      title: data.title || slug,
      excerpt: data.excerpt || "",
      date: data.date || new Date().toISOString().split("T")[0],
      tags: Array.isArray(data.tags) ? data.tags : [],
      readTime: data.readTime || "5 min read",
      coverGradient: data.coverGradient || "from-[#06b6d4] via-[#6366f1] to-[#818cf8]",
      type,
      content
    });
  }
  
  return posts;
}

export function getAllPosts(): BlogPost[] {
  const baseDir = "/home/workspace/Documents/blog";
  const articlesDir = join(baseDir, "articles");
  const notesDir = join(baseDir, "notes");
  
  const articles = getPostsFromDir(articlesDir, "article");
  const notes = getPostsFromDir(notesDir, "note");
  
  return [...articles, ...notes].sort((a, b) => {
    return new Date(b.date).getTime() - new Date(a.date).getTime();
  });
}

export default async (c: Context) => {
  const allPosts = getAllPosts();
  // The blog list page does not need the full content to save bandwidth
  const postsWithoutContent = allPosts.map(({ content, ...rest }) => rest);
  
  return c.json({ posts: postsWithoutContent });
};
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
- `Documents/blog`

**Secrets required** (configure in [Settings > Advanced](/?t=settings&s=advanced)):
- `ZO_API_KEY`

