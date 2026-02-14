# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Marketing website for **AI Services Hampshire** (trading as Antek Automation) — an AI automation agency in Andover, Hampshire, UK. Single-page site targeting local small businesses for AI voice agents, chatbots, and workflow automation.

**Live site:** [aiserviceshampshire.co.uk](https://aiserviceshampshire.co.uk)

## Tech Stack

Single `index.html` with inline CSS and vanilla JavaScript. No build step, no frameworks, no package.json. Fonts loaded from Google Fonts (Sora + DM Sans).

**No build or dev commands needed** — open `index.html` in a browser to preview. Deploy to any static host.

## File Structure

- `index.html` — main landing page (~2,970 lines, all CSS/JS inline)
- `privacy-policy.html` — legal privacy policy
- `terms.html` — legal terms of business
- `robots.txt` / `sitemap.xml` — SEO files (canonical domain: `aiserviceshampshire.co.uk`)
- `images/bolt.png` — case study screenshot

## Architecture

Single-page layout with fixed nav and anchor-based scrolling. Section IDs for navigation:

`#hero` → `#pain-points` → `#services` → `#demo` → `#how-it-works` → `#industries` → `#why-us` → `#faq` → `#contact`

Plus a hidden `about-micro` SEO text block and a footer.

### Key Integrations

- **Contact form** → POST to n8n webhook (`https://antekauto.app.n8n.cloud/webhook/29e3a09b-5b23-489b-a800-a07262afb4cb`), includes honeypot field (`website`, hidden via `aria-hidden`)
- **Cal.com embed** → inline booking widget (`antek-automation/30min`), rendered in `#my-cal-inline-30min`
- **Retell AI** → live demo phone numbers in the `#demo` section (partner integration)

### JavaScript Functionality (inline, end of index.html)

- Mobile hamburger menu toggle with ARIA attributes
- IntersectionObserver scroll-reveal with staggered delays
- Waveform bar animation (24 bars, random heights)
- FAQ accordion (max-height transitions)
- Stat counter animation (ease-out cubic on scroll)
- Contact form: validation → honeypot check → fetch POST to n8n → toast notification

## Design System

### Colour palette (CSS custom properties)

- Background: `#0a0f1c` (primary), `#111827` (secondary), `#1a1f2e` (cards)
- Text: `#f1f5f9` (primary), `#94a3b8` (secondary), `#64748b` (muted)
- Accents: `#3b82f6` (electric blue), `#06b6d4` (cyan), `#10b981` (emerald green — CTAs only)
- Border: `#1e293b`
- **No warm tones** — zero orange, amber, gold, coral, salmon, or yellow anywhere

### Typography

- Display/headings: **Sora** (Google Fonts)
- Body: **DM Sans** (Google Fonts)

### Animation constraints

- Staggered fade-up on scroll (IntersectionObserver, ~100ms delays)
- Card hover: `translateY(-4px)` with box-shadow transition
- Single animated gradient orb in hero (CSS keyframes)
- Number counter animation for stats
- **No** particle effects, floating bubbles, or matrix rain

### Layout rules

- Full-width sections, ~100px vertical padding, max-width 1200px container
- Mobile-first responsive (breakpoints: 768px, 1024px)
- No stock photos — CSS gradients, SVG patterns, and icons only

## Content & Copy Rules

- **UK English** spelling throughout (optimise, specialise, colour)
- Conversational but professional tone — target audience is local tradespeople and business owners, not developers
- Benefit-led copy — lead with what the customer gets

## SEO Requirements

- Single H1 (hero headline only), H2 per section, H3 for sub-items
- Semantic HTML5 (`<header>`, `<main>`, `<section>`, `<footer>`, `<nav>`)
- `lang="en-GB"` on `<html>`
- JSON-LD schemas: LocalBusiness (geo: 51.2115, -1.4914) and FAQPage
- Open Graph + Twitter Card meta tags, geo meta tags (GB-HAM, Andover)
- Canonical URL: `https://aiserviceshampshire.co.uk`
- Update `sitemap.xml` if adding new pages

## Quality Targets

- Lighthouse: 90+ on Performance, SEO, Accessibility, Best Practices
- No console errors
- JSON-LD validates at schema.org validator
- Dark theme consistent throughout — no white sections
