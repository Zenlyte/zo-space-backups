---
format: zopack
version: "1.0"
name: zo-space-backup
author: unknown.zo.computer
routes: 126
exported: 2026-04-17
---

# zo-space-backup

## Routes

### `/temporal` (page, private)

```tsx
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta name="description" data-zo-default-seo="true" content="Space to showcase my Zo Computer projects. " />
    <meta name="author" content="Zo" />
```

### `/api/temporal-auth-check` (api, public)

```typescript
{"authenticated":false,"error":"Unauthorized"}
```

### `/api/temporal/*` (api, public)

```typescript
{"error":"Unauthorized"}
```

### `/api/share/:id/download` (api, public)

```typescript
{"error":"Method not allowed"}
```

### `/api/flowpulse` (api, public)

```typescript
{"agents_tracked":34,"agents_enabled":34,"healthy_agents":0,"at_risk_agents":3,"no_data_agents":31,"total_runs":39,"runs_7d":2,"alerts_24h":0,"critical_alerts_24h":0,"last_check":"2026-04-12T08:09:31.438Z"}
```

### `/zo-space-theme-gallery/:id` (page, public)

```tsx
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta name="description" data-zo-default-seo="true" content="Space to showcase my Zo Computer projects. " />
    <meta name="author" content="Zo" />
```

### `/blog` (page, public)

```tsx
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta name="description" data-zo-default-seo="true" content="Space to showcase my Zo Computer projects. " />
    <meta name="author" content="Zo" />
```

### `/api/blog/:slug` (api, public)

```typescript
{"error":"Post not found"}
```

### `/Zo-Ops` (page, private)

```tsx
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta name="description" data-zo-default-seo="true" content="Space to showcase my Zo Computer projects. " />
    <meta name="author" content="Zo" />
```

### `/api/twinmind-callback` (api, public)

```typescript
<html><body><h1>Error</h1><p>No authorization code received</p></body></html>
```

### `/blog/:slug` (page, public)

```tsx
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta name="description" data-zo-default-seo="true" content="Space to showcase my Zo Computer projects. " />
    <meta name="author" content="Zo" />
```

### `/api/career-ops/scan-history` (api, public)

```typescript
{"entries":[{"url":"https://www.shopify.com/careers/search","company":"Shopify","title":"Shopify careers","source":"tracked_company","added_at":"2026-04-13T09:35:35.847Z","status":"added"},{"url":"https://www.d2l.com/careers/jobs/?job_id=7696196&gh_jid=7696196","title":"Bilingual Product Support Ana
```

### `/api/skills-gallery` (api, public)

```typescript
{"error":"Unauthorized"}
```

### `/skills-gallery` (page, private)

```tsx
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta name="description" data-zo-default-seo="true" content="Space to showcase my Zo Computer projects. " />
    <meta name="author" content="Zo" />
```

### `/api/zo-space-theme-gallery/skill` (api, public)

```typescript
---
name: zo-space-themer
description: "Apply pre-designed themes from the Zo Space Theme Gallery to your pages. Supports direct theme selection by name, or describe what you want and Zo will find the best match. Use when the user says 'apply a theme', 'change the look of my page', 'make my site loo
```

### `/api/zo-space-theme-gallery` (api, public)

```typescript
[{"id":"academia","name":"Academia","mode":"light","accent":"#7C2D12","fontType":"serif","description":"Classical scholarly aesthetic with gravitas. Deep browns, parchment tones, ornate serif typography, and structured layouts evoking university libraries and academic journals.","tags":["classical",
```

### `/api/zo-space-theme-gallery/:id` (api, public)

```typescript
{"error":"Theme not found"}
```

### `/icon-configurator` (page, public)

```tsx
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta name="description" data-zo-default-seo="true" content="Space to showcase my Zo Computer projects. " />
    <meta name="author" content="Zo" />
```

### `/api/logs` (api, public)

```typescript
{"lines":[{"time":"2026-04-18T02:00:00.000Z","level":"INFO","source":"job-ops","message":"⏰ [visa-sponsors-uk] Next run scheduled for: 2026-04-18T02:00:00.000Z"},{"time":"2026-04-17T11:11:05.985Z","level":"INFO","source":"wss (stderr)","message":"[WS Server] Unknown message type: {\"type\": \"chat_e
```

