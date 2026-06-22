---
format: zopack
version: "1.0"
name: zo-space-backup
author: unknown.zo.computer
routes: 132
exported: 2026-06-22
---

# zo-space-backup

## Routes

### `/` (page, public)

```tsx

```

### `/404` (page, public)

```tsx

```

### `/Zo-Ops` (page, private)

```tsx
import React, { useState, useEffect, useCallback, useRef } from "react";
import { Menu, X, ExternalLink, Lock, LayoutDashboard, Palette, Settings, Share2, Clock, Briefcase, Sparkles, PenLine } from 'lucide-react';

interface Project {
  name: string;
  desc: string;
  status: "backlog" | "in-progress" | "completed" | "archived";
  tags: string[];
  link: string | null;
  priority?: "high" | "medium" | "low" | "none";
  order?: number;
}

// Curtis's ZoSpace design system
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

const COLUMNS: { id: Project["status"]; label: string; color: string }[] = [
  { id: "backlog", label: "Backlog", color: "#f59e0b" },
  { id: "in-progress", label: "In Progress", color: "#06b6d4" },
  { id: "completed", label: "Completed", color: "#22c55e" },
  { id: "archived", label: "Archived", color: "#64748b" },
];

const PRIORITY_COLUMNS: { id: Project["priority"]; label: string; color: string }[] = [
  { id: "high", label: "High", color: "#ef4444" },
  { id: "medium", label: "Medium", color: "#f59e0b" },
  { id: "low", label: "Low", color: "#06b6d4" },
  { id: "none", label: "None", color: "#64748b" },
];

function GlobalNav() {
  const [navOpen, setNavOpen] = useState(false);
  const [navAuth, setNavAuth] = useState(false);
  const [navLinks, setNavLinks] = useState<any[]>([]);
  const navRef = useRef<HTMLDivElement>(null);

  useEffect(() => {
    fetch("/api/nav-links", { headers: { Accept: "application/json" }, credentials: "include" })
      .then(r => r.json())
      .then(d => { 
        setNavLinks(d.links || []); 
        setNavAuth(d.authenticated); 
      })
      .catch(() => {});
      
    const interval = setInterval(() => {
      fetch("/api/auth-status", { headers: { Accept: "application/json" }, credentials: "include" })
        .then(r => r.json())
        .then(d => setNavAuth(d.authenticated))
        .catch(() => {});
    }, 30000);
    
    const handleClick = (e: MouseEvent) => {
      if (navRef.current && !navRef.current.contains(e.target as Node)) {
        setNavOpen(false);
      }
    };
    document.addEventListener("mousedown", handleClick);
    
    return () => {
      clearInterval(interval);
      document.removeEventListener("mousedown", handleClick);
    };
  }, []);

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

  const filteredNavLinks = navLinks.filter(l => l.path !== window.location.pathname);

  const COLORS = {
    cyan: "#06b6d4",
    cyanLight: "#22d3ee",
    indigo: "#6366f1",
    indigoLight: "#818cf8",
    muted: "#94a3b8",
    dimmed: "#64748b",
    border: "rgba(255,255,255,0.08)"
  };

  return (
    <>
      <div className="hidden md:block fixed top-6 right-6 z-[9999]" ref={navRef}>
        <div className="relative">
          <button 
            onClick={() => setNavOpen(!navOpen)}
            className="flex items-center gap-2 px-3 py-2 rounded-lg bg-zinc-900/50 hover:bg-zinc-800/80 backdrop-blur-md transition-colors border"
            style={{ borderColor: COLORS.border }}
          >
            {navOpen ? <X className="w-5 h-5" style={{ color: COLORS.cyan }} /> : <Menu className="w-5 h-5" style={{ color: COLORS.cyan }} />}
          </button>
          
          {navOpen && (
            <div className="absolute top-full right-0 mt-3 min-w-[250px] w-max max-w-md rounded-xl overflow-hidden shadow-2xl"
              style={{ background: "rgba(15,17,23,0.95)", backdropFilter: "blur(20px)", border: `1px solid ${COLORS.border}` }}>
              {navAuth && (
                <div className="px-4 py-2.5 flex items-center gap-2 text-xs font-mono" style={{ borderBottom: `1px solid ${COLORS.border}`, color: COLORS.cyan }}>
                  <Lock className="w-3 h-3" />
                  <span>Authenticated view</span>
                </div>
              )}
              <div className="py-2 max-h-[70vh] overflow-y-auto">
                {filteredNavLinks.map((link: any) => {
                  const IconComp = ICON_MAP[link.icon] || ExternalLink;
                  return (
                    <a key={link.path} href={link.path}
                      onClick={() => setNavOpen(false)}
                      className="flex items-start gap-3 px-4 py-3 transition-colors hover:bg-white/5 group">
                      <div className="w-8 h-8 rounded-lg flex items-center justify-center shrink-0 mt-0.5"
                        style={{
                          background: link.category === "private" ? `${COLORS.indigo}15` : `${COLORS.cyan}15`,
                          border: `1px solid ${link.category === "private" ? `${COLORS.indigo}30` : `${COLORS.cyan}30`}`,
                        }}>
                        <IconComp className="w-4 h-4" style={{ color: link.category === "private" ? COLORS.indigoLight : COLORS.cyan }} />
                      </div>
                      <div className="min-w-0">
                        <div className="flex items-center gap-2">
                          <span className="text-sm font-medium text-white group-hover:text-cyan-400 transition-colors">{link.name}</span>
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
      </div>

      <div className="md:hidden fixed bottom-6 right-6 z-[9999]">
        {navOpen && (
          <div
            className="absolute bottom-16 right-0 mb-2 min-w-[200px] w-max max-w-[calc(100vw-2rem)] rounded-xl shadow-2xl overflow-hidden"
            style={{ background: "rgba(15,17,23,0.98)", backdropFilter: "blur(20px)", border: `1px solid ${COLORS.border}` }}
          >
            {navAuth && (
              <div className="px-4 py-2.5 flex items-center gap-2 text-xs font-mono" style={{ borderBottom: `1px solid ${COLORS.border}`, color: COLORS.cyan }}>
                <Lock className="w-3 h-3" />
                <span>Authenticated</span>
              </div>
            )}
            <div className="py-2 max-h-[60vh] overflow-y-auto">
              <div className="px-4 py-2 text-xs font-mono tracking-widest uppercase" style={{ color: COLORS.dimmed }}>
                Pages
              </div>
              {filteredNavLinks.map((link: any) => {
                const IconComp = ICON_MAP[link.icon] || ExternalLink;
                return (
                  <a key={link.path} href={link.path}
                    onClick={() => setNavOpen(false)}
                    className="flex items-center gap-3 px-4 py-3 text-sm text-white hover:bg-white/5 transition-colors">
                    <div className="w-6 flex justify-center shrink-0">
                      <IconComp className="w-4 h-4" style={{ color: link.category === "private" ? COLORS.indigoLight : COLORS.cyan }} />
                    </div>
                    <span className="truncate">{link.name}</span>
                    {link.category === "private" && (
                      <span className="ml-auto shrink-0 px-1.5 py-0.5 rounded text-[10px] font-mono"
                        style={{ background: `${COLORS.indigo}20`, color: COLORS.indigoLight }}>
                        Private
                      </span>
                    )}
                  </a>
                );
              })}
            </div>
          </div>
        )}
        
        <button
          onClick={() => setNavOpen(!navOpen)}
          className="w-14 h-14 rounded-full flex items-center justify-center shadow-lg transition-transform hover:scale-105 active:scale-95"
          style={{ background: COLORS.cyan, color: "white", boxShadow: `0 4px 20px -5px ${COLORS.cyan}60` }}
        >
          {navOpen ? <X className="w-6 h-6" /> : <Menu className="w-6 h-6" />}
        </button>
      </div>
    </>
  );
}

export default function ZoOps() {
  const [projects, setProjects] = useState<Project[]>([]);
  const [loading, setLoading] = useState(true);
  const [dragOver, setDragOver] = useState<Project["status"] | null>(null);
  const [dragging, setDragging] = useState<string | null>(null);
  const [collapsed, setCollapsed] = useState<Record<string, boolean>>({});
  const [selectedProject, setSelectedProject] = useState<Project | null>(null);
  const [view, setView] = useState<"status" | "priority">("status");
  const [insertBefore, setInsertBefore] = useState<{ name: string; status: string } | null>(null);

  const fetchProjects = useCallback(async () => {
    try {
      const res = await fetch("/api/projects");
      if (res.ok) {
        const data = await res.json();
        setProjects(data);
      }
    } catch (err) {
      console.error("Failed to load projects:", err);
    } finally {
      setLoading(false);
    }
  }, []);

  useEffect(() => {
    fetchProjects();
  }, [fetchProjects]);

  const moveProject = async (name: string, newStatus: Project["status"]) => {
    const optimistic = projects.map((p) =>
      p.name === name ? { ...p, status: newStatus } : p
    );
    setProjects(optimistic);

    try {
      const res = await fetch(`/api/projects?name=${encodeURIComponent(name)}&status=${newStatus}`, {
        method: "PATCH",
      });
      if (!res.ok) {
        setProjects(projects);
      }
    } catch {
      setProjects(projects);
    }
  };

  const reorderProject = async (name: string, newOrder: number, newStatus?: Project["status"], newPriority?: Project["priority"]) => {
    const groupKey = view === "status" ? "status" : "priority";
    const updated = projects.map((p) => {
      if (p.name === name) {
        return {
          ...p,
          order: newOrder,
          ...(newStatus ? { status: newStatus } : {}),
          ...(newPriority ? { priority: newPriority } : {}),
        };
      }
      return p;
    });
    setProjects(updated);
    try {
      const params = new URLSearchParams({ name, newOrder: String(newOrder) });
      if (newStatus) params.set("newStatus", newStatus);
      if (newPriority) params.set("newPriority", newPriority);
      const res = await fetch(`/api/projects?${params}`, { method: "PATCH" });
      if (!res.ok) setProjects(projects);
    } catch {
      setProjects(projects);
    }
  };

  const saveProject = async (updated: Project) => {
    try {
      const res = await fetch("/api/projects", {
        method: "PUT",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(updated),
      });
      if (res.ok) {
        const result = await res.json();
        setProjects((prev) => prev.map((p) => (p.name === updated.name ? result.project : p)));
        setSelectedProject(null);
      }
    } catch (err) {
      console.error("Failed to save project:", err);
    }
  };

  const onDragStart = (e: React.DragEvent, name: string) => {
    setDragging(name);
    e.dataTransfer.effectAllowed = "move";
    e.dataTransfer.setData("text/plain", name);
  };

  const onDragOver = (e: React.DragEvent, colId: string) => {
    e.preventDefault();
    e.dataTransfer.dropEffect = "move";
    setDragOver(colId as any);

    // Calculate insert position based on mouse Y
    const cardEls = (e.currentTarget as HTMLElement).querySelectorAll("[data-drag-card]");
    let insertBeforeName: string | null = null;
    cardEls.forEach((el) => {
      const rect = el.getBoundingClientRect();
      const midY = rect.top + rect.height / 2;
      if (e.clientY < midY) {
        if (!insertBeforeName) insertBeforeName = el.getAttribute("data-drag-card");
      }
    });
    setInsertBefore(insertBeforeName ? { name: insertBeforeName, status: colId } : null);
  };

  const onDragLeave = () => setDragOver(null);

  const onDrop = async (e: React.DragEvent, colId: string) => {
    e.preventDefault();
    setDragOver(null);
    const name = e.dataTransfer.getData("text/plain") || dragging;
    if (!name) { setDragging(null); setInsertBefore(null); return; }
    const dragged = projects.find((p) => p.name === name);
    if (!dragged) { setDragging(null); setInsertBefore(null); return; }

    const groupKey = view === "status" ? "status" : "priority";
    const itemsInCol = projects
      .filter((p) => (p as any)[groupKey] === colId)
      .sort((a, b) => (a.order ?? 0) - (b.order ?? 0));

    let newOrder: number;
    if (insertBefore && insertBefore.status === colId) {
      newOrder = itemsInCol.findIndex((p) => p.name === insertBefore.name);
      if (newOrder < 0) newOrder = itemsInCol.length;
    } else {
      newOrder = itemsInCol.length;
    }

    if (view === "status") {
      const newStatus = colId !== dragged.status ? colId as Project["status"] : undefined;
      await reorderProject(name, newOrder, newStatus);
    } else {
      const newPriority = colId !== dragged.priority ? colId as Project["priority"] : undefined;
      await reorderProject(name, newOrder, undefined, newPriority);
    }

    setDragging(null);
    setInsertBefore(null);
  };

  const handleDragEnd = () => {
    setDragging(null);
    setDragOver(null);
  };

  const byStatus = COLUMNS.map((col) => ({
    ...col,
    items: projects
      .filter((p) => p.status === col.id)
      .sort((a, b) => (a.order ?? 0) - (b.order ?? 0)),
  }));

  const byPriority = PRIORITY_COLUMNS.map((col) => ({
    ...col,
    items: projects
      .filter((p) => (p.priority ?? "medium") === col.id)
      .sort((a, b) => (a.order ?? 0) - (b.order ?? 0)),
  }));

  return (
    <>
      <style>{`
        @import url('https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@400;500;600;700&family=Inter:wght@400;500;600&family=JetBrains+Mono:wght@400;500&display=swap');
        * { box-sizing: border-box; }
        .font-heading { font-family: 'Space Grotesk', sans-serif; }
        .font-body { font-family: 'Inter', sans-serif; }
        .font-mono { font-family: 'JetBrains Mono', monospace; }
        .glass { background: rgba(15,17,23,0.8); backdrop-filter: blur(12px); border: 1px solid rgba(255,255,255,0.08); }
        .hide-scrollbar::-webkit-scrollbar { display: none; }
        .hide-scrollbar { -ms-overflow-style: none; scrollbar-width: none; }
        .vertical-text { writing-mode: vertical-rl; text-orientation: mixed; transform: rotate(180deg); }
      `}</style>

      <div className="min-h-screen text-white" style={{ background: COLORS.bg, fontFamily: "'Inter', sans-serif" }}>
        {/* Glass Header */}
        <header className="sticky top-0 z-50 glass max-w-7xl mx-auto" style={{ fontFamily: "'Space Grotesk', sans-serif" }}>
          <div className="w-full px-4 py-3 md:py-4 flex flex-col md:flex-row md:items-center justify-between gap-3">
            <div className="flex items-center gap-3">
              <div
                className="w-8 h-8 rounded-lg flex items-center justify-center"
                style={{ background: `linear-gradient(135deg, ${COLORS.cyan}, ${COLORS.indigo})` }}
              >
                <span className="text-white text-lg">📋</span>
              </div>
              <span className="font-heading font-semibold">Project Ops</span>
            </div>

            <div className="flex items-center gap-4">
              <span className="font-mono text-xs" style={{ color: COLORS.muted }}>
                {projects.length} projects
              </span>
              <button
                onClick={fetchProjects}
                className="font-mono text-xs px-3 py-1.5 rounded transition-all"
                style={{
                  background: `${COLORS.cyan}15`,
                  color: COLORS.cyan,
                  border: `1px solid ${COLORS.cyan}30`,
                }}
              >
                Refresh
              </button>
              <div className="flex items-center rounded-lg overflow-hidden" style={{ border: `1px solid ${COLORS.border}` }}>
                <button
                  onClick={() => setView("status")}
                  className="font-mono text-xs px-3 py-1.5 transition-all"
                  style={{
                    background: view === "status" ? COLORS.cyan : "transparent",
                    color: view === "status" ? "#000" : COLORS.dimmed,
                  }}
                >
                  Status
                </button>
                <button
                  onClick={() => setView("priority")}
                  className="font-mono text-xs px-3 py-1.5 transition-all"
                  style={{
                    background: view === "priority" ? COLORS.cyan : "transparent",
                    color: view === "priority" ? "#000" : COLORS.dimmed,
                  }}
                >
                  Priority
                </button>
              </div>
            </div>
          </div>
        </header>

        {/* Main Content */}
        <main className="w-full px-4 py-6">
          {loading ? (
            <div className="flex items-center justify-center h-64">
              <div className="text-center">
                <div
                  className="w-8 h-8 border-2 border-t-cyan-400 border-gray-700 rounded-full animate-spin mx-auto mb-4"
                />
                <p className="font-mono text-sm" style={{ color: COLORS.muted }}>
                  Loading projects...
                </p>
              </div>
            </div>
          ) : (
            <div className="flex justify-center">
              <div className="flex gap-3 overflow-x-auto pb-4">
                {(view === "status" ? byStatus : byPriority).map((col) => {
                  const isOver = dragOver === col.id;
                  const isCollapsed = collapsed[col.id];
                  return (
                    <div key={col.id} className="shrink-0" style={{ width: isCollapsed ? "52px" : "320px", transition: "width 0.25s ease" }}>
                      {isCollapsed ? (
                        /* Collapsed Column — thin vertical bar */
                        <div className="h-full rounded-xl flex flex-col items-center py-3 gap-2" style={{ background: COLORS.card, border: `1px solid ${COLORS.border}` }}>
                          <button onClick={() => setCollapsed(c => ({ ...c, [col.id]: false }))} className="p-1.5 rounded-lg transition-colors hover:bg-white/10" style={{ color: col.color }} title={`Expand ${col.label}`}>
                            <svg xmlns="http://www.w3.org/2000/svg" className="w-4 h-4" viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="2" strokeLinecap="round" strokeLinejoin="round"><polyline points="9 18 15 12 9 6" /></svg>
                          </button>
                          <div className="flex-1 flex items-start pt-4">
                            <div className="vertical-text font-heading font-semibold text-sm tracking-wide" style={{ color: col.color }}>{col.label}</div>
                          </div>
                          <div className="w-6 h-6 rounded-full flex items-center justify-center font-mono text-[10px] font-semibold" style={{ background: `${col.color}25`, color: col.color }}>
                            {col.items.length}
                          </div>
                        </div>
                      ) : (
                        /* Expanded Column */
                        <div className="rounded-xl transition-all" style={{ background: isOver ? `${col.color}10` : COLORS.card, border: `1px solid ${isOver ? col.color : COLORS.border}` }}
                          onDragOver={(e) => onDragOver(e, col.id)} onDragLeave={onDragLeave} onDrop={(e) => onDrop(e, col.id)}>
                          {/* Column Header */}
                          <div className="px-3 py-2.5 flex items-center justify-between" style={{ borderBottom: `1px solid ${COLORS.border}` }}>
                            <div className="flex items-center gap-2">
                              <div className="w-2 h-2 rounded-full" style={{ background: col.color }} />
                              <h2 className="font-heading font-semibold text-sm" style={{ color: COLORS.muted }}>{col.label}</h2>
                            </div>
                            <div className="flex items-center gap-1.5">
                              <span className="font-mono text-[10px] px-1.5 py-0.5 rounded-full" style={{ background: `${col.color}20`, color: col.color }}>{col.items.length}</span>
                              <button onClick={() => setCollapsed(c => ({ ...c, [col.id]: true }))} className="p-1 rounded transition-colors hover:bg-white/10" style={{ color: COLORS.dimmed }} title={`Collapse ${col.label}`}>
                                <svg xmlns="http://www.w3.org/2000/svg" className="w-3.5 h-3.5" viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="2" strokeLinecap="round" strokeLinejoin="round"><polyline points="15 18 9 12 15 6" /></svg>
                              </button>
                            </div>
                          </div>

                          {/* Cards */}
                          <div className="p-3 space-y-2 min-h-32 max-h-[calc(100vh-12rem)] overflow-y-auto">
                            {col.items.length === 0 && !isOver && (
                              <p
                                className="font-mono text-xs text-center py-8"
                                style={{ color: COLORS.dimmed }}
                              >
                                Drop projects here
                              </p>
                            )}
                            {col.items.map((project) => (
                              <>
                              {insertBefore && insertBefore.name === project.name && insertBefore.status === col.id && (
                                <div className="h-0.5 rounded-full mb-2" style={{ background: COLORS.cyan, boxShadow: `0 0 8px ${COLORS.cyan}` }} />
                              )}
                              <div
                                key={project.name}
                                data-drag-card={project.name}
                                draggable
                                onDragStart={(e) => onDragStart(e, project.name)}
                                onDragEnd={handleDragEnd}
                                onClick={() => setSelectedProject(project)}
                                className="rounded-lg p-3 cursor-grab active:cursor-grabbing transition-all"
                                style={{
                                  background: dragging === project.name ? "#000" : "#0a0a0f",
                                  border: `1px solid ${dragging === project.name ? "transparent" : COLORS.border}`,
                                  opacity: dragging === project.name ? 0.4 : 1,
                                }}
                              >
                                <div className="flex items-start justify-between gap-2">
                                  <div className="flex-1 min-w-0">
                                    <h3
                                      className="font-heading font-medium text-sm truncate"
                                      style={{ color: COLORS.cyanLight }}
                                    >
                                      {project.name}
                                      {view === "priority" && (() => {
                                        const pc = PRIORITY_COLUMNS.find(c => c.id === project.priority);
                                        return pc ? <span className="inline-block w-2 h-2 rounded-full ml-2 align-middle" style={{ background: pc.color }} title={`Priority: ${pc.label}`} /> : null;
                                      })()}
                                    </h3>
                                    <p
                                      className="font-body text-xs mt-1 line-clamp-2"
                                      style={{ color: COLORS.dimmed }}
                                    >
                                      {project.desc}
                                    </p>
                                  </div>
                                  {project.link && (
                                    <a
                                      href={project.link}
                                      className="shrink-0 transition-colors"
                                      style={{ color: COLORS.dimmed }}
                                      onClick={(e) => e.stopPropagation()}
                                      onMouseEnter={(e) => (e.currentTarget.style.color = COLORS.cyan)}
                                      onMouseLeave={(e) => (e.currentTarget.style.color = COLORS.dimmed)}
                                    >
                                      <svg
                                        xmlns="http://www.w3.org/2000/svg"
                                        className="w-3.5 h-3.5"
                                        viewBox="0 0 24 24"
                                        fill="none"
                                        stroke="currentColor"
                                        strokeWidth="2"
                                        strokeLinecap="round"
                                        strokeLinejoin="round"
                                      >
                                        <path d="M18 13v6a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V8a2 2 0 0 1 2-2h6" />
                                        <polyline points="15 3 21 3 21 9" />
                                        <line x1="10" y1="14" x2="21" y2="3" />
                                      </svg>
                                    </a>
                                  )}
                                </div>
                                {project.tags.length > 0 && (
                                  <div className="flex flex-wrap gap-1 mt-2">
                                    {project.tags.slice(0, 3).map((tag) => (
                                      <span
                                        key={tag}
                                        className="font-mono text-[10px] px-1.5 py-0.5 rounded"
                                        style={{
                                          background: `${COLORS.indigo}20`,
                                          color: COLORS.indigoLight,
                                        }}
                                      >
                                        {tag}
                                      </span>
                                    ))}
                                  </div>
                                )}
                              </div>
                              </>
                            ))}
                          </div>
                        </div>
                      )}
                    </div>
                  );
                })}
              </div>
            </div>
          )}
        </main>
      </div>
      <GlobalNav />
      {selectedProject && (
        <ProjectModal
          project={selectedProject}
          onClose={() => setSelectedProject(null)}
          onSave={saveProject}
          columns={COLUMNS}
          priorityColumns={PRIORITY_COLUMNS}
          colors={COLORS}
        />
      )}
    </>
  );
}

function ProjectModal({ project, onClose, onSave, columns, priorityColumns, colors }: {
  project: Project;
  onClose: () => void;
  onSave: (p: Project) => void;
  columns: { id: Project["status"]; label: string; color: string }[];
  priorityColumns: { id: Project["priority"]; label: string; color: string }[];
  colors: Record<string, string>;
}) {
  const [form, setForm] = useState({ ...project, tags: project.tags.join(", "), priority: project.priority || "medium" });
  const [saving, setSaving] = useState(false);
  const [conversations, setConversations] = useState<any[]>([]);
  const [loadingConvs, setLoadingConvs] = useState(false);
  const [activeTab, setActiveTab] = useState<"details" | "conversations">("details");

  useEffect(() => {
    if (activeTab === "conversations" && conversations.length === 0) {
      fetchConversations();
    }
  }, [activeTab]);

  const fetchConversations = async () => {
    setLoadingConvs(true);
    try {
      // Use project name and tags as search query
      const query = `${project.name} ${project.tags.join(" ")}`;
      const res = await fetch(`/api/projects-conversations?q=${encodeURIComponent(query)}`);
      if (res.ok) {
        const data = await res.json();
        setConversations(data.conversations || []);
      }
    } catch (err) {
      console.error("Failed to fetch conversations:", err);
    } finally {
      setLoadingConvs(false);
    }
  };

  const handleSubmit = async (e: React.FormEvent) => {
    e.preventDefault();
    setSaving(true);
    const updated: Project = {
      ...form,
      tags: form.tags.split(",").map((t) => t.trim()).filter(Boolean),
    };
    await onSave(updated);
    setSaving(false);
  };

  return (
    <div className="fixed inset-0 z-[9999] flex items-center justify-center p-4" style={{ background: "rgba(0,0,0,0.7)", backdropFilter: "blur(8px)" }} onClick={onClose}>
      <div className="w-full max-w-xl rounded-2xl overflow-hidden flex flex-col max-h-[90vh]" style={{ background: "#0f1117", border: "1px solid rgba(255,255,255,0.12)" }} onClick={(e) => e.stopPropagation()}>
        {/* Modal Header */}
        <div className="flex items-center justify-between p-6 border-b" style={{ borderColor: "rgba(255,255,255,0.08)" }}>
          <h2 className="font-heading font-semibold text-lg" style={{ color: colors.cyanLight }}>{project.name}</h2>
          <button onClick={onClose} className="p-1 rounded hover:bg-white/10 transition-colors" style={{ color: colors.dimmed }}>
            <svg xmlns="http://www.w3.org/2000/svg" className="w-5 h-5" viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="2"><line x1="18" y1="6" x2="6" y2="18"/><line x1="6" y1="6" x2="18" y2="18"/></svg>
          </button>
        </div>

        {/* Tabs */}
        <div className="flex px-6 border-b" style={{ borderColor: "rgba(255,255,255,0.08)" }}>
          <button 
            onClick={() => setActiveTab("details")}
            className={`px-4 py-3 text-xs font-mono font-bold uppercase tracking-widest transition-all border-b-2 ${activeTab === "details" ? "border-blue-500 text-blue-400" : "border-transparent text-slate-500 hover:text-slate-300"}`}
          >
            Details
          </button>
          <button 
            onClick={() => setActiveTab("conversations")}
            className={`px-4 py-3 text-xs font-mono font-bold uppercase tracking-widest transition-all border-b-2 ${activeTab === "conversations" ? "border-blue-500 text-blue-400" : "border-transparent text-slate-500 hover:text-slate-300"}`}
          >
            Conversations ({conversations.length || "..."})
          </button>
        </div>

        <div className="flex-1 overflow-y-auto p-6">
          {activeTab === "details" ? (
            <form onSubmit={handleSubmit} className="space-y-4">
              <div>
                <label className="block font-mono text-xs mb-1.5" style={{ color: colors.muted }}>NAME</label>
                <input
                  type="text"
                  value={form.name}
                  onChange={(e) => setForm({ ...form, name: e.target.value })}
                  className="w-full rounded-lg px-3 py-2 text-sm text-white outline-none"
                  style={{ background: "#0a0a0f", border: `1px solid ${colors.border}` }}
                  required
                />
              </div>
              <div>
                <label className="block font-mono text-xs mb-1.5" style={{ color: colors.muted }}>DESCRIPTION</label>
                <textarea
                  value={form.desc}
                  onChange={(e) => setForm({ ...form, desc: e.target.value })}
                  className="w-full rounded-lg px-3 py-2 text-sm text-white outline-none resize-none"
                  style={{ background: "#0a0a0f", border: `1px solid ${colors.border}` }}
                  rows={3}
                />
              </div>
              <div>
                <label className="block font-mono text-xs mb-1.5" style={{ color: colors.muted }}>TAGS (comma-separated)</label>
                <input
                  type="text"
                  value={form.tags}
                  onChange={(e) => setForm({ ...form, tags: e.target.value })}
                  className="w-full rounded-lg px-3 py-2 text-sm text-white outline-none"
                  style={{ background: "#0a0a0f", border: `1px solid ${colors.border}` }}
                  placeholder="React, TypeScript, AI"
                />
              </div>
              <div className="grid grid-cols-2 gap-6">
                <div>
                  <label className="block font-mono text-xs mb-1.5" style={{ color: colors.muted }}>STATUS</label>
                  <div className="grid grid-cols-1 gap-2">
                    {columns.map((col) => (
                      <button
                        key={col.id}
                        type="button"
                        onClick={() => setForm({ ...form, status: col.id })}
                        className="flex items-center gap-2 px-3 py-2 rounded-lg text-xs font-medium transition-all"
                        style={{
                          background: form.status === col.id ? `${col.color}25` : "#0a0a0f",
                          border: `1px solid ${form.status === col.id ? col.color : colors.border}`,
                          color: form.status === col.id ? col.color : colors.muted,
                        }}
                      >
                        <div className="w-2 h-2 rounded-full" style={{ background: col.color }} />
                        {col.label}
                      </button>
                    ))}
                  </div>
                </div>
                <div>
                  <label className="block font-mono text-xs mb-1.5" style={{ color: colors.muted }}>PRIORITY</label>
                  <div className="grid grid-cols-1 gap-2">
                    {priorityColumns.map((col) => (
                      <button
                        key={col.id}
                        type="button"
                        onClick={() => setForm({ ...form, priority: col.id })}
                        className="flex items-center gap-2 px-3 py-2 rounded-lg text-xs font-medium transition-all"
                        style={{
                          background: form.priority === col.id ? `${col.color}25` : "#0a0a0f",
                          border: `1px solid ${form.priority === col.id ? col.color : colors.border}`,
                          color: form.priority === col.id ? col.color : colors.muted,
                        }}
                      >
                        <div className="w-2 h-2 rounded-full" style={{ background: col.color }} />
                        {col.label}
                      </button>
                    ))}
                  </div>
                </div>
              </div>
              <div className="flex gap-3 pt-4 border-t" style={{ borderColor: "rgba(255,255,255,0.08)" }}>
                <button
                  type="button"
                  onClick={onClose}
                  className="flex-1 px-4 py-2 rounded-lg text-sm font-medium transition-colors"
                  style={{ background: "rgba(255,255,255,0.06)", color: colors.muted }}
                >
                  Cancel
                </button>
                <button
                  type="submit"
                  disabled={saving}
                  className="flex-1 px-4 py-2 rounded-lg text-sm font-medium transition-all disabled:opacity-50"
                  style={{ background: colors.cyan, color: "#000" }}
                >
                  {saving ? "Saving..." : "Save Changes"}
                </button>
              </div>
            </form>
          ) : (
            /* Conversations Tab */
            <div className="space-y-4">
              {loadingConvs ? (
                <div className="flex items-center justify-center py-12">
                  <div className="w-6 h-6 border-2 border-t-cyan-400 border-white/10 rounded-full animate-spin" />
                </div>
              ) : conversations.length === 0 ? (
                <div className="text-center py-12 text-sm text-slate-500 font-mono italic">
                  No matching conversations found.
                </div>
              ) : (
                <div className="space-y-3">
                  {conversations.map((conv: any) => (
                    <div key={conv.conversation_id} className="p-4 rounded-xl border border-white/5 bg-white/[0.02] hover:bg-white/[0.04] transition-colors group relative">
                      <div className="flex items-start justify-between gap-3 mb-2">
                        <h4 className="text-sm font-medium text-slate-200 line-clamp-2 leading-relaxed">
                          {conv.title}
                        </h4>
                        <span className="text-[10px] font-mono text-slate-500 shrink-0 mt-0.5">
                          {new Date(conv.updated_at).toLocaleDateString("en-CA", { month: "short", day: "numeric" })}
                        </span>
                      </div>
                      <div className="flex items-center gap-2">
                        <span className="text-[10px] font-mono uppercase tracking-widest text-blue-500/60 group-hover:text-blue-400 transition-colors">
                          {conv.conversation_id.split("_")[1].slice(0, 8)}
                        </span>
                      </div>
                    </div>
                  ))}
                </div>
              )}
              <div className="pt-4 border-t text-center" style={{ borderColor: "rgba(255,255,255,0.08)" }}>
                <p className="text-[10px] font-mono text-slate-500 uppercase tracking-widest">
                  Showing top {conversations.length} related threads
                </p>
              </div>
            </div>
          )}
        </div>
      </div>
    </div>
  );
}
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

```

### `/api/billing` (api, public)

```typescript

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
        value = JSON.parse(value.replace(/'/g, '"'));
      } catch (e) {
        value = value.slice(1, -1).split(",").map((s) => s.trim().replace(/^["']|["']$/g, ""));
      }
    } else {
      // Remove quotes from string
      value = value.replace(/^["']|["']$/g, "");
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
import type { Context } from "hono";

export default async (c: Context) => {
  const tokenFile = "/home/workspace/Data/buildin/token.json";
  const { unlinkSync, existsSync } = await import("fs");
  
  if (existsSync(tokenFile)) {
    try {
      unlinkSync(tokenFile);
    } catch {}
  }
  
  return c.json({ success: true });
}
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
- `Documents/blog`
- `Data/buildin`

**Files to initialize:**
- `Data/buildin/token.json` with content: `[]`

