# Hydra UI

Production-ready React component library and dashboard built with Next.js, TypeScript, and SCSS Modules — no UI framework dependencies.

**Live demo → [creators.ocudeus.com](https://creators.ocudeus.com)**

> Source code is private. This repo exists as a portfolio reference.

---

## Overview

Hydra is a brand management platform for running influencer (KOL) marketing campaigns. It includes a full component system built from scratch, a content creator discovery interface, and a node-based visual campaign planner.

The goal was to ship a production-grade internal tool without leaning on any UI framework — every component is hand-rolled, fully typed, and composable.

---

## Features

### Content Creator Discovery
Browse and filter a KOL database across multiple dimensions simultaneously — platform, tier, follower range, category, location, age, and gender. Results update instantly with a paginated grid and table view. A slide-out filter panel keeps the UI clean while exposing full filtering power.

### Campaign Planner
A node-based visual editor built on React Flow. Users can compose campaign structures by connecting activity nodes, campaign nodes, and daily schedule nodes on an infinite canvas. Supports drag-and-drop, edge connections, and a live mini-map.

### Component Library Page
An in-app live preview page that renders every component in the design system with all its variants — used during development as a sandbox and doubles as documentation.

### Global Search
A keyboard-accessible search bar (`Ctrl+K`) in the header wires into each page's filter logic via React Context — no prop drilling, no external state library.

---

## Component System

All components are built from scratch with no third-party UI dependencies. APIs are variant-driven with typed props — no loose `className` overrides.

| Component | Description |
|---|---|
| `Button` | Solid, border, and ghost styles; accent, neutral, grey variants; icon support; small size |
| `Input` | Controlled text input with label, error, and disabled states |
| `Textarea` | Auto-sizing multiline input with the same API as Input |
| `Select` | Custom dropdown with option groups, small variant, grey style |
| `Toggle` | Accessible on/off switch with controlled state |
| `Tabs` | Horizontal tab switcher with active state and full keyboard nav |
| `Accordion` | Collapsible content sections with animated expand/collapse |
| `Table` | Sortable, typed data table with column config |
| `Card` | General-purpose content container |
| `Label` | Status badge with positive, warning, accent, neutral, grey, and negative variants |
| `Menu` | Dropdown menu with `MenuGroup` and `MenuItem` subcomponents |
| `Toast` | Notification system via context — `useToast()` hook, auto-dismiss, stacked |
| `PlatformBadge` | Platform-aware badge for Instagram, TikTok, YouTube, and X |
| `CreatorCard` | Composite card for KOL profiles — tier, stats, platform, and actions |
| more will be added.

### Example API

```tsx
<Button solid accent onClick={handleHire}>Hire</Button>
<Button border neutral icon={<Bell size={16} />} />
<Button small solid grey>More</Button>

<Label positive>Celebrity</Label>
<Label warning small>Macro</Label>

<Select
  options={PLATFORM_OPTIONS}
  value={platform}
  onChange={setPlatform}
  small
  grey
/>
```

---

## Architecture

### Stack

| | |
|---|---|
| Framework | Next.js 16 (App Router) |
| Language | TypeScript |
| Styling | SCSS Modules |
| Node editor | React Flow (`@xyflow/react`) |
| Backend / auth | Supabase |
| Linter / formatter | Biome |
| Runtime | Bun |

### Key decisions

**No UI framework.** Every component — buttons, dropdowns, modals, toasts — is written from scratch. This keeps the bundle lean, avoids version-lock, and means the component API is exactly what the product needs.

**SCSS Modules over CSS-in-JS.** Scoped class names with zero runtime cost. Global design tokens (colors, spacing, radii, typography) live in a shared SCSS variables file imported per-module.

**Server components by default.** Pages are server components unless they need interactivity. `"use client"` is applied at the lowest possible boundary — usually a leaf component, not an entire page.

**Context for cross-cutting state.** The search bar, toast notifications, and plan editor each have their own React Context. No Redux, no Zustand — the state surface is small enough that Context is the right tool.

**Shared data modules.** Data and utility functions used across multiple routes are extracted into standalone modules rather than imported from page files, keeping the dependency graph clean.

---

## Project Structure

```
app/
├── components/          # Design system — all reusable UI components
├── components-page/     # Live component preview page
├── content-creators/    # KOL discovery — listing + detail pages
│   ├── data.ts          # Creator data and slug utilities
│   ├── page.tsx         # Listing page with filters
│   └── [id]/            # Creator detail page
├── planner/             # Campaign planner
│   ├── page.tsx         # Plan list
│   └── [id]/            # Node editor + custom node types
├── context/             # React Context providers
├── icons.ts             # Icon re-exports
├── types.ts             # Shared TypeScript types
└── layout.tsx           # Root layout — shell, sidebar, header
```
