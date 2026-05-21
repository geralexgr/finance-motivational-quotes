# Fortune Flow — CLAUDE.md

## Project structure
Single-file app — all HTML, CSS, and JS lives in `index.html`. There is no build step, no package.json, and no framework.

## Running the app
```bash
open index.html            # open directly in the default browser
npx serve .                # serve locally at http://localhost:3000
```

## Code style

### CSS
- **Always use CSS custom properties** for color, spacing, radius, and transition values — never hardcode raw values.
- Design tokens are defined in `:root`, `[data-theme="dark"]`, and `[data-theme="light"]`. Every new rule must respect both themes.
- New UI elements must use `var(--glass-bg)`, `var(--glass-border)`, `var(--toggle-bg)`, `var(--text-primary / secondary / tertiary)`, and `var(--accent)`.
- Transitions on theme-sensitive properties must include `var(--theme-transition)` (e.g. `transition: color var(--theme-transition)`).
- Use `backdrop-filter: blur(...)` + `-webkit-backdrop-filter` together for glass surfaces.
- Border-radius uses `var(--radius-pill)` for pill shapes and `var(--radius-lg)` for cards.
- Spacing uses `var(--spacing-xs / sm / md / lg / xl)` — no magic pixel values.

### JavaScript
- Vanilla JS only — no libraries or frameworks.
- `const` by default; `let` only when reassignment is needed.
- DOM queries run once at the top and are stored in named variables.

### Animation
- Entrance animations use `cubic-bezier(0.22, 1, 0.36, 1)` (spring-like).
- Theme transitions use `cubic-bezier(0.4, 0, 0.2, 1)` (ease).
- Interactive hover/active states use short `0.2s ease` transitions.

## What NOT to add
- No external JS libraries or CSS frameworks.
- No `<script src="...">` tags pointing to CDNs (Google Fonts link is the sole exception).
- No inline `style=""` attributes — all styles go in the `<style>` block.
- Do not hardcode `#hex` or `rgb()` colors outside the theme blocks.

## Git & PR workflow
- Branch naming: `feature/<short-description>` or `fix/<short-description>`.
- Target branch for PRs: `main`.
- Screenshots go in `assets/` and are captured with headless Chrome:
  ```bash
  /Applications/Google\ Chrome.app/Contents/MacOS/Google\ Chrome \
    --headless=new --screenshot=assets/screenshot.png \
    --window-size=1280,800 --hide-scrollbars http://localhost:5173
  ```
- Create PRs with:
  ```bash
  gh pr create --title "..." --body "..." --base main --head <branch>
  ```

## Verification
- After any visual change, take a screenshot and compare dark + light themes.
- After any JS change, manually test: navigation (Prev/Next buttons), keyboard shortcuts (Space, ←, →), copy-to-clipboard, and theme toggle persistence across refresh.
- There is no automated test suite — manual verification is the feedback loop.

## Important rules
- ALWAYS use existing CSS tokens — never introduce a new hardcoded value.
- ALWAYS verify both dark and light themes after any UI change.
- Keep `index.html` as the single source of truth — do not split into separate files unless explicitly asked.
