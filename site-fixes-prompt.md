# Site Fixes Prompt — aiserviceshampshire.co.uk

Apply all of the following fixes to the site's `index.html`. The site is a single-page vanilla HTML file with inline CSS and JS, no build step.

---

## 1. Mobile Hamburger Menu — Full-Screen Solid Overlay

### Problem
The `.nav__mobile` div sits inside `<nav class="nav">` which has `backdrop-filter: blur(16px)`. Per CSS spec, `backdrop-filter` creates a new containing block for fixed-position descendants, so `position: fixed; bottom: 0` on the menu resolves relative to the 72px nav bar — not the viewport. The menu ends up 0px tall with content bleeding through.

### Fix

**HTML:** Move the `<div class="nav__mobile" id="navMobile">` element **outside** of `<nav>`. Place it between `</nav>` and `<main>` as a sibling:

```html
  </nav>

  <div class="nav__mobile" id="navMobile" role="menu">
    <a href="#services" role="menuitem">Services</a>
    <a href="#demo" role="menuitem">Demo</a>
    <a href="#how-it-works" role="menuitem">How It Works</a>
    <a href="#why-us" role="menuitem">Why Us</a>
    <a href="#faq" role="menuitem">FAQ</a>
    <a href="#contact" class="nav__cta" role="menuitem">Book a Free Discovery Call</a>
  </div>

  <main>
```

**CSS:** Bump `.nav` z-index to `10000`. Replace all `.nav__mobile` styles with:

```css
.nav__mobile {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  height: 100dvh;
  background: #0a0f1c;
  z-index: 9999;
  padding: 96px 32px 40px;
  display: flex;
  flex-direction: column;
  gap: 0;
  opacity: 0;
  visibility: hidden;
  transition: opacity 0.3s ease, visibility 0.3s ease;
  overflow-y: auto;
  -webkit-overflow-scrolling: touch;
}

.nav__mobile.active {
  opacity: 1;
  visibility: visible;
}

.nav__mobile a {
  display: block;
  font-size: 1.5rem;
  font-weight: 600;
  color: var(--text-primary);
  padding: 16px 0;
  border-bottom: 1px solid rgba(255, 255, 255, 0.08);
  transition: color 0.2s;
}

.nav__mobile a:last-child {
  border-bottom: none;
}

.nav__mobile a:hover {
  color: var(--accent-blue);
}

.nav__mobile .nav__cta {
  display: block;
  text-align: center;
  margin-top: auto;
  padding: 16px 24px;
  background: var(--accent-green);
  color: #000000;
  font-weight: 700;
  font-size: 1rem;
  border-radius: 8px;
  border-bottom: none;
}

.nav__mobile .nav__cta:hover {
  color: #000000;
}
```

**CSS:** Add hamburger-to-X animation:

```css
.nav__hamburger.open span:nth-child(1) {
  transform: translateY(7px) rotate(45deg);
}
.nav__hamburger.open span:nth-child(2) {
  opacity: 0;
}
.nav__hamburger.open span:nth-child(3) {
  transform: translateY(-7px) rotate(-45deg);
}
```

**JS:** Replace the mobile nav JS with this (adds X animation, scroll lock, close on outside tap):

```javascript
var toggle = document.getElementById('navToggle');
var mobile = document.getElementById('navMobile');
var scrollY = 0;

function closeMenu() {
  mobile.classList.remove('active');
  toggle.classList.remove('open');
  toggle.setAttribute('aria-expanded', 'false');
  toggle.setAttribute('aria-label', 'Open menu');
  document.body.style.position = '';
  document.body.style.top = '';
  document.body.style.overflow = '';
  document.body.style.width = '';
  window.scrollTo(0, scrollY);
}

function openMenu() {
  scrollY = window.scrollY;
  mobile.classList.add('active');
  toggle.classList.add('open');
  toggle.setAttribute('aria-expanded', 'true');
  toggle.setAttribute('aria-label', 'Close menu');
  document.body.style.position = 'fixed';
  document.body.style.top = '-' + scrollY + 'px';
  document.body.style.overflow = 'hidden';
  document.body.style.width = '100%';
}

toggle.addEventListener('click', function () {
  if (mobile.classList.contains('active')) {
    closeMenu();
  } else {
    openMenu();
  }
});

mobile.querySelectorAll('a').forEach(function (link) {
  link.addEventListener('click', function () {
    closeMenu();
  });
});

mobile.addEventListener('click', function (e) {
  if (e.target === mobile) closeMenu();
});
```

