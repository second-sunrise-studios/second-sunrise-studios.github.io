# Agent guide — Second Sunrise Studios landing

You are editing a static landing page for Second Sunrise Studios, an online school
for gamedev and digital art. The owner is not a programmer — they describe what they
want in plain language, and you apply the changes and publish them.

## Stack & constraints

- **Single file**: `index.html` is the entire site. No build step, no bundler, no framework.
- **CSS**: Tailwind via CDN (`cdn.tailwindcss.com`) + custom CSS in a `<style>` block inside `index.html`. Custom tailwind config is also inline.
- **Fonts**: Satoshi (Fontshare CDN) and JetBrains Mono (Google Fonts) loaded via `<link>`. The brand font `assets/fonts/ChargerSport.otf` is shipped but not currently wired in.
- **Hosting**: GitHub Pages, deployed from `main`. Push to `main` → live in ~30s.

**Do not**:
- Add a build step, npm dependencies, or a package.json.
- Migrate to a framework (React, Vue, Astro, etc.).
- Add server-side code — Pages serves static files only.
- Edit anything inside `reference/` — that directory is in `.gitignore` and contains source materials, not production assets.
- Reintroduce the astronaut video background (`reference/legacy/astronaut-hero.mp4`); it was explicitly removed.

**Do**:
- Make changes directly in `index.html`. The HTML is long but well-commented with section markers (`<!-- ============ NAVBAR ============ -->`, etc.) — use them to navigate.
- Reuse existing utility classes (`.font-display`, `.chip`, `.btn-primary`, `.btn-ghost`, `.panel`, `.panel-dark`, `.game-card`, `.hairline`, `.reveal*`, `.stat-num`, `.fld`). Don't invent parallel classes for the same purpose.
- Reuse the existing color palette: `navy-{950,900,800,700}`, `sunrise{,-400,-600,-glow}`, `teal-soft`. Defined in the inline tailwind config near the top.
- Keep image references pointing to `assets/`. If you add a new image, optimize it first (max ~1200px wide, target <200KB).

## Project structure

```
.
├── index.html              # The entire site
├── assets/                 # Everything the page serves
│   ├── logo-horizontal.png       # In use (header, hero, footer)
│   ├── logo-stacked.png          # Brand variant
│   ├── logo-stacked-compact.png  # Brand variant
│   ├── logo-white.png            # All-white variant
│   └── fonts/ChargerSport.otf    # Brand display font (not wired in)
├── reference/              # Source materials — IGNORED BY GIT, do not touch
│   ├── prototype.jpg              # Client's prototype
│   ├── source/                    # Original-resolution assets, .tif, .eps, .mp4
│   ├── client-uploads/            # Originals shared by the client
│   └── legacy/                    # Files removed from production
├── .gitignore
├── README.md
└── AGENTS.md               # This file
```

## Local preview

```sh
python3 -m http.server 8000
# open http://localhost:8000
```

Or open `index.html` directly in a browser — it works without a server because everything is CDN-based.

## Publishing changes

The workflow is intentionally minimal:

```sh
git add -A
git commit -m "<short description in english>"
git push
```

Within ~30 seconds, the change is live at the GitHub Pages URL configured for this repo. There is **no staging environment, no PR review, no CI**. Push = publish.

**If you break something in production**, revert the last commit:

```sh
git revert HEAD
git push
```

That re-publishes the previous working state immediately.

## Editorial conventions

- Page copy is in **Spanish (rioplatense, voseo)** — "aprendé", "vos", "querés", not "aprendes", "tú", "quieres". Keep this consistent in any new copy you write.
- The brand voice is direct, no filler ("enseñanza directa, sin relleno" is literally one of the value propositions). Avoid corporate filler in any new copy.
- The poetic anchor is "second sunrise / segundo amanecer / horizonte" — used as metaphor for learning and new starts. Use sparingly, don't overdo it.
- Section ordering is deliberate: Hero → Cursos → Tutorías → Por qué nosotros → Planes → Instructores → Contacto. Don't reorder without discussing it.

## When in doubt

- Make the smallest possible change that satisfies the request.
- Preserve existing visual identity (dark navy, sunrise orange, twin-sun background scene).
- Don't add features the user didn't ask for.
- If a change would require new dependencies, a build step, or restructuring the file — stop and ask the user first.
