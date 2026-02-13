# AGENTS.md — singhsidhukuldeep.github.io

> Comprehensive project reference for AI agents and contributors.
> Last updated: 2026-02-13

---

## Project Overview

**singhsidhukuldeep.github.io** is Kuldeep Singh Sidhu's personal GitHub Pages site. It serves as a minimal landing page with contact info and project links, plus a custom URL redirect system with a marketing splash screen.

- **Hosting**: GitHub Pages (static files only — no server, no build step)
- **Stack**: Pure HTML / CSS / JS (no frameworks, no bundler)
- **Domain**: `singhsidhukuldeep.github.io` (and potentially a custom domain)

---

## File Structure

```
singhsidhukuldeep.github.io/
├── index.html          # Main landing page
├── 404.html            # Redirect splash + 404 page (GitHub Pages catch-all)
├── ads.txt             # Ad verification file
├── AGENTS.md           # This file
├── .agents/
│   └── skills/
│       └── frontend-design/
│           ├── SKILL.md
│           └── LICENSE.txt
└── .claude/
    └── skills/
        └── frontend-design/  (symlink/copy of .agents version)
```

---

## Pages

### 1. `index.html` — Landing Page

The main entry point. A dark, elegant single-screen page with:

**Design**:
- Dark background (`#111111`) with gold (`#fbbf24`) and purple (`#a855f7`) accent colors
- Inter font (weights 300/400/500/600)
- Ionicons v7.1.0 for icons (loaded via unpkg CDN)
- Two ambient glare orbs (gold + purple) with `blur(80–90px)` that follow mouse/gyroscope
- Parallax effect on content + footer via `mousemove` and `deviceorientation`
- Staggered reveal animations (`translateY` + `blur`) with `animation-delay` cascading

**Content**:
- Intro text: greeting with highlighted name + LinkedIn CTA
- Divider line
- 4 project links with icons:
  - **Crack DS Interviews** → dsprep.com (`.fade-link` — text fades to show URL on hover)
  - **Your Everyday Tools** → OnlineToolsVault.com (`.fade-link`)
  - **MDresearchAI.com** → disabled (`.scramble-link .disabled-link` — scramble effect to "Under Development")
  - **SoulGita.com** → disabled (`.scramble-link .disabled-link` — scramble effect)
- Footer: social links (LinkedIn, GitHub, Website, Twitter) + copyright with dynamic year

**Interactive Effects**:
- `.fade-link`: On hover, text fades out (opacity 0), swaps to URL text, fades back in (opacity 1). 200ms transition.
- `.scramble-link`: On hover, text scrambles character-by-character to reveal target text (Matrix-style). Uses `setInterval` at 30ms with random characters from `ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789!@#$%^&*()`.
- `.disabled-link`: Prevents click navigation (`e.preventDefault()`), cursor: not-allowed, greyed out color.

**CSS Variables** (index.html):
```css
--bg-color: #111111;
--text-color: #f5f5f5;
--highlight-color: #fbbf24;
--muted-color: #a3a3a3;
--link-color: #d4d4d4;
```

---

### 2. `404.html` — Redirect Splash + 404 Page

GitHub Pages serves `404.html` for ANY path that doesn't match an existing file. This file handles two modes:

#### Mode A: Redirect (`/r/` prefix)

When the URL path starts with `/r/` and has content after it (e.g., `/r/google.com`), it:

1. Parses the redirect target from the path (everything after `/r/`)
2. Prepends `https://` if no protocol specified
3. Shows a 7-second splash screen with:
   - Brand header (lightning bolt + "Explore more.")
   - "Redirecting you to" label
   - Target domain displayed in large gold Syne font (**auto-shrinks to always fit one line**)
   - Dual progress bars (top thin bar + central bar with glowing dot)
   - Countdown timer ("Redirecting in 7s" → "Redirecting in 6s" → ... → "Redirecting now...")
   - Percentage counter (0% → 100%, updated via `requestAnimationFrame`)
   - 4 randomly-selected project marketing cards with **2-line descriptions** (from pool of 8)
   - "Not redirected? Click here →" fallback link
4. At 6.5s: triggers exit animation (blur + scale + fade)
5. At 7.0s: `window.location.href = target`