---

## 2. Mobile Grid Layouts — Single Column on Phones

### Problem
Services cards display in a 2-column grid on mobile, making text cramped and cards cut off.

### Fix

**Services grid:** Change the breakpoint where it goes single-column from `≤480px` to `≤768px`:

```css
/* 2-column only for tablets */
@media (max-width: 1024px) and (min-width: 769px) {
  .services__grid {
    grid-template-columns: repeat(2, 1fr);
  }
  .service-card--large {
    grid-row: span 1;
  }
}

/* Single column on mobile */
@media (max-width: 768px) {
  .services__grid {
    grid-template-columns: 1fr;
  }
  .service-card--large {
    grid-row: span 1;
  }
  .service-card {
    padding: 28px 22px;
  }
}
```

**Stats grid:** Change from `repeat(2, 1fr)` to `1fr` in the `≤768px` media query:

```css
@media (max-width: 768px) {
  .stats__grid {
    grid-template-columns: 1fr;
    gap: 16px;
  }
}
```

**Leave these alone** (already correct):
- Pain points: single column at ≤1024px
- How It Works: single column at ≤768px
- Demo cards: single column at ≤768px
- Why Us: single column at ≤768px
- Industries: 2-column at ≤480px (small cards, intentional)

---

## 3. Bolt Image — Use WebP

Change the case study image from PNG to WebP:

```html
<!-- Change this: -->
<img src="images/bolt.png" ...>

<!-- To this: -->
<img src="images/bolt.webp" ...>
```

Ensure `images/bolt.webp` exists alongside the PNG.

---

## 4. Add Demo Phone Numbers

In the phone demos section (inside the `<article>` with "Call Our AI Voice Agents"), add these entries after the existing phone numbers:

```html
<div class="phone-demo-item">
  <span class="phone-label">Ember &amp; Oak Restaurant AI Host</span>
  <a href="tel:+447426476540" class="phone-number">+44 7426 476540</a>
</div>
<div class="phone-demo-item">
  <span class="phone-label">Web Design for Tradespeople AI Assistant</span>
  <a href="tel:+447723488012" class="phone-number">+44 7723 488012</a>
</div>
```

---

## 5. PageSpeed: Lazy-Load Cal.com Embed

### Problem
Cal.com loads eagerly on page load, adding ~1.8s JS execution, ~170 KiB unused JS, and 7 long main-thread tasks.

### Fix
Replace the entire Cal.com `<script>` block with a lazy-loading version that uses IntersectionObserver to only load when the booking section scrolls into view:

```html
<!-- ═══ CAL.COM EMBED (lazy-loaded) ═══ -->
<script type="text/javascript">
  (function () {
    var calLoaded = false;
    function loadCal() {
      if (calLoaded) return;
      calLoaded = true;
      (function (C, A, L) { var p = function (a, ar) { a.q.push(ar); }; var d = C.document; C.Cal = C.Cal || function () { var cal = C.Cal; var ar = arguments; if (!cal.loaded) { cal.ns = {}; cal.q = cal.q || []; d.head.appendChild(d.createElement("script")).src = A; cal.loaded = true; } if (ar[0] === L) { var api = function () { p(api, arguments); }; var namespace = ar[1]; api.q = api.q || []; if (typeof namespace === "string") { cal.ns[namespace] = cal.ns[namespace] || api; p(cal.ns[namespace], ar); p(cal, ["initNamespace", namespace]); } else p(cal, ar); return; } p(cal, ar); }; })(window, "https://app.cal.com/embed/embed.js", "init");
      Cal("init", "30min", { origin: "https://app.cal.com" });
      Cal.ns["30min"]("inline", {
        elementOrSelector: "#my-cal-inline-30min",
        config: { "layout": "month_view", "useSlotsViewOnSmallScreen": "true" },
        calLink: "antek-automation/30min",
      });
      Cal.ns["30min"]("ui", { "hideEventTypeDetails": false, "layout": "month_view" });
    }
    var calTarget = document.getElementById('my-cal-inline-30min');
    if (calTarget && 'IntersectionObserver' in window) {
      var calObserver = new IntersectionObserver(function (entries) {
        if (entries[0].isIntersecting) {
          loadCal();
          calObserver.disconnect();
        }
      }, { rootMargin: '200px' });
      calObserver.observe(calTarget);
    } else {
      loadCal();
    }
  })();
</script>
```