### `/api/security` (api, public)

```typescript
{"events":[{"time":"2026-04-17T08:39:56.422Z","type":"system","severity":"info","source":"supervisord","message":"stopped: zo-space (terminated by SIGTERM)"},{"time":"2026-04-17T08:35:17.275Z","type":"system","severity":"info","source":"supervisord","message":"stopped: zo-space (terminated by SIGTER
```

### `/api/failures` (api, public)

```typescript
{"failures":[{"time":"2026-04-17T11:11:06.001Z","severity":"medium","category":"Service","source":"web","message":"[Error: aborted] { code: 'ECONNRESET' }"},{"time":"2026-04-17T11:11:06.001Z","severity":"medium","category":"Service","source":"web","message":"[Error: aborted] { code: 'ECONNRESET' }"}
```

### `/api/trivia/dates` (api, public)

```typescript
{"dates":["2026-03-25","2026-03-26","2026-03-27","2026-03-28","2026-03-29","2026-03-30","2026-03-31","2026-04-01","2026-04-02","2026-04-03","2026-04-04","2026-04-05","2026-04-06","2026-04-07","2026-04-08","2026-04-09","2026-04-10","2026-04-11","2026-04-12","2026-04-13","2026-04-14","2026-04-15","202
```

### `/api/calendar` (api, public)

```typescript
{"error":"Unauthorized - Authentication required"}
```

### `/api/extension-save` (api, public)

```typescript
{"headers":{"accept":"application/json","accept-encoding":"gzip, deflate, br, zstd","connection":"keep-alive","host":"localhost:3099","user-agent":"Bun/1.2.21"},"envKeyLength":49}
```

### `/api/generate-icon` (api, public)

```typescript
{"error":"Missing job param"}
```

### `/share` (page, private)

```tsx
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta name="description" data-zo-default-seo="true" content="Space to showcase my Zo Computer projects. " />
    <meta name="author" content="Zo" />
```

### `/api/test-write` (api, public)

```typescript
{"success":true}
```

### `/api/test-exec` (api, public)

```typescript
{"success":true,"stdout":"tesseract 5.3.0\n leptonica-1.82.0\n  libgif 5.2.1 : libjpeg 6b (libjpeg-turbo 2.1.2) : libpng 1.6.39 : libtiff 4.5.0 : zlib 1.2.13 : libwebp 1.2.4 : libopenjp2 2.5.0\n Found AVX2\n Found AVX\n Found FMA\n Found SSE4.1\n Found OpenMP 201511\n Found libarchive 3.6.2 zlib/1.2
```

### `/zo-status` (page, public)

```tsx
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta name="description" data-zo-default-seo="true" content="Space to showcase my Zo Computer projects. " />
    <meta name="author" content="Zo" />
```

### `/api/benchmarks/refresh` (api, public)

```typescript
{"status":"refresh started"}
```

### `/api/billing` (api, public)

```typescript
{"plan":"Pro","credits":{"balance":3852,"used":6148},"billing":{"cycle_start":"2026-03-01","cycle_end":"2026-03-31","estimated_bill":0},"data_source":"STATIC_MOCK","note":"Billing data is mocked. Check Zo Billing page for real invoices.","last_updated":"2026-04-17T11:11:06.247Z"}
```

### `/api/audit` (api, public)

```typescript
{"events":[],"stats":{"total":0,"auth":0,"api":0,"failures":0,"system":0,"rejected":0},"data_source":"STATIC_MOCK","note":"Audit events are mocked. Security monitoring is active.","last_updated":"2026-04-17T11:11:06.248Z"}
```

### `/api/test-env` (api, public)

```typescript
{"headers":{"accept":"application/json","accept-encoding":"gzip, deflate, br, zstd","connection":"keep-alive","host":"localhost:3099","user-agent":"Bun/1.2.21"},"reqHeader":{"accept":"application/json","accept-encoding":"gzip, deflate, br, zstd","connection":"keep-alive","host":"localhost:3099","use
```

### `/` (page, public)

