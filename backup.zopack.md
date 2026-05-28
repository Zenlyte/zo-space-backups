---
format: zopack
version: "1.0"
name: zo-space-backup
author: unknown.zo.computer
routes: 1
exported: 2026-05-28
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

function DraggableZenny() { return null as any; }
function HexAvatar({ size = 140 }: { size?: number }) { return <div /> as any; }
function SectionHeader({ label, title, highlight }: { label: string; title: string; highlight: string }) { return <div /> as any; }
function StatusBadge({ status }: { status: string }) { return <div /> as any; }

interface PostMeta { slug: string; title: string; excerpt: string; date: string; tags: string[]; readTime: string; }

export default function Home() { return <div /> as any; }
```

