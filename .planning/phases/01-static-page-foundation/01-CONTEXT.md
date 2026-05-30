# Phase 1: Static Page Foundation - Context

**Gathered:** 2026-05-29
**Status:** Ready for planning

## Phase Boundary

Deliver a complete, well-designed static HTML page with the comparison table structure, all page content (title, description, methodology section), and Tailwind CSS styling. Two GPU columns show the default selections (H100, RTX 3090) with placeholders for Phase 2 data and Phase 3 interactivity.

**In scope:** PAGE-01–04 (title, description, tone), TABL-01–02 (table columns/rows), FEAT-03–04 (Tailwind styling, responsive design)

**Out of scope (deferred):** GPU data calculations (Phase 2), dropdown interactivity (Phase 3), GNUS column highlighting (Phase 2)

## Implementation Decisions

### Page Layout
- **D-01:** Centered single-column layout with `max-w-5xl` container and `mx-auto`. Content flows: page title → description paragraph → GPU selector area (placeholder) → comparison table → methodology section.
- **D-02:** Title is an `<h1>` in a header section. Description is a `<p>` with max-width prose for readability. Methodology is a `<section>` at the bottom.

### Table Design
- **D-03:** Comparison table uses Tailwind's `table-auto` with visible borders (`border`, `border-collapse`). Rows use alternating backgrounds (`bg-gray-50` on even rows) for readability. Header row uses `bg-gray-100`.
- **D-04:** Column order: Category/Precision Level → GNUS.ai (Decentralized) → GPU 1 (H100) → GPU 2 (RTX 3090). This matches the project request specification.
- **D-05:** Table uses clear numeric formatting with placeholder values for GPU columns (e.g., "—" or "TBD" for now, since real data comes in Phase 2).

### Mobile Responsiveness
- **D-06:** Table wrapped in `overflow-x-auto` div for horizontal scroll on small screens. Everything else flows naturally with Tailwind's responsive utilities.
- **D-07:** Base font size appropriate for readability. Text wraps naturally within table cells. No stacked/card-layout conversion — horizontal scroll preserves the comparison format.

### Controls Placeholder
- **D-08:** GPU selector area shows labeled static text: "GPU 1: H100" and "GPU 2: RTX 3090". No interactive elements yet (Phase 3 adds dropdowns). This gives users context without broken UI.
- **D-09:** The placeholder area is structurally separate from the table so Phase 3 can replace it cleanly.

### Claude's Discretion
- Color palette and exact spacing values (Tailwind defaults are suitable)
- Font sizing hierarchy (Tailwind's typography scale)
- Exact wording of description paragraph (must be factual, neutral, include key points from PAGE-02/03)

## Canonical References

**Downstream agents MUST read these before planning or implementing.**

### Requirements
- `.planning/project-request.md` — Original design spec with data values, table structure, and feature list
- `.planning/REQUIREMENTS.md` — Formal v1 requirements with REQ-IDs
- `.planning/PROJECT.md` — Project constraints (single HTML file, Tailwind CDN, vanilla JS, no build tools)

### Design & Structure
- `.planning/ROADMAP.md` § Phase 1 — Success criteria and phase dependencies

No external design specs or ADRs. Requirements fully captured in decisions and referenced documents above.

## Existing Code Insights

**Greenfield project** — no existing HTML or JavaScript files. All code will be new.

### Established Patterns
- **Single-file HTML:** All CSS (Tailwind via CDN) and JS (vanilla, inline) in one `index.html`
- **No frameworks:** No React, Vue, or build tools — consistent with project constraints

## Specific Ideas

No specific UI references or examples provided. Standard professional design with Tailwind defaults.

## Deferred Ideas

None — discussion stayed within phase scope.

---

*Phase: 1-Static Page Foundation*
*Context gathered: 2026-05-29*
