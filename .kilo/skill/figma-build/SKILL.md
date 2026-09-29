---
name: figma-build
description: Build a Next.js + Tailwind site from a Figma design using the Figma MCP server. Reads design specs, tokens, and layouts, then generates matching code.
---

# Figma Build Skill

You are an agent that builds production sites from Figma designs using the Figma MCP server.

## Prerequisites

1. Your Figma file must be live on figma.com (not just a local `.fig` file). If you only have `UI/Fit Log.fig`, upload it:
   - Create a free Figma account at figma.com
   - Click **New > Import** and select your `.fig` file
   - Open the file, click **Share > Copy link**
   - The URL looks like: `https://www.figma.com/design/ABC123def456/Fit-Log`
   - Copy the file key (`ABC123def456`) — you will pass it to MCP tools

2. The Figma MCP server is configured in `kilo.jsonc`. If you see tools prefixed with `figma_` in your tool list, the server is connected.

## Workflow

### Step 1 — Get design context

Start by pulling the full design context for the file. This returns colors, typography, spacing, and component specs.

```
Use the figma MCP tools to get the design context for file key: {{FIGMA_FILE_KEY}}
Focus on: color styles, text styles (font family, size, weight), spacing/grid tokens, and button/card component variants.
```

### Step 2 — Extract layout for each screen

For each screen in the README requirements (Navbar, Hero/Banner, Library, Workout Details, My Plan, Footer), do:

1. Get the Figma node ID for that screen/frame.
2. Call the MCP tool to read the frame layout and measurements.
3. Extract: container width, columns/gutter, component positions, dimensions, and any constraints.

### Step 3 — Generate tokens

Convert extracted design tokens into a Tailwind config (`tailwind.config.js`) and a CSS variables file (`app/globals.css`). Map Figma colors to a palette, typography to heading classes, etc.

### Step 4 — Scaffold the project

If not already scaffolded:

```bash
npx create-next-app@latest . --typescript --tailwind --app --eslint --src-dir
```

### Step 5 — Build components

For each UI component in the README, implement a React component that matches the Figma spec exactly. Common components for this project:

- `components/Navbar.tsx` — with Plan/Saved badge counters
- `components/Hero.tsx` — banner with CTA and hero image
- `components/LibraryCard.tsx` — workout card with stats row
- `components/WorkoutDetail.tsx` — two-column detail page
- `components/StatsCard.tsx` — metric summary card
- `components/Footer.tsx`

### Step 6 — Wire up data

This project uses the API: `https://api.api-store.workers.dev/api/fitlog`

- Create `lib/api.ts` with a `fetchWorkouts()` function
- Use SWR or React Query for data fetching with loading states
- Type the data with TypeScript interfaces

### Step 7 — Add interactions

Implement per README:
- Add to Plan / Save for Later buttons → update state, increment badge counters, show toasts
- Mark as Done / Remove buttons on My Plan page
- Sort dropdown (Duration, Calories, Rating)
- Tab switching (Today's Plan / Saved)
- Empty states
- 404 page
- Loading animations

## Tool Reference (Figma MCP)

| Tool | Purpose |
|---|---|
| `figma_get_design` | Full design context (tokens, components) for a file |
| `figma_get_frame` | Layout + measurements for a specific frame/node |
| `figma_export_images` | Export images/assets at specific scales |
| `figma_get_styles` | Color + text styles |
| `figma_get_components` | Component variants and properties |
| `figma_add_comment` | Add a comment to a Figma frame (for notes) |

## Usage

```
Use the figma-build skill with Figma file key: <FILE_KEY>
```

The skill auto-detects available `figma_*` MCP tools. If no Figma tools appear, double-check your MCP config in `kilo.jsonc` and restart your Kilo session.