---

## 6. PageSpeed: GPU-Composited Waveform Animations

### Problem
25 waveform `<span>` elements animate `height`, which triggers layout on every frame (non-composited).

### Fix

**CSS:** Set a fixed height and animate with `transform: scaleY()` instead:

```css
.hero__waveform span {
  width: 4px;
  height: 80px;
  border-radius: 4px;
  background: linear-gradient(to top, var(--accent-primary), var(--accent-secondary));
  animation: waveform 1.2s ease-in-out infinite;
  transform-origin: bottom;
  will-change: transform, opacity;
}

@keyframes waveform {
  0%, 100% {
    transform: scaleY(0.25);
    opacity: 0.4;
  }
  50% {
    transform: scaleY(1);
    opacity: 1;
  }
}
```

**JS:** Remove the `bar.style.height = ...` line from the waveform bar creation loop. The bars no longer need individual inline heights since the animation handles scale:

```javascript
var waveform = document.getElementById('waveform');
for (var i = 0; i < 24; i++) {
  var bar = document.createElement('span');
  bar.style.animationDelay = (i * 0.08) + 's';
  waveform.appendChild(bar);
}
```

---

## 7. PageSpeed: Footer Text Contrast (WCAG AA)

### Problem
Footer text uses `var(--text-muted)` (`#64748b`) on `#0a0f1c` background = ~3.6:1 contrast ratio. WCAG AA requires 4.5:1.

### Fix
Change all footer elements from `var(--text-muted)` to `var(--text-secondary)` (`#94a3b8`, ~5.9:1 ratio):

- `.footer__brand p` → `color: var(--text-secondary)`
- `.footer__links a` → `color: var(--text-secondary)`
- `.footer__copy` → `color: var(--text-secondary)`
- `.footer__tagline` → `color: var(--text-secondary)`
- `.footer__partner` → `color: var(--text-secondary)`

---

## 8. PageSpeed: Non-Render-Blocking Fonts

### Problem
Google Fonts CSS link blocks rendering for ~750ms on mobile.

### Fix
Replace the font loading `<link>` tags in `<head>` with the non-blocking pattern:

```html
<!-- Preconnect to third-party origins -->
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link rel="dns-prefetch" href="https://app.cal.com">

<!-- Fonts (non-render-blocking) -->
<link rel="preload" as="style"
  href="https://fonts.googleapis.com/css2?family=DM+Sans:ital,wght@0,400;0,500;0,600;0,700;1,400&family=Sora:wght@400;500;600;700;800&display=swap">
<link
  href="https://fonts.googleapis.com/css2?family=DM+Sans:ital,wght@0,400;0,500;0,600;0,700;1,400&family=Sora:wght@400;500;600;700;800&display=swap"
  rel="stylesheet" media="print" onload="this.media='all'">
<noscript><link
  href="https://fonts.googleapis.com/css2?family=DM+Sans:ital,wght@0,400;0,500;0,600;0,700;1,400&family=Sora:wght@400;500;600;700;800&display=swap"
  rel="stylesheet"></noscript>
```

Also add `min-height: 3.4em` to `.hero__sub` to prevent CLS during font swap.

---

## 9. Cloudflare Dashboard (manual, not code)

These cannot be fixed in code — do them in the Cloudflare dashboard:

- **Scrape Shield > Email Address Obfuscation** → OFF (removes render-blocking `email-decode.min.js`)
- **Rules** → Add security headers (HSTS, CSP, X-Frame-Options, COOP, X-Content-Type-Options) to improve Best Practices score
- **Caching** → Set long cache TTLs for static assets (images, CSS, JS)
