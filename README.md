# AI Services Hampshire

Marketing website for **AI Services Hampshire** (formerly Andover AI Automation) — an AI automation agency based in Andover, Hampshire, UK, specialising in AI voice agents, chatbots, and workflow automation for local small businesses.

**Live site:** [aiserviceshampshire.co.uk](https://aiserviceshampshire.co.uk)

## Tech Stack

- Single `index.html` with inline CSS and JavaScript for maximum performance
- No build step, no frameworks, no dependencies
- Vanilla JS (IntersectionObserver for animations, accordion, contact form)
- Google Fonts (Sora + DM Sans)

## Features

- **Rebranded Design:** Complete visual overhaul to "AI Services Hampshire" with a dark premium theme and specific "Hampshire" localization.
- **Hero Video/Orb:** Animated gradient orb and waveform visualization for AI context.
- **Interactive Demo:** Live Retell AI voice agent phone numbers and interactive chat simulation.
- **Service Breakdown:** Detailed sections for Voice Agents, Chatbots, and Workflow Automation tailored to local trades and businesses.
- **Industry Specifics:** Dedicated "Who We Help" section targeting Plumbers, HVAC, Estate Agents, and Healthcare in Hampshire.
- **Contact:** Integrated n8n webhook form and Cal.com booking widget.
- **Legal:** Dedicated Privacy Policy and Terms of Business pages.

## Hampshire SEO & Optimization

The entire site has been rewritten and optimised specifically for **Hampshire-based SEO**.

### 1. targeted Keywords
- **Primary:** "AI Services Hampshire", "AI Agency Hampshire", "AI Automation Andover"
- **Secondary:** "AI Voice Agents Hampshire", "Chatbots for Hampshire Businesses", "Workflow Automation South of England"
- **Location-Specific:** Andover, Winchester, Basingstoke, Southampton, Portsmouth.

### 2. Technical SEO
- **Meta Tags:** Fully updated `<title>`, `<meta name="description">`, and `<meta name="keywords">` to reflect the new brand and location.
- **Canonical URL:** Set to `https://aiserviceshampshire.co.uk` to prevent duplicate content issues.
- **Open Graph & Twitter Cards:** Custom social sharing previews with the new brand title and description.
- **Geo Tags:** Added specific `geo.region` (GB-HAM), `geo.placename` (Andover), and `geo.position` coordinates for local search relevance.

### 3. Structured Data (JSON-LD)
- **LocalBusiness Schema:** Full schema implementation defining the business as an "AI Agency" in Andover, Hampshire. Includes `areaServed` (Andover, Hampshire, South of England), `sameAs` links to Antek Automation, and specific `priceRange` and `openingHours` data.
- **FAQPage Schema:** Complete Q&A schema for the 10 FAQs, helping the site appear in Google's "People Also Ask" snippets.

### 4. Content Strategy
- **Localized Copy:** All text has been rewritten to speak directly to "Hampshire businesses," "Andover trades," and "local professionals."
- **Trust Signals:** "Certified Retell AI Partner" and "Powered by Antek Automation" badges prominent in the hero and footer.
- **Micro-Section:** A dedicated SEO text block at the bottom of the page reinforces the location and service keywords for LLMs and search crawlers.

## Deployment

No build step required. Deploy the root directory to any static hosting provider:

- **GitHub Pages** — push to `main`, enable Pages in repo settings
- **Netlify** — connect the repo, publish directory: `/`
- **Vercel** — import the repo, framework preset: Other
- **Any web server** — upload `index.html`, `privacy-policy.html`, `terms.html`, `robots.txt`, `sitemap.xml`, and the `images/` folder

## Project Structure

```
.
├── index.html                  # Main landing page (AI Services Hampshire)
├── privacy-policy.html         # Legal privacy policy page
├── terms.html                  # Legal terms of business page
├── robots.txt                  # Search engine crawl rules
├── sitemap.xml                 # Sitemap including new pages
├── images/
│   └── bolt.png                # Bolt Electrical case study screenshot
├── CLAUDE.md                   # Project guidance
└── README.md                   # This file
```

## Contact

**Email:** hello@antekautomation.com
**Phone:** 0333 038 9960