```tsx
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta name="description" data-zo-default-seo="true" content="Space to showcase my Zo Computer projects. " />
    <meta name="author" content="Zo" />
```

### `/receipts` (page, public)

```tsx
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta name="description" data-zo-default-seo="true" content="Space to showcase my Zo Computer projects. " />
    <meta name="author" content="Zo" />
```

### `/api/diagnose` (api, public)

```typescript
{"error":"Route /api/diagnose encountered an error"}
```

### `/api/receipts` (api, public)

```typescript
{"error":"Unauthorized"}
```

### `/openclaw-dashboard` (page, private)

```tsx
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta name="description" data-zo-default-seo="true" content="Space to showcase my Zo Computer projects. " />
    <meta name="author" content="Zo" />
```

### `/dashboard` (page, private)

```tsx
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta name="description" data-zo-default-seo="true" content="Space to showcase my Zo Computer projects. " />
    <meta name="author" content="Zo" />
```

### `/api/twinmind` (api, public)

```typescript
{"error":"Unauthorized - Authentication required"}
```

### `/api/datasets/start` (api, public)

```typescript
{"error":"Unauthorized - please log in to Zo Space"}
```

### `/docs` (api, public)

```typescript
User service unavailable
```

### `/api/sites` (api, public)

```typescript
{"routes":[],"total":0,"error":"Zo API unavailable"}
```

### `/api/my-models` (api, public)

```typescript
{"models":[{"modelName":"byok:857c99ef-13b7-4ef5-81d8-709ca6470896","label":" Aether_gpt-5.4-mini","provider":"","isByok":true},{"modelName":"byok:e3ecae53-f617-4fbe-8575-3ee1fa04cb87","label":"Z.AI_GLM-5-Turbo","provider":"","isByok":true},{"modelName":"byok:a5930920-fdfc-4d2d-865d-a8516e2b34c0","l
```

### `/knowledge-graph` (page, private)

```tsx
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta name="description" data-zo-default-seo="true" content="Space to showcase my Zo Computer projects. " />
    <meta name="author" content="Zo" />
```

### `/api/x-feed` (api, public)

```typescript
{"source":"cache","cached":true,"posts":[{"id":"2044341223406915787","url":"https://x.com/Z3nlyte/status/2044341223406915787","full_text":"who cares","date_string":"Apr 15, 2026","likes":1,"retweets":0,"replies":1,"views":21},{"id":"2039660632442839547","url":"https://x.com/Z3nlyte/status/2039660632
```

### `/api/updates` (api, public)

```typescript
{"source":"cache","updates":[{"id":"2044341223406915787","url":"https://x.com/Z3nlyte/status/2044341223406915787","full_text":"who cares","date_string":"Apr 15, 2026","likes":1,"retweets":0,"replies":1,"views":21,"type":"tweet"},{"id":"2039660632442839547","url":"https://x.com/Z3nlyte/status/2039660
```

### `/api/blog` (api, public)

```typescript
{"posts":[{"slug":"zo-city-isometric-city","title":"Zo City: Visualizing 229 Elements as an Isometric City","excerpt":"I turned my Zo Computer workspace into a living isometric city. 175 skills, 97 routes, 39 agents — all rendered as glowing buildings you can watch grow over time.","date":"2026-04-1
```

### `/kg-search` (api, public)

```typescript
{"error":"Route /kg-search encountered an error"}
```

### `/api/share` (api, public)

```typescript
{"error":"Unauthorized"}
```

### `/profile` (page, public)

```tsx
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta name="description" data-zo-default-seo="true" content="Space to showcase my Zo Computer projects. " />
    <meta name="author" content="Zo" />
```

### `/kg-entity` (api, public)

```typescript
{"error":"Name is required"}
```

### `/api/models` (api, public)

```typescript
{"models":[{"model_name":"byok:d4e0ee6f-1a00-42e8-9ad8-f1aaca2a8855","label":"ZenMux_gemini-3.1-flash-lite-preview","vendor":"Custom","type":null,"priority":null,"context_window":null,"is_byok":true},{"model_name":"byok:3ba88d07-8098-4879-b9ad-c42c45cfaeae","label":" Aether_minimax-m2.7","vendor":"C
```

