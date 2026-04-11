# Phase 01: Scaffold & Config System - Context

**Gathered:** 2026-04-11
**Status:** Ready for planning

<domain>
## Phase Boundary

Build the foundational skeleton: `index.html` shell, `config/certificate.config.json` with full schema, a JS config loader, dynamic CSS variable injection from config, an SPA view switcher (loading → search | certificate | error), and `/data/sample.json`. All visible text and colors must be driven by config — nothing hardcoded in HTML.

</domain>

<decisions>
## Implementation Decisions

### Config Schema Fields

- Schema should be **fully defined upfront** covering all phases (org info, certificate display, feature toggles, search copy) — no incremental extension needed in later phases
- **Flat naming convention** for org fields: `org_name`, `logo_url`, `primary_color`, `secondary_color`
- **Boolean feature flags** at the top level: `show_qr`, `show_description`, `show_seal` — all default `true`
- **Certificate display fields** all in config: `certificate_title`, `issued_by_label`, `date_label`, `id_label`, `signature_name`, `signature_title`, `seal_url`, `signature_url`
- **Search/landing page copy** also in config (for Phase 04): headline, subtext, input placeholder, button label, footer note

### CSS Variable Coverage

- Inject: **colors and image URLs** — `--primary-color`, `--secondary-color`, `--logo-url`, `--seal-url`, `--signature-url`
- **Font families** are also configurable via config: expose `--font-heading` and `--font-body` as CSS variables (fonts still loaded from Google Fonts CDN)
- **Certificate border** is configurable: both `border_color` and `border_width` come from config and map to CSS variables
- CSS variables are **injected once at app boot** (config load) — not re-injected on SPA view transitions

### File & Module Organization

- JavaScript: **single `app.js` file** — all logic in one place, no bundler needed
- CSS: **single `styles.css` file** — all styles including reset, variables, certificate, search, and error views
- Assets: **`assets/images/`** and **`assets/fonts/`** subdirectories (not a flat `assets/` folder)
- Attendee data: **`data/` at root level** — alongside `config/` and `assets/`

### Error & Loading States

- Loading indicator: **pure CSS spinner** — no library dependency
- Config failure error state: **centered message with icon** — "Could not load configuration. Please try again."
- Error state styling: **neutral grey/system colors** — no branding applied (brand config may be the thing that failed)
- **Same error state for all failure types** — network failure, JSON parse error, and invalid config shape all show the same message

### Copilot's Discretion

- Specific spinner animation style/size
- Exact error icon (SVG inline or Unicode symbol)
- Internal JS function/variable naming conventions
- Search page copy field names in config (e.g., `search_headline` vs `landing_headline`)

</decisions>

<specifics>
## Specific Ideas

- The config schema should be designed holistically for all 6 phases in Milestone 1.0 — downstream phases (QR toggle, PDF, search copy) should not need to introduce new top-level config keys
- Flat config structure preferred over nested objects (e.g., `primary_color` not `colors.primary`)
- CSS variable naming should mirror config key names where possible for clarity

</specifics>

<deferred>
## Deferred Ideas

None — discussion stayed within phase scope.

</deferred>

---

_Phase: 01-scaffold-config-system_
_Context gathered: 2026-04-11_
