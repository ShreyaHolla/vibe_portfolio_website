# AGENTS

This file documents how AI agents should work on the **Shreya V Holla — portfolio website** project.

## Project Overview

- **Purpose**: Personal portfolio for **Shreya V Holla** with Home, About, and Projects pages, plus a newsletter signup funnel.
- **Framework**: Astro (static output, suitable for Vercel).
- **Styling**: Plain CSS using a small design system of CSS variables (no Tailwind, no extra UI libraries).
- **Newsletter**: Formspree form endpoint as a placeholder (`https://formspree.io/f/YOUR_FORM_ID` to be replaced by the user).

## Tech & Configuration

- **Astro version**: `"astro": "^5.x"` (see `package.json`).
- **Output**: `output: "static"` in `astro.config.mjs` for static export.
- **Deployment**: Vercel, with `vercel.json` specifying:
  - `buildCommand: "npm run build"`
  - `outputDirectory: "dist"`
  - `framework: "astro"`

### Commands

Run all commands from the project root:

- `npm install` — install dependencies.
- `npm run dev` — local dev server (default `http://localhost:4321`).
- `npm run build` — production build into `dist/`.
- `npm run preview` — preview the production build locally.

## Design System & UX

- **Colors (CSS variables in `src/styles/global.css`)**:
  - `--color-bg: #FAF9F6` (off‑white/cream, main background).
  - `--color-text: #1A1A1A` (primary text).
  - `--color-text-secondary: #6B6B6B` (supporting text).
  - `--color-accent: #7C3AED` (primary accent, “violent purple”).
  - `--color-green: #2D5A4A` (secondary accent, used sparingly).
  - `--color-border: #E5E2D9` (borders and subtle dividers).

- **Typography (via Fontshare)**:
  - Headings: `Clash Display`, weight 500.
  - Body: `Cabinet Grotesk`, weights 100 & 400.
  - Fonts are loaded in `Layout.astro` via the Fontshare CDN link.

- **Layout & Feel**:
  - Clean, minimal, bold with **generous whitespace**.
  - Large typography for hero and page headings.
  - One clear focal point per section (hero, newsletter, projects grid, etc.).
  - Subtle hover states (opacity and small translate transforms).
  - Smooth scrolling via `html { scroll-behavior: smooth; }`.

## Files & Responsibilities

### Layout & Shell

- `src/layouts/Layout.astro`
  - Wraps every page: `<Header />`, `<Footer />`, `<main><slot /></main>`.
  - Loads Fontshare fonts and imports `../styles/global.css`.
  - Accepts `title` and optional `description` props for `<title>` and SEO meta.

### Components

- `src/components/Header.astro`
  - Sticky header with logo text **“Shreya V Holla”**.
  - Nav links: Home (`/`), About (`/about`), Projects (`/projects`).
  - Mobile hamburger menu toggling a full‑screen nav overlay.
  - Uses `Astro.url.pathname` to highlight the active link.

- `src/components/Footer.astro`
  - Simple footer with dynamic year, copyright.
  - Placeholder social links to Twitter, LinkedIn, GitHub.

- `src/components/Button.astro`
  - Variants: `"primary"` (violet), `"secondary"` (outline).
  - Supports `href` for link-style buttons or `type` for `<button>`.
  - Uses `.filter(Boolean)` on the `class:list` array to avoid `undefined`.

- `src/components/Newsletter.astro`
  - Section id: `id="newsletter"` for anchor linking.
  - Heading: “Join the newsletter”.
  - Subtext: “Weekly insights on design, code, and creativity.”
  - Form:
    - `action="https://formspree.io/f/YOUR_FORM_ID"` (to be replaced).
    - Email input + submit button (violent purple).
  - Uses a visually hidden label for accessibility.

- `src/components/ProjectCard.astro`
  - Reusable project card with:
    - Placeholder image/gradient block (or optional real image).
    - Title (Clash Display), description (Cabinet Grotesk).
    - “View Project →” CTA.
  - Hover: small lift + subtle shadow.

### Pages

- `src/pages/index.astro` (Home)
  - Hero:
    - Heading: “Designer & Developer”.
    - Subheading: “I build thoughtful digital experiences”.
    - Primary button → `/about`.
  - Newsletter section: `<Newsletter />` rendered beneath hero.

- `src/pages/about.astro` (About)
  - Page heading: “About”.
  - Two‑column grid (on desktop):
    - Left: placeholder colored block for portrait image.
    - Right: 2–3 paragraphs of placeholder bio text.
  - “Skills & Services” section (flex list of tags).
  - CTA button linking to `/#newsletter`.

- `src/pages/projects.astro` (Projects)
  - Page heading: “Projects”.
  - `projects` array with 3–4 placeholder entries.
  - Grid layout:
    - 1 column on mobile.
    - 2 columns on ≥768px.
  - Renders `<ProjectCard />` for each project.

## Agent Guidelines

- **Respect the design system**:
  - Reuse existing CSS variables for colors/spacing instead of introducing new ones unless strictly necessary.
  - Maintain the minimal, bold, whitespace‑rich aesthetic.

- **Technology constraints**:
  - Keep to Astro + plain CSS; avoid adding heavy dependencies (CSS frameworks, JS frameworks) unless the user explicitly asks.
  - Prefer static generation; don’t introduce server‑side rendering or dynamic runtimes without a clear requirement.

- **Accessibility**:
  - Use semantic HTML (`<main>`, `<header>`, `<footer>`, `<section>`, `<nav>`, `<article>`).
  - Maintain or improve ARIA attributes and focus styles.
  - Provide `alt` text or ARIA labels for images and decorative elements.

- **Performance**:
  - Keep pages light; avoid unneeded scripts and large assets.
  - Use Astro’s static output and component‑driven structure.

- **When extending the site**:
  - For new sections or pages, start from existing patterns (Layout, Button, ProjectCard).
  - Keep navigation consistent (update `Header.astro` when adding major new pages).
  - Document any new conventions or patterns in this `AGENTS.md` file.

## Newsletter Configuration

- To make the form live, the user must:
  1. Create a form in Formspree.
  2. Replace `YOUR_FORM_ID` in `src/components/Newsletter.astro` with the real ID.
  3. Optionally update copy to match the real newsletter focus.

Agents **must not** hard‑code a real Formspree endpoint without explicit user instruction.

## Deployment Notes

- Builds have been verified locally with `npm run build`.
- Vercel should auto‑detect Astro from `vercel.json`; no custom build step is required beyond `npm run build`.
- When changing output paths or build commands, ensure `vercel.json`, `astro.config.mjs`, and the README stay in sync.