### `/kg-by-type` (api, public)

```typescript
{"error":"Missing type parameter"}
```

### `/kg-stats` (api, public)

```typescript
{"vault":{"total_notes":229,"by_type":{"technology":35,"project":64,"company":15,"concept":38,"person":24,"place":21,"product":2,"activity":7,"organization":13,"store":1,"reflection":1,"library/tool":1,"document":1,"tool":1,"website":1,"event":2,"documentation":1,"system":1},"knowledge_entries":18},
```

### `/kg-recall` (api, public)

```typescript
{"error":"Route /kg-recall encountered an error"}
```

### `/kg-browse` (api, public)

```typescript
{"total":229,"entities":{"technology":[{"name":"API wrapper","file":"API wrapper","tags":[""],"updated":"2026-03-27 23:57","created":"2026-03-27 23:57"},{"name":"Bot","file":"Bot","tags":[""],"updated":"2026-03-01 10:08","created":"2026-03-01 10:08"},{"name":"Bun","file":"Bun","tags":[""],"updated":
```

### `/kg-graph` (api, public)

```typescript
{"nodes":[{"id":"Tauri","name":"Tauri","type":"technology","facts_count":1,"knowledge_count":0},{"id":"PostgreSQL","name":"PostgreSQL","type":"technology","facts_count":1,"knowledge_count":0},{"id":"TwinMind→Blitzit","name":"TwinMind→Blitzit","type":"project","facts_count":2,"knowledge_count":0},{"i
```

### `/api/files` (api, public)

```typescript
{"path":"/","items":[{"name":"Articles","path":"Articles","isDir":true},{"name":"Automations","path":"Automations","isDir":true},{"name":"Backups","path":"Backups","isDir":true},{"name":"Bookmarks","path":"Bookmarks","isDir":true},{"name":"config","path":"config","isDir":true},{"name":"CONVERSATION"
```

### `/api/auth-status` (api, public)

```typescript
{}
```

### `/api/services` (api, public)

```typescript
// fetch error: The operation timed out.
```

### `/api/system-stats` (api, public)

```typescript
{"timestamp":"2026-04-17T11:11:10.830Z","memory":{"total":34359738368,"used":9596620800,"available":24763117568,"percent":27.9,"totalGB":32,"usedGB":8.94},"disk":{"total":549755813888,"used":161959759872,"available":387796054016,"percent":29.5,"totalGB":512,"usedGB":150.84},"cpu":{"load1":0,"load5":
```

### `/api/credits` (api, public)

```typescript
{"credits":null,"error":"Billing API unavailable"}
```

### `/zo-space-theme-gallery` (page, public)

```tsx
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta name="description" data-zo-default-seo="true" content="Space to showcase my Zo Computer projects. " />
    <meta name="author" content="Zo" />
```

### `/zo-control-deck` (page, private)

```tsx
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta name="description" data-zo-default-seo="true" content="Space to showcase my Zo Computer projects. " />
    <meta name="author" content="Zo" />
```

### `/job-ops` (page, private)

```tsx
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta name="description" data-zo-default-seo="true" content="Space to showcase my Zo Computer projects. " />
    <meta name="author" content="Zo" />
```

### `/telemetry` (page, private)

```tsx
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta name="description" data-zo-default-seo="true" content="Space to showcase my Zo Computer projects. " />
    <meta name="author" content="Zo" />
```

### `/api/trivia/leaderboard` (api, public)

```typescript
{"today":[],"week":[],"month":[{"rank":1,"user_handle":"curtastrophe","score":1,"streak":1}],"alltime":[{"rank":1,"user_handle":"curtastrophe","score":1,"streak":1}]}
```

### `/zo-city-three-test` (page, public)

```tsx
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta name="description" data-zo-default-seo="true" content="Space to showcase my Zo Computer projects. " />
    <meta name="author" content="Zo" />
```

### `/api/trivia/random` (api, public)

```typescript
{"questions":[{"play_date":"2026-04-04","question":"A developer creates an API route at `/api/secrets` in Zo Space and sets `public: false`. They expect this to prevent unauthorized access. What is the actual security behavior?","options":["The route remains publicly accessible at the network level;
```