**Usage examples**:
- `singhsidhukuldeep.github.io/r/google.com` → redirects to `https://google.com`
- `singhsidhukuldeep.github.io/r/https://example.com/path` → redirects to `https://example.com/path`

#### Mode B: 404 (no `/r/` prefix)

Any other non-existent path shows a clean 404 page with:
- Brand header (lightning bolt + "Explore more.")
- Large "404" in gold→purple gradient text
- "This page doesn't exist."
- "Go back home →" pill button with gradient border on hover

#### Design System (404.html)

**Fonts**: Syne (display, 400–800), Space Mono (monospace labels), Inter (body, 300–500)

**CSS Variables**:
```css
--bg: #0a0a0a;
--surface: #141414;
--surface-2: #1c1c1c;
--border: #222222;
--border-hover: #333333;
--text: #f0f0f0;
--text-muted: #6b6b6b;
--text-dim: #4a4a4a;
--gold: #fbbf24;
--gold-glow: rgba(251, 191, 36, 0.4);
--purple: #a855f7;
--purple-glow: rgba(168, 85, 247, 0.3);
```

**Visual Effects**:
- Grain/noise texture overlay (SVG fractalNoise filter, 2.5% opacity)
- Gold ambient orb (700px, blur 80px, 12% opacity radial gradient)
- Purple ambient orb (500px, blur 90px, 15% opacity radial gradient, offset)
- Staggered entrance animations (10 delay slots: `anim-d1` through `anim-d10`)
- Exit animation: `scale(1.03)` + `blur(12px)` + `opacity: 0` over 0.6s
- Top progress bar: gold → orange → red → purple gradient with glow
- Central progress bar: gold → purple gradient with glowing dot pseudo-element
- Card hover: `translateY(-2px)`, gradient border reveal via mask-composite trick, arrow slides right + turns gold

#### URL Auto-Fit (Single Line Guarantee)

The redirect URL is **always displayed on a single line**, regardless of length or screen size:

- **CSS**: `white-space: nowrap; overflow: hidden; text-overflow: ellipsis; width: 100%;`
- **JS**: After rendering, a double-`requestAnimationFrame` callback measures `scrollWidth` vs `clientWidth` and shrinks the font in 0.5px steps (from the CSS-computed size down to a floor of 10px) until the text fits without overflow.
- **Fallback**: `text-overflow: ellipsis` is the CSS safety net if JS hasn't fired yet or the URL is extremely long even at min font size.
- The starting font size is `clamp(1.8rem, 5vw, 2.8rem)` — the JS only reduces from there, never increases.

#### Card Descriptions (2-Line Display)

Card descriptions use `-webkit-line-clamp: 2` with `-webkit-box-orient: vertical` to show up to 2 lines of text, providing enough context for users to understand each project. Overflow beyond 2 lines is hidden (no ellipsis, just clipped).

#### No-Scroll Layout

The page **never scrolls** on any screen size:

- `html, body { height: 100%; overflow: hidden; }` — enforced globally, no media query overrides
- All vertical margins use `clamp()` with viewport-height units so spacing auto-compresses on shorter screens:
  - `.brand`: `clamp(1rem, 3vh, 2.5rem)`
  - `.redirect-domain`: `clamp(0.75rem, 2.5vh, 2rem)`
  - `.progress-container`: `clamp(1rem, 3vh, 2.5rem)`
  - `.divider-gradient`: `clamp(0.75rem, 2vh, 2rem)`
  - `.projects-label`: `clamp(0.5rem, 1.5vh, 1.25rem)`
  - `.cards-grid`: `clamp(0.75rem, 2vh, 2rem)`
- Cards stay in a **2-column grid on all screen sizes** (never stacks to single column)

#### Responsive Behavior

**Desktop** (> 640px):
- `.page` padding: `2rem`
- Cards: `0.9rem 1rem` padding, 36px icon, 0.85rem title, 0.68rem description, arrow visible
- Card grid: `max-width: 520px`, `gap: 0.75rem`

**Tablet** (641–768px):
- Card grid: `max-width: 440px`

**Mobile** (≤ 640px):
- `.page` padding: `1.5rem 1rem`
- Cards: `0.6rem 0.7rem` padding, 28px icon, 0.75rem title, 0.6rem description
- Card favicon: 16px (down from 20px)
- Card **arrow hidden** (`display: none`) to save horizontal space
- Card grid: `gap: 0.5rem`
- Progress bar: `max-width: 280px`
- Ambient orbs shrunk (400px gold, 300px purple)

