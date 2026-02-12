# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Marketing website for **Andover AI Automation** — an AI automation agency in Andover, Hampshire, UK. Single-page site targeting local small businesses for AI voice agents, chatbots, and workflow automation services. The full specification lives in `andover-ai-site-prompt_1.md`.

## Tech Stack (Two Options)

**Option A (Preferred):** Next.js 14+ (App Router, static export), Tailwind CSS, Framer Motion, TypeScript. Deploy to Vercel/Netlify.

**Option B (Simpler):** Single `index.html` with inline CSS/JS, vanilla JavaScript, no build step.

### If using Option A
```bash
npx create-next-app@latest . --typescript --tailwind --app
npm run dev          # local development
npm run build        # production build (static export)
npm run lint         # ESLint
```

## Architecture

Single-page layout with anchor-based navigation across 9 sections: Hero, Problem/Pain Points, Services (bento grid), How It Works (3-step timeline), Who We Help (industry cards), Why Choose Us/Stats, FAQ (accordion), Contact & Booking, Footer.

### Key Integrations
- **Contact form** → POST to n8n webhook (`https://antekauto.app.n8n.cloud/webhook-test/29e3a09b-5b23-489b-a800-a07262afb4cb`), includes honeypot spam field
- **Cal.com embed** → inline calendar booking widget (`antek-automation/30min`)
- **Icons** → Lucide Icons or Heroicons (outline style)

## Design System

### Colour palette
- Background: `#0a0f1c` (primary), `#111827` (secondary), `#1a1f2e` (cards)
- Text: `#f1f5f9` (primary), `#94a3b8` (secondary), `#64748b` (muted)
- Accents: `#3b82f6` (electric blue), `#06b6d4` (cyan), `#10b981` (emerald green — CTAs only)
- **No warm tones** — zero orange, amber, gold, coral, salmon, or yellow anywhere

### Typography
- Display: Cabinet Grotesk, Clash Display, Satoshi, or General Sans. **Not** Inter/Roboto/Arial.
- Body: Plus Jakarta Sans or DM Sans.

### Animation constraints
- Staggered fade-up on scroll (IntersectionObserver, ~100ms delays)
- Gentle parallax on hero background
- Card hover: `translateY(-4px)` with box-shadow transition
- Single animated gradient orb in hero (CSS only)
- Number counter animation for stats
- **No** particle effects, floating bubbles, or matrix rain

### Layout rules
- Full-width sections, 80-120px vertical padding
- Bento-style grid for services
- Asymmetric hero (text left, visual right)
- Mobile-first responsive (breakpoints: 320px, 768px, 1440px)
- No stock photos — CSS gradients, SVG patterns, and icons only

## Content & Copy Rules

- **UK English** spelling throughout (optimise, specialise, colour)
- Conversational but professional tone — target audience is local tradespeople and business owners, not developers
- Benefit-led copy — lead with what the customer gets
- Weave target SEO keywords naturally (see spec file for full keyword list with impression data)

## SEO Requirements

- Single H1 (hero headline only), H2 per section, H3 for sub-items
- Semantic HTML5 (`<header>`, `<main>`, `<section>`, `<article>`, `<footer>`, `<nav>`)
- `lang="en-GB"` on `<html>`
- JSON-LD schema: LocalBusiness (geo: 51.2115, -1.4914), Organization, FAQ
- Open Graph + Twitter Card meta tags
- Canonical URL, robots meta `index, follow`
- Generate `robots.txt` and `sitemap.xml`

## Quality Targets

- Lighthouse: 90+ on Performance, SEO, Accessibility, Best Practices
- No console errors
- JSON-LD validates at schema.org validator
- Dark theme consistent throughout — no white sections