### `/api/trivia/by-date` (api, public)

```typescript
{"error":"Missing date parameter"}
```

### `/api/agents` (api, public)

```typescript
{"agents":[],"total":0,"error":"Zo API unavailable"}
```

### `/trivia` (page, private)

```tsx
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta name="description" data-zo-default-seo="true" content="Space to showcase my Zo Computer projects. " />
    <meta name="author" content="Zo" />
```

### `/repurpose` (page, private)

```tsx
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta name="description" data-zo-default-seo="true" content="Space to showcase my Zo Computer projects. " />
    <meta name="author" content="Zo" />
```

### `/api/datasets/proxy/*` (api, public)

```typescript
502 Bad Gateway - Datasette is not running or unreachable: Unable to connect. Is the computer able to access the url?
```

### `/api/contact` (api, public)

```typescript
{"error":"Method not allowed"}
```

### `/api/benchmarks` (api, public)

```typescript
{"models":{"gemini-3-1-pro-preview":{"name":"Gemini 3.1 Pro Preview","provider":"Google","creator":"Google","context":1000000,"input_cost":2,"output_cost":12,"intelligence":57.2,"ttft":19.664,"tokens_per_second":132.057,"source":"leaderboard_scrape","coding":55.5,"_source":"api"},"gpt-5-4-xhigh":{"n
```

### `/api/career-ops/scan` (api, public)

```typescript
{"error":"Method not allowed"}
```

### `/data/zo-trivia/` (page, private)

```tsx
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta name="description" data-zo-default-seo="true" content="Space to showcase my Zo Computer projects. " />
    <meta name="author" content="Zo" />
```

### `/speech-game` (page, public)

```tsx
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta name="description" data-zo-default-seo="true" content="Space to showcase my Zo Computer projects. " />
    <meta name="author" content="Zo" />
```

### `/speech-game/stickers` (page, public)

```tsx
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta name="description" data-zo-default-seo="true" content="Space to showcase my Zo Computer projects. " />
    <meta name="author" content="Zo" />
```

### `/api/speech-game-auth` (api, public)

```typescript
{"error":"Invalid passcode"}
```

### `/api/career-ops/batch` (api, public)

```typescript
{"success":true,"message":"Batch processing started (limit: 3). Check /dev/shm/career-ops-batch.log for progress.","status":"running","log":"/dev/shm/career-ops-batch.log"}
```

### `/speech-game-manifest.json` (api, public)

```typescript
{"name":"S-Blend Speech Game","short_name":"S-Blends","description":"Speech therapy practice game for s-blend words","start_url":"/speech-game","scope":"/speech-game","display":"standalone","orientation":"portrait","theme_color":"#7c3aed","background_color":"#eff6ff","icons":[{"src":"/icons/speech-g
```

### `/speech-game-sw.js` (api, public)

```typescript
const CACHE_NAME = "sblend-v1";
const PRECACHE = [
  "/speech-game",
  "/speech-game/stickers",
  "/icons/speech-game-192.png",
  "/icons/speech-game-512.png",
];

self.addEventListener("install", (e) => {
  e.waitUntil(
    caches.open(CACHE_NAME).then((cache) => cache.addAll(PRECACHE)).then(() =>
```

### `/data/zo-trivia/api/query` (api, public)

```typescript
{"error":"Invalid query. Use: stats, plays-by-date, questions-by-date, correctness-dist, leaderboard"}
```

### `/buildin-auth` (page, private)

```tsx
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta name="description" data-zo-default-seo="true" content="Space to showcase my Zo Computer projects. " />
    <meta name="author" content="Zo" />
```

### `/api/buildin/disconnect` (api, public)

```typescript
{"success":true}
```

### `/api/projects` (api, public)

```typescript
[{"name":"Zo Project Ops","desc":"Lightweight project planning and tracking interface for Zo Computer projects and related conversation threads.","status":"in-progress","tags":["Productivity","Workspace","Planning"],"link":"/Zo-Ops","order":0,"priority":"high"},{"name":"Zo Trivia","desc":"Daily inte
```

### `/api/test-deps` (api, public)