---

## Project Cards (Marketing Pool)

8 projects are defined in the `allProjects` array. On each redirect page load, 4 are randomly selected via Fisher-Yates shuffle.

| # | Name | URL | Icon (Ionicon) | Favicon URL | Description |
|---|------|-----|----------------|-------------|-------------|
| 1 | ProofMD | https://proofMD.ai | `medkit-outline` | `proofmd.ai/favicon.png` | Medical research assistant for clinical decisions |
| 2 | ReplyRunner | https://ReplyRunner.com | `megaphone-outline` | `replyrunner.com/fav.svg` | Reddit & X conversations into marketing channels |
| 3 | TrendingDraft | https://TrendingDraft.com | `create-outline` | `trendingdraft.com/favicon.svg` | Build your personal brand on LinkedIn |
| 4 | fitDietAI | https://fitDietAI.com | `nutrition-outline` | `fitdietai.com/favicon.ico` | Plan your diet one photo at a time |
| 5 | SoulGita | https://SoulGita.com | `book-outline` | `soulgita.com/favicon.ico` | Bhagavad Gita reimagined with AI |
| 6 | DSPrep | https://DSprep.com | `rocket-outline` | `dsprep.com/assets/images/favicon.png` | All-in-one open-source DS interview prep |
| 7 | ToolsVault | https://OnlineToolsVault.com | `construct-outline` | `onlinetoolsvault.com/vite.svg` | Free, private, browser-based everyday tools |
| 8 | TapWhisper | https://TapWhisper.com | `mic-outline` | `tapwhisper.com/favicon.png` | Best voice-to-text for Mac |

**Favicon strategy**: Each card tries loading the site's actual favicon via `<img>`. On load error (`onerror`), it replaces the `<img>` with the Ionicon fallback icon. This gracefully handles sites that are down (fitDietAI, SoulGita currently unreachable).

**Favicon status** (as of 2026-02-13):
- Working (real image): ProofMD (`.png`), ReplyRunner (`/fav.svg`), TrendingDraft (`/favicon.svg`), DSPrep (`/assets/images/favicon.png`), ToolsVault (`/vite.svg`), TapWhisper (`/favicon.png`)
- Unreachable (fallback to Ionicon): fitDietAI, SoulGita
- Note: Many SPAs return `text/html` at `/favicon.ico` (catch-all route). Always check the `<link rel="icon">` tag in page HTML for the real path.

---

## External Dependencies

| Resource | Version | CDN | Purpose |
|----------|---------|-----|---------|
| Inter | Variable | Google Fonts | Body text (index.html, 404.html) |
| Syne | Variable | Google Fonts | Display headings (404.html) |
| Space Mono | Variable | Google Fonts | Monospace labels (404.html) |
| Ionicons | 7.1.0 | unpkg | Icons throughout both pages |

All loaded via CDN. No `node_modules`, no package.json, no build tooling.

---

## Key Architecture Decisions

### Why 404.html for routing?
GitHub Pages has no server-side routing. The only catch-all mechanism is `404.html` — GitHub serves it for ANY request that doesn't match an existing file. This lets `/r/anything` resolve to `404.html`, where client-side JS reads `window.location.pathname` to determine behavior.

### Why no SPA framework?
The site is intentionally zero-dependency pure HTML/CSS/JS:
- Instant load (no bundle to parse)
- GitHub Pages compatible with no build step
- No version conflicts or supply chain risk
- Easy to maintain and modify

### Why Fisher-Yates shuffle?
Unbiased random selection of 4 from 8 projects. The algorithm shuffles the full array in-place, then slices the first 4 elements. This ensures every project has an equal probability of appearing.

### Why 7-second delay?
Gives visitors enough time to see and potentially click on the marketing cards. The delay was iterated through 4s → 7s → 10s → 7s based on user testing.

### Why vh-based clamp margins?
Using `clamp(min, vh-value, max)` for vertical spacing ensures the layout compresses gracefully on shorter viewports without scrolling. The `vh` middle value scales with screen height, while the `min` and `max` bounds prevent extremes.

### Why double requestAnimationFrame for URL fit?
A single rAF can fire before the browser has computed layout after toggling `display: flex`. The double-rAF pattern (rAF inside rAF) guarantees the browser has painted at least one frame, so `scrollWidth` and `clientWidth` return accurate measurements.

