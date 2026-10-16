# DNBH: a rental and content site for a bike shop in Da Nang

**Status:** not in production yet. A demo is running for the owner, and launch is planned for October 2026.

## Problem
The shop handled rentals in Booqable, club rides in Strava and routes in RideWithGPS. Customers had no single place to pick a bike, book it and read about rides, and the owner had no way to edit the site himself.

## What I built
I was the only developer and project lead.
- **Rental wizard on Booqable.** Several steps: dates and bikes, gear and snacks, personal details, review and checkout. Pickup times follow the shop's opening hours, synced from Booqable.
- **Ask the Hub.** An on-site assistant. It calls gpt-4o-mini on the server and answers only from CMS content (FAQ, pages, routes, tours), with links to its sources. A filter blocks any price answers, a monthly cap limits usage, and a WhatsApp handoff passes the customer to a person.
- **CMS-managed content.** The owner edits pages, routes and SEO content cards in Payload.

Stack: Next.js 15.4, React 19, Payload CMS 3.90 on SQLite (Postgres is planned later), and a Hono backend in TypeScript on Node 24 for Booqable and the assistant.

## How I worked
I set up and run coding agents (Cursor, Grok Bot). I or a Cursor agent build on short-lived branches. An auditor agent reviews each diff: it runs typecheck, unit tests and build, checks schema rules, runs the site locally and takes Playwright screenshots at 4 widths, then compares the result with decisions I have already settled. I decide what changes. Fix lists go to a Cursor cloud agent.

Every PR has a required PR check (install, typecheck, unit tests, build). `main` accepts PRs only, squash merge, no force-push. Deploys to Vercel are manual.

## Results and evidence
- The owner edits pages, routes and content cards himself in Payload.
- 151 unit tests in 27 files, passing.
- 36 Playwright e2e spec files. A manual GitHub Actions run against the demo had 44 tests (mobile and desktop): 42 passed, 2 skipped. 62 Booqable tests need a live backend and are left out of remote runs.

## Links
- Code: private repository, walkthrough on request
- GitHub: https://github.com/Schwibl
