---
format: zopack
version: "1.0"
name: zo-space-backup
author: unknown.zo.computer
routes: 132
exported: 2026-05-16
---

# zo-space-backup

## Routes

### `/temporal` (page, private)

```tsx

```

### `/api/temporal-auth-check` (api, public)

```typescript

```

### `/api/temporal/*` (api, public)

```typescript

```

### `/api/share/:id/download` (api, public)

```typescript

```

### `/api/flowpulse` (api, public)

```typescript

```

### `/zo-space-theme-gallery/:id` (page, public)

```tsx

```

### `/blog` (page, public)

```tsx
import { useState, useEffect, useRef } from "react";
import { ArrowRight, ArrowLeft, Clock, Tag, Search, Filter, X, Menu, Lock } from "lucide-react";

export default function Blog() { /* truncated in export input */ }
```

### `/api/blog/:slug` (api, public)

```typescript

```

### `/Zo-Ops` (page, private)

```tsx

```

### `/api/twinmind-callback` (api, public)

```typescript

```

### `/blog/:slug` (page, public)

```tsx

```

### `/api/career-ops/scan-history` (api, public)

```typescript

```

### `/api/skills-gallery` (api, public)

```typescript

```

### `/skills-gallery` (page, private)

```tsx

```

### `/api/zo-space-theme-gallery/skill` (api, public)

```typescript

```

### `/api/zo-space-theme-gallery` (api, public)

```typescript

```

### `/api/zo-space-theme-gallery/:id` (api, public)

```typescript

```

### `/icon-configurator` (page, public)

```tsx

```

### `/api/logs` (api, public)

```typescript

```

### `/api/security` (api, public)

```typescript

```

### `/api/failures` (api, public)

```typescript

```

### `/api/trivia/dates` (api, public)

```typescript

```

### `/api/calendar` (api, public)

```typescript

```

### `/api/extension-save` (api, public)

```typescript

```

### `/api/generate-icon` (api, public)

```typescript

```

### `/share` (page, private)

```tsx

```

### `/api/test-write` (api, public)

```typescript

```

### `/api/test-exec` (api, public)

```typescript

```

### `/zo-status` (page, public)

```tsx

```

### `/api/benchmarks/refresh` (api, public)

```typescript

```

### `/api/billing` (api, public)

```typescript

```

### `/api/audit` (api, public)

```typescript

```

### `/api/test-env` (api, public)

```typescript

```

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

const ZENNY_STATES = {
  idle: { src: "/pets/zenny-idle-v1.png", frames: 6 },
  left: { src: "/pets/zenny-running-left-v1.png", frames: 8 },
  right: { src: "/pets/zenny-running-right-v1.png", frames: 8 },
} as const;

function DraggableZenny() { /* truncated in export input */ }
function HexAvatar({ size = 140 }: { size?: number }) { /* truncated in export input */ }
function SectionHeader({ label, title, highlight }: { label: string; title: string; highlight: string }) { /* truncated in export input */ }
function StatusBadge({ status }: { status: string }) { /* truncated in export input */ }
export default function Home() { /* truncated in export input */ }
```

### `/receipts` (page, public)

```tsx

```

### `/api/diagnose` (api, public)

```typescript

```

### `/api/receipts` (api, public)

```typescript

```

### `/openclaw-dashboard` (page, private)

```tsx

```

### `/dashboard` (page, private)

```tsx

```

### `/api/twinmind` (api, public)

```typescript

```

### `/api/datasets/start` (api, public)

```typescript

```

### `/docs` (api, public)

```typescript

```

### `/api/sites` (api, public)

```typescript

```

### `/api/my-models` (api, public)

```typescript

```

### `/knowledge-graph` (page, private)

```tsx

```

### `/api/updates` (api, public)

```typescript

```

### `/api/blog` (api, public)

```typescript

```

### `/kg-search` (api, public)

```typescript

```

### `/api/share` (api, public)

```typescript

```

### `/profile` (page, public)

```tsx

```

### `/kg-entity` (api, public)

```typescript

```

### `/api/models` (api, public)

```typescript

```

### `/kg-by-type` (api, public)

```typescript

```

### `/kg-stats` (api, public)

```typescript

```

### `/kg-recall` (api, public)

```typescript

```

### `/kg-browse` (api, public)

```typescript

```

### `/kg-graph` (api, public)

```typescript

```

### `/api/files` (api, public)

```typescript

```

### `/api/services` (api, public)

```typescript

```

### `/api/system-stats` (api, public)

```typescript

```

### `/api/credits` (api, public)

```typescript