### Why always 2-column card grid?
Single-column layout on mobile would stack 4 cards vertically, making the page too tall and requiring scrolling. Keeping 2 columns at all breakpoints (with compact styling on mobile) ensures the page fits within the viewport.

---

## Timing Constants (404.html)

These values are synchronized across multiple locations in the file:

| What | Value | Where |
|------|-------|-------|
| Total redirect duration | **7 seconds** | JS: `remaining = 7`, `duration = 7000`, `setTimeout` at 6500/7000 |
| CSS progress bar animation | **7s** | `.top-bar-fill` and `.progress-fill`: `animation: fillProgress 7s linear` |
| Exit animation trigger | **6.5s** | `setTimeout` adding `.page-exit` class |
| Actual redirect | **7.0s** | `setTimeout` calling `window.location.href` |
| Countdown text | **"7s"** | `#countdown` initial text |

**WARNING**: When changing the redirect duration, ALL of the above must be updated together. There are CSS animations (`7s`), JS countdown (`remaining = 7`), JS duration (`7000`), exit animation trigger (`6500`), and redirect trigger (`7000`).

---

## Local Development

Since this is a GitHub Pages static site, you can serve it locally with any static file server. To properly test the `/r/` redirect routes, you need a server that serves `404.html` for missing paths:

```bash
python3 -c "
import http.server, socketserver, os
os.chdir('/Users/kuldeep/Downloads/GitHub/singhsidhukuldeep.github.io')

class Handler(http.server.SimpleHTTPRequestHandler):
    def do_GET(self):
        path = self.translate_path(self.path)
        if os.path.isfile(path):
            super().do_GET()
        elif os.path.isfile(path + '/index.html'):
            self.path = self.path.rstrip('/') + '/index.html'
            super().do_GET()
        else:
            self.path = '/404.html'
            super().do_GET()

    def end_headers(self):
        self.send_header('Cache-Control', 'no-store, no-cache, must-revalidate, max-age=0')
        self.send_header('Pragma', 'no-cache')
        self.send_header('Expires', '0')
        super().end_headers()

socketserver.TCPServer.allow_reuse_address = True
httpd = socketserver.TCPServer(('', 9000), Handler)
print('Serving on http://localhost:9000')
httpd.serve_forever()
"
```

**Test URLs**:
- `http://localhost:9000/` — Landing page (index.html)
- `http://localhost:9000/r/google.com` — Redirect splash (7s then redirects)
- `http://localhost:9000/r/https://example.com/path?q=1` — Redirect with full URL
- `http://localhost:9000/r/this-is-a-really-long-domain.example.com/deep/path` — Tests URL auto-shrink
- `http://localhost:9000/anything-else` — 404 page

**Caching issues**: Browsers aggressively cache `404.html`. The dev server above sends aggressive no-cache headers. If changes aren't appearing, hard-refresh with `Cmd+Shift+R` or open a new incognito window (`Cmd+Shift+N`).

---

## Design Language

Both pages share a cohesive dark aesthetic:

- **Background**: Near-black (`#0a0a0a` / `#111111`)
- **Accent gold**: `#fbbf24` — used for highlights, progress bars, hover states, brand
- **Accent purple**: `#a855f7` — used for secondary orb, gradient endpoints, 404 text
- **Ambient depth**: Blurred radial-gradient orbs create atmospheric lighting without being distracting
- **Motion philosophy**: Staggered entrance reveals (blur → clear, slide up → settle), exit with blur + scale out. Hover states are subtle lifts + gradient border reveals.
- **Typography hierarchy**: Display (Syne, bold) → Body (Inter, light/regular) → Mono labels (Space Mono, small uppercase)
- **No-scroll principle**: Content must always fit within the viewport. Use vh-based margins and compact mobile styling to achieve this.

---

## Potential Future Work

- Custom domain support (CNAME file)
- Analytics/tracking on redirect clicks
- Dynamic project data from an external source
- Open Graph / social preview meta tags for shared redirect links
- Additional marketing sections on the splash page

---

## Git Conventions

Based on existing commit history:
- Prefix: `feat:` for new features
- Style: lowercase descriptions, imperative mood
- Single-line preferred for simple changes, multi-clause for compound changes
