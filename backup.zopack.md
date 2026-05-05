---
format: zopack
version: "1.0"
name: zo-space-backup
author: unknown.zo.computer
routes: 1
exported: 2026-05-05
---

# zo-space-backup

## Routes

### `/temporal` (page, private)

```tsx
import { useEffect, useState, useRef } from "react";

const COLORS = {
  bg: "#0a0a0f",
  card: "#0f1117",
  cyan: "#06b6d4",
  cyanLight: "#22d3ee",
  indigo: "#6366f1",
  indigoLight: "#818cf8",
  muted: "#94a3b8",
  dimmed: "#64748b",
  border: "rgba(255,255,255,0.08)",
};

function GlobalNav() {
  const [open, setOpen] = useState(false);
  const [links, setLinks] = useState<any[]>([]);
  const [auth, setAuth] = useState(false);
  const ref = useRef<HTMLDivElement>(null);

  useEffect(() => {
    fetch("/api/nav-links", { headers: { Accept: "application/json" } })
      .then(r => r.json())
      .then(d => { setLinks(d.links || []); setAuth(d.authenticated); })
      .catch(() => {});
      
    const onClickOutside = (e: MouseEvent) => {
      if (ref.current && !ref.current.contains(e.target as Node)) setOpen(false);
    };
    document.addEventListener("mousedown", onClickOutside);
    return () => document.removeEventListener("mousedown", onClickOutside);
  }, []);

  return (<>...</>);
}

export default function TemporalDashboard() { /* trimmed for export payload */ return <div />; }
```

