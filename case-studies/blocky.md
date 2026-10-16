# Blocky: a diagram editor with an AI assistant

**Status:** my own product at an early stage. Private repository, no deployments, no users yet.

## Problem
People who sketch processes and funnels draw boxes and arrows, but the drawing cannot tell them what happens when numbers flow through it. I wanted an editor where a diagram can also be run, and where an assistant can suggest edits that the user accepts or rejects.

## What I built
- **Canvas editor.** Blocks, ports, edges and zones on a Konva canvas, with Preact, @preact/signals, SCSS/BEM and TypeScript on Vite.
- **Simulation.** Numeric signals run through the diagram.
- **AI proposals.** The user describes a change in plain language. The assistant returns a full proposed graph, and nothing changes until the user accepts it.
- **Groq proxy with per-user quotas.** The browser never calls the provider. The Hono backend sends requests to Groq (Llama 3.1 8B Instant by default). Each user has a monthly cap on model calls; over the cap the API returns 429. The server refuses to start without a valid cap, and without an API key it runs in stub mode.
- **Backend.** Hono on Node, Postgres 16, shared zod contracts in `shared/` used by both client and server, invite-only signup with argon2 and HMAC session cookies.

## How I worked
I set up and run coding agents (Cursor, Grok Bot). I design and write the specs, Cursor agents implement, and I review and merge. After each merged PR a QA agent pulls `main`, starts the stack locally, tests the changes in a browser and files labeled GitHub issues. Cursor agents fix them and I merge the fixes.

## Results and evidence
- On 18 September 2026 the QA agent filed issues #12 to #17 (2 bugs, 4 enhancements) before noon. A Cursor agent fixed all six in PR #18 (23 files, +162/-40), which I merged at 14:38 the same day. The re-test about 20 minutes later confirmed the fixes and found one new bug (#19).
- Repository created 8 September 2026; 11 PRs merged from 16 to 18 September.
- Every PR runs two required checks in GitHub Actions: install, typecheck and build, plus a Playwright smoke test (3 tests against local Vite). Both pass on `main`. `main` takes changes through PRs only, with no force-push.

## Links
- Code: private repository, walkthrough on request
- GitHub: https://github.com/Schwibl