```typescript
{"name":"zo-space","type":"module","scripts":{"clear-cache":"rm -rf node_modules/.vite","build":"bun run clear-cache && vite build","prod":"bun run build && bun run server.ts"},"dependencies":{"@dnd-kit/core":"^6.3.1","@dnd-kit/modifiers":"^9.0.0","@dnd-kit/sortable":"^10.0.0","@dnd-kit/utilities":"
```

### `/speech-game/stats` (page, public)

```tsx
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta name="description" data-zo-default-seo="true" content="Space to showcase my Zo Computer projects. " />
    <meta name="author" content="Zo" />
```

### `/zo-city` (page, public)

```tsx
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta name="description" data-zo-default-seo="true" content="Space to showcase my Zo Computer projects. " />
    <meta name="author" content="Zo" />
```

### `/zos` (page, public)

```tsx
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta name="description" data-zo-default-seo="true" content="Space to showcase my Zo Computer projects. " />
    <meta name="author" content="Zo" />
```

### `/about-the-build` (page, public)

```tsx
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta name="description" data-zo-default-seo="true" content="Space to showcase my Zo Computer projects. " />
    <meta name="author" content="Zo" />
```

### `/404` (page, public)

```tsx
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta name="description" data-zo-default-seo="true" content="Space to showcase my Zo Computer projects. " />
    <meta name="author" content="Zo" />
```

### `/api/zos/now` (api, public)

```typescript
{"error":"Route /api/zos/now encountered an error"}
```

### `/api/zos/signals` (api, public)

```typescript
{"error":"Route /api/zos/signals encountered an error"}
```

### `/api/career-ops` (api, public)

```typescript
{"total":10,"applied":0,"responded":0,"interview":0,"offer":0,"rejected":0,"discarded":0,"avgScore":3.08,"pdfRate":0,"scoreDistribution":{"green":2,"yellow":4,"red":4},"statusBreakdown":{"Not Applied":1,"Evaluated":9},"pipelineFunnel":[{"stage":"Evaluated","count":10},{"stage":"Applied","count":0},{
```

### `/career-ops` (page, private)

```tsx
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta name="description" data-zo-default-seo="true" content="Space to showcase my Zo Computer projects. " />
    <meta name="author" content="Zo" />
```

### `/api/career-ops/pipeline` (api, public)

```typescript
{"pending":[{"url":"https://databricks.com/company/careers/open-positions/job?gh_jid=8285292002","company":"Databricks","title":"Delivery Solutions Architect","source":"ats_api","added_at":"2026-04-13T09:35:35.847Z"},{"url":"https://databricks.com/company/careers/open-positions/job?gh_jid=8476496002
```

### `/api/career-ops/applications` (api, public)

```typescript
{"applications":[{"id":"001","date":"2026-04-12","company":"Salesforce (Tableau)","role":"Data Analytics, Senior Analyst (Tableau exp mandatory)","url":"https://careers.salesforce.com/en/jobs/jr335903/","score":"3.0","status":"Not Applied","pdf":false,"report":"reports/001-salesforce-tableau-2026-04
```

### `/api/health-check` (api, public)

```typescript
{"services":[{"name":"Mengram (Direct)","category":"Memory","status":"Operational","lastChecked":"2026-04-17T11:10:53.371Z"},{"name":"Google Tasks","category":"Integrations","status":"Operational","lastChecked":"2026-04-17T11:11:00.143Z"},{"name":"TwinMind","category":"Integrations","status":"Operat
```

### `/api/speech-game-data` (api, public)

```typescript
{"error":"Unauthorized"}
```

### `/api/telemetry-data` (api, public)

```typescript
{"skills":[{"name":"fabric","runs":1598,"success":1598,"fail":0,"successRate":100,"avgDurationMs":2,"recentErrors":[]},{"name":"raindrop","runs":1580,"success":1580,"fail":0,"successRate":100,"avgDurationMs":1,"recentErrors":[]},{"name":"twinmind","runs":1240,"success":26,"fail":1214,"successRate":2
```

### `/model-advisor` (page, public)

```tsx
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta name="description" data-zo-default-seo="true" content="Space to showcase my Zo Computer projects. " />
    <meta name="author" content="Zo" />
```

