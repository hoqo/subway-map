# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is an interactive Kyiv subway map built with SvelteKit, TypeScript, and D3.js. The application renders an SVG-based visualization of the subway system based on the official Kyiv metro map.

## Key Commands

```bash
# Development
yarn dev          # Start development server on localhost:5173
yarn dev --open   # Start dev server and open in browser

# Build & Production
yarn build        # Build for production
yarn preview      # Preview production build locally

# Code Quality (run these before committing)
yarn lint         # Run ESLint and Prettier checks
yarn format       # Auto-format code with Prettier
yarn check        # Run svelte-check for TypeScript errors
yarn check:watch  # Run type checking in watch mode

# Install dependencies
yarn              # Install all dependencies
```

## Architecture & Code Structure

### Core Technologies

- **SvelteKit 2.22.0** with Svelte 5 - Application framework
- **TypeScript** - Type safety with strict mode enabled
- **D3.js** - SVG path generation for subway lines (Catmull-Rom splines)
- **Vite** - Build tool and dev server

### Application Structure

The app follows SvelteKit's file-based routing with a single page displaying the subway map:

- **`src/routes/+page.svelte`** - Main page with header, map container, and legend
- **`src/lib/components/Map/Map.svelte`** - Core SVG map component (3500x3500 viewBox)
  - Renders subway lines as `<path>` elements using D3's curveCardinal
  - Renders stations as `<circle>` elements with optional labels
- **`src/lib/components/Map/mocks.ts`** - Subway line data with station coordinates
- **`src/lib/components/Legend/`** - Color-coded legend components

### Data Model

- **`iSubwayLine`** - Represents a subway line with:
  - `name`: string (line name)
  - `color`: string (hex color)
  - `nodes`: iSubwayStation[] (array of stations)
- **`iSubwayStation`** - Represents a station with:
  - `name?`: optional string (station name if labeled)
  - `x`, `y`: number (SVG coordinates)

### Styling Approach

- Global styles in `src/lib/global.css`
- Component-scoped styles using Svelte's `<style>` blocks
- Fixed layout: header (82px), map container (747px), legend footer

## Development Notes

When modifying the subway map:

1. Station coordinates are defined in `src/lib/components/Map/mocks.ts`
2. The map uses a 3500x3500 SVG coordinate system
3. D3's curveCardinal creates smooth curves between stations
4. Each subway line has a unique color for visual distinction