```

### `/zo-space-theme-gallery` (page, public)

```tsx

```

### `/zo-control-deck` (page, private)

```tsx

```

### `/job-ops` (page, private)

```tsx

```

### `/telemetry` (page, private)

```tsx

```

### `/api/trivia/leaderboard` (api, public)

```typescript

```

### `/zo-city-three-test` (page, public)

```tsx

```

### `/api/trivia/random` (api, public)

```typescript

```

### `/api/trivia/by-date` (api, public)

```typescript

```

### `/api/agents` (api, public)

```typescript

```

### `/trivia` (page, public)

```tsx

```

### `/repurpose` (page, private)

```tsx

```

### `/api/datasets/proxy/*` (api, public)

```typescript

```

### `/api/benchmarks` (api, public)

```typescript
import type { Context } from "hono";
import { readFileSync, existsSync } from "fs";
import { join } from "path";

export default async (c: Context) => { /* truncated in export input */ };
```

### `/api/career-ops/scan` (api, public)

```typescript

```

### `/data/zo-trivia/` (page, private)

```tsx

```

### `/speech-game` (page, public)

```tsx

```

### `/speech-game/stickers` (page, public)

```tsx

```

### `/api/speech-game-auth` (api, public)

```typescript

```

### `/api/career-ops/batch` (api, public)

```typescript

```

### `/speech-game-manifest.json` (api, public)

```typescript

```

### `/speech-game-sw.js` (api, public)

```typescript

```

### `/data/zo-trivia/api/query` (api, public)

```typescript

```

### `/buildin-auth` (page, private)

```tsx

```

### `/api/buildin/disconnect` (api, public)

```typescript

```

### `/api/projects` (api, public)

```typescript

```

### `/api/test-deps` (api, public)

```typescript

```

### `/api/zos/now` (api, public)

```typescript

```

### `/api/zos/build-log` (api, public)

```typescript

```

### `/speech-game/stats` (page, public)

```tsx

```

### `/api/auth-status` (api, public)

```typescript

```

### `/zo-city` (page, public)

```tsx

```

### `/about-the-build` (page, public)

```tsx

```

### `/404` (page, public)

```tsx

```

### `/api/zos/signals` (api, public)

```typescript

```

### `/api/career-ops` (api, public)

```typescript

```

### `/career-ops` (page, private)

```tsx

```

### `/api/career-ops/pipeline` (api, public)

```typescript

```

### `/api/career-ops/applications` (api, public)

```typescript

```

### `/api/health-check` (api, public)

```typescript
import type { Context } from "hono";
import { readFileSync, existsSync, readdirSync } from "node:fs";
import { execSync } from "node:child_process";

export default async (c: Context) => { /* truncated in export input */ };
```

### `/api/speech-game-data` (api, public)

```typescript

```

### `/api/telemetry-data` (api, public)

```typescript

```

### `/model-advisor` (page, public)

```tsx

```

### `/api/buildin/callback` (api, public)

```typescript

```

### `/api/trivia/unsubscribe` (api, public)

```typescript

```

### `/api/datasets/viewer` (api, public)

```typescript

```

### `/data-explorer` (page, private)

```tsx

```

### `/api/datasets/list` (api, public)

```typescript

```

### `/api/puzzle-callback` (page, public)

```tsx

```

### `/api/nav-links` (api, public)

```typescript

```

### `/s/:id` (page, public)

```tsx

```

### `/api/share/:id` (api, public)

```typescript

```

### `/api/trivia` (api, public)

```typescript

```

### `/trivia/archive` (page, private)

```tsx

```

### `/api/trivia/subscribe` (api, public)

```typescript

```

### `/api/family-log` (api, public)

```typescript

```

### `/trivia/leaderboard` (page, private)

```tsx

```

### `/api/trivia/user-stats` (api, public)

```typescript

```

### `/api/projects-conversations` (api, public)

```typescript

```

### `/api/receipt-images` (api, public)

```typescript

```

### `/api/buildin/status` (api, public)

```typescript

```

### `/secret` (page, public)

```tsx

```

### `/api/contact` (api, public)

```typescript

```

### `/api/x-feed` (api, public)

```typescript

```

### `/press` (page, public)

```tsx

```

### `/zos-lite` (page, public)

```tsx

```

### `/api/zo-city-data` (api, public)

```typescript

```

### `/api/voi-zos` (api, public)

```typescript

```

### `/zos` (page, public)

```tsx

```

### `/zoboard` (page, private)

```tsx

```

### `/api/zoboard/*` (api, public)

```typescript

```

### `/zoboard/:slug` (page, private)

```tsx

```