### `/api/buildin/callback` (api, public)

```typescript
{"error":"Missing authorization code"}
```

### `/api/trivia/unsubscribe` (api, public)

```typescript
<!DOCTYPE html>
<html><body style="font-family:sans-serif;padding:40px;text-align:center;">
  <h2>Invalid Request</h2>
  <p>Email parameter is required.</p>
  <a href="/trivia">Go to Trivia</a>
</body></html>
```

### `/api/datasets/viewer` (api, public)

```typescript
{"success":false,"error":"Command failed: pkill -f 'datasette.*8002' || true; pkill -f 'duckdb.*serve.*8003' || true; pkill -f 'python.*8003' || true"}
```

### `/data-explorer` (page, private)

```tsx
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta name="description" data-zo-default-seo="true" content="Space to showcase my Zo Computer projects. " />
    <meta name="author" content="Zo" />
```

### `/api/datasets/list` (api, public)

```typescript
{"datasets":[{"id":"zo-trivia","name":"zo-trivia-questions","title":"Zo Trivia Questions","description":"Daily trivia questions for the Zo Trivia game covering Zo Computer features, edge cases, security, and power-user workflows.","path":"/home/workspace/Data/zo-trivia","type":"SQLite","tables":1},{
```

### `/api/puzzle-callback` (page, public)

```tsx
404 Not Found
```

### `/api/nav-links` (api, public)

```typescript
{"authenticated":false,"links":[{"name":"Home","path":"/","description":"Homepage","icon":"layout-dashboard","category":"public"},{"name":"Profile","path":"/profile","description":"User profile","icon":"settings","category":"public"},{"name":"Blog","path":"/blog","description":"Posts and articles","
```

### `/s/:id` (page, public)

```tsx
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta name="description" data-zo-default-seo="true" content="Space to showcase my Zo Computer projects. " />
    <meta name="author" content="Zo" />
```

### `/api/share/:id` (api, public)

```typescript
{"error":"Share not found"}
```

### `/api/trivia` (api, public)

```typescript
{"id":40,"play_date":"2026-04-17","question":"Which file is strictly required to exist in a skill's directory to define its metadata and instructions within Zo Computer?","options":["index.ts","manifest.json","SKILL.md","config.yaml"],"already_answered":false,"previous_answer":null,"user_handle":nul
```

### `/trivia/archive` (page, private)

```tsx
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta name="description" data-zo-default-seo="true" content="Space to showcase my Zo Computer projects. " />
    <meta name="author" content="Zo" />
```

### `/api/trivia/subscribe` (api, public)

```typescript
{"error":"Subscription failed","message":"JSON Parse error: Unexpected EOF"}
```

### `/api/family-log` (api, public)

```typescript
{"error":"Unauthorized"}
```

### `/trivia/leaderboard` (page, private)

```tsx
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta name="description" data-zo-default-seo="true" content="Space to showcase my Zo Computer projects. " />
    <meta name="author" content="Zo" />
```

### `/api/trivia/user-stats` (api, public)

```typescript
{"error":"Not authenticated"}
```

### `/api/projects-conversations` (api, public)

```typescript
{"error":"Query parameter 'q' is required"}
```

### `/api/receipt-images` (api, public)

```typescript
Unauthorized
```

### `/api/buildin/status` (api, public)

```typescript
{"connected":false}
```

### `/api/zos/build-log` (api, public)

```typescript
{"error":"Route /api/zos/build-log encountered an error"}
```

### `/secret` (page, public)

```tsx
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta name="description" data-zo-default-seo="true" content="Space to showcase my Zo Computer projects. " />
    <meta name="author" content="Zo" />
```

### `/api/zo-city-data` (api, public)

```typescript
{"total":381,"districts":[{"id":"skills","name":"Skills","color":"#8b5cf6","label":"Automation Hills","count":191},{"id":"agents","name":"Agents","color":"#ec4899","label":"Agent Quarter","count":51},{"id":"routes","name":"Routes","color":"#22c55e","label":"Downtown Core","count":131},{"id":"service
```

## Setup

**Directories to create:**
- `Data/zo-trivia`

