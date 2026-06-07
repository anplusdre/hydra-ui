 ---
  # Hydra UI — Dashboard. 

  Production-ready React component library 
  
  **Live demo → [creators.ocudeus.com](https://creators.ocudeus.com)**

  > Source code is private. This repo exists as a portfolio reference.

  ---

  ## What it does

  - **Content Creators** — browse, filter, and sort a KOL database by platform, tier, category, location, age, gender, and
  price range
  - **Campaign Planner** — node-based visual editor (React Flow) for building campaign activity graphs
  - **System Overview** — dashboard landing with key metrics
  - **Component Library** — internal design system with a live preview page

  ## Stack

  | | |
  |---|---|
  | Framework | Next.js 16 (App Router) |
  | Language | TypeScript |
  | Styling | SCSS Modules |
  | Node editor | React Flow (`@xyflow/react`) |
  | Backend/auth | Supabase |
  | Linter/formatter | Biome |
  | Runtime | Bun |

  ## Architecture notes

  - **Custom component library** — Button, Select, Table, Toast, Label, Tabs, Accordion, etc. built from scratch with zero
  UI-framework dependencies
  - **App Router conventions** — server components by default, `"use client"` only where interactivity is needed
  - **Shared data layer** — creator data and slug utilities extracted into a standalone module imported by both the listing
  page and the global Header
  - **Context-based search** — global `SearchContext` wires the Header search bar to page-level filtering without prop
  drilling

  ---
