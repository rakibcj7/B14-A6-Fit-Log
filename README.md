# FitLog — Workout Library

A dark, no-nonsense gym companion built with Next.js. Pick a lift, lock it into today's plan, and watch the week's work add up.

## Description

FitLog is a responsive workout tracking web app. Users can browse a library of exercises (sourced from a live API), view detailed workout pages, add exercises to a daily plan, save favorites, mark workouts as complete, and track metrics — all with a dark theme inspired by the Figma design.

## Technologies Used

| Technology | Purpose |
|---|---|
| **Next.js 16 (App Router)** | Full-stack React framework with SSR/SSG |
| **TypeScript** | Type-safe component and data layer |
| **Tailwind CSS v4** | Utility-first styling and responsive design |
| **Lucide React** | Icon library |
| **REST API** | Live data from `api.api-store.workers.dev` |

## Features

1. **Workout Library** — Browse a 3×4 grid of exercises with category tags, stats (duration, calories, rating), and a sort dropdown (Duration, Calories, Rating).

2. **Workout Details** — Two-column layout with large image, key specs table, step-by-step instructions, and CTA buttons to add to today's plan or save for later.

3. **My Plan Page** — Tabbed interface (Today's Plan / Saved) with live metrics summary (Exercises, Minutes, Calories), mark-as-done, remove, and view-details actions.

4. **Persistent State** — Plan and saved workouts persist in localStorage across sessions with live badge counters in the navbar.

5. **Responsive Design** — Fully responsive across mobile, tablet, and desktop with collapsible grids and stacked hero layout.

6. **Toast Notifications** — Real-time feedback on all actions (add/save/remove/mark done).

7. **Loading & Empty States** — Skeleton loading on page load and a friendly empty state with a CTA when no workouts are saved.

8. **404 Page** — Custom not-found page for invalid routes with a back-to-home link.

## Getting Started

```bash
npm install
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) to view the app.

## Build

```bash
npm run build
```
