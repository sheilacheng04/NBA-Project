# NBA Project

A front-end web application that replicates the look and feel of [NBA.com](https://www.nba.com/), featuring live scores, standings, player stats, team rosters, and AI-powered playoff predictions for the 2025-26 NBA season.

---

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Project Structure](#project-structure)
- [Data Files](#data-files)
- [Sections](#sections)
  - [Home](#home)
  - [Standings](#standings)
  - [Stats](#stats)
  - [Teams](#teams)
  - [Predictions](#predictions)
- [Technologies Used](#technologies-used)
- [Getting Started](#getting-started)
- [How It Works](#how-it-works)
- [Customization](#customization)

---

## Overview

This project is a **single-page application (SPA)** built entirely with vanilla HTML, CSS, and JavaScript — no frameworks or build tools required. It mirrors the NBA.com interface with a dark navigation bar, scrollable scoreboard strip, hero banner, news cards, video highlights, conference standings, stat leaders, team cards, and a playoff probability board driven by JSON prediction data.

---

## Features

- **Responsive Design** — Adapts to desktop, tablet, and mobile screen sizes with a hamburger menu for smaller viewports.
- **SPA Navigation** — Hash-based client-side routing with smooth section transitions and browser back/forward support.
- **Scoreboard Bar** — Horizontally scrollable strip displaying recent game results with team logos and scores.
- **Hero Banner & News Grid** — Featured content area with All-Star Weekend coverage and news cards with images.
- **Video Highlights** — Horizontally scrollable row of video thumbnail cards for recent game and event highlights.
- **Conference Standings** — Sortable Eastern/Western Conference tables with win/loss records, percentages, home/away splits, last-10 records, and streak data. Playoff and play-in cut-off lines are visually indicated.
- **Season Stat Leaders** — Categorized leader boards for Points, Rebounds, Assists, Blocks, Steals, Three Pointers Made, Three Point %, Field Goal %, and Fantasy Points.
- **All 30 Teams** — Grid of team cards organized by conference, each displaying the team logo and name.
- **AI-Powered Predictions** — Playoff probability board loaded from a JSON file, featuring per-team cards with playoff probability and win percentage. Filterable by All Teams, Eastern Conference, or Western Conference.
- **Game-Level Predictions** — JSON-based matchup predictions with home-team win probabilities and visual probability bars.

---

## Project Structure

```
NBA-Project-main/
├── index.html                          # Main application (current version)
├── index_old.html                      # Original saved NBA.com page (reference)
├── predictions.json                    # Game-by-game matchup prediction data
├── formatted_predictions_percent.json  # Team-level playoff probability data
├── README.md                           # This file
└── assets/                             # Static assets
    ├── *.css                           # Stylesheets (original NBA.com styles)
    ├── logo*.svg                       # NBA team logos (30 teams)
    ├── logo-nba*.svg                   # NBA and league branding logos
    ├── icon-*.svg                      # Social media icons
    ├── *.jpg                           # News, hero, and video thumbnail images
    ├── saved_resource.html             # Saved reference pages
    └── f.txt                           # Additional asset file
```

---

## Data Files

### `predictions.json`

Contains game-by-game prediction data with the following fields per entry:

| Field           | Description                                  |
|-----------------|----------------------------------------------|
| `home_team`     | Home team name                               |
| `away_team`     | Away team name                               |
| `home_logo`     | Path to home team logo SVG                   |
| `away_logo`     | Path to away team logo SVG                   |
| `home_win_prob` | Home team win probability (0.0–1.0)          |
| `game_date`     | Scheduled game date (YYYY-MM-DD)             |
| `game_time`     | Scheduled tip-off time (e.g., "7:30 PM ET")  |

### `formatted_predictions_percent.json`

Contains team-level season predictions with the following fields per entry:

| Field                | Description                                |
|----------------------|--------------------------------------------|
| `TeamName`           | Full team name                             |
| `PlayoffProbability` | Probability of making the playoffs (e.g., "98.93%") |
| `WinPCT`             | Projected win percentage (e.g., "75.0%")   |
| `PointsPG`           | Average points per game                    |
| `OppPointsPG`        | Opponent average points per game           |
| `ThreePointPCT`      | Three-point shooting percentage            |

---

## Sections

### Home

The landing page features:
- A **hero banner** highlighting the 2026 NBA All-Star Weekend.
- A **video highlights** carousel with game recaps, dunks, and top plays.
- A **news grid** with cards covering All-Star events, MVP race, trade deadline, and player highlights.

### Standings

Displays the 2025-26 season standings for both conferences:
- Toggle between **Eastern** and **Western** Conference views.
- Columns: Rank, Team (with logo), Wins, Losses, Win %, Games Back, Home record, Away record, Last 10, Streak.
- Dashed lines indicate **playoff** and **play-in** cut-offs (after 6th and 10th seeds).

### Stats

Shows season leader boards across nine categories:
- Points Per Game, Rebounds Per Game, Assists Per Game
- Blocks Per Game, Steals Per Game, Three Pointers Made
- Three Point Percentage, Field Goal Percentage, Fantasy Points Per Game

Each category displays the top 5 players with their team abbreviation and stat value.

### Teams

A visual grid of all 30 NBA teams organized by conference:
- **Eastern Conference** — 15 teams displayed alphabetically.
- **Western Conference** — 15 teams displayed alphabetically.
- Each card shows the team logo and name with hover effects.

### Predictions

An AI-powered playoff probability board:
- **Intro card** explaining the AI-driven forecasting methodology.
- **Conference filter** buttons: All Teams, Eastern, Western.
- **Team probability cards** showing each team's playoff probability and win percentage, loaded dynamically from `formatted_predictions_percent.json`.

---

## Technologies Used

| Technology     | Usage                                          |
|----------------|------------------------------------------------|
| **HTML5**      | Page structure and semantic markup             |
| **CSS3**       | Styling, layout (CSS Grid, Flexbox), animations, responsive design via media queries |
| **JavaScript** | SPA routing, dynamic DOM rendering, Fetch API for loading JSON data |
| **Google Fonts** | Roboto, Roboto Condensed, Roboto Slab typefaces |

No build tools, bundlers, or JavaScript frameworks are used — the project runs directly in the browser.

---

## Getting Started

### Prerequisites

- A modern web browser (Chrome, Firefox, Edge, Safari).
- A local web server to serve the files (required for `fetch()` to load JSON data).

### Running Locally

1. **Clone or download** the repository.

2. **Start a local server** from the project root. For example:

   Using Python:
   ```bash
   # Python 3
   python -m http.server 8000
   ```

   Using Node.js (with `http-server`):
   ```bash
   npx http-server -p 8000
   ```

   Using VS Code: Install the **Live Server** extension and click "Go Live".

3. **Open the application** in your browser:
   ```
   http://localhost:8000/index.html
   ```

> **Note:** Opening `index.html` directly via `file://` will cause the prediction data to fail loading due to CORS restrictions on the Fetch API.

---

## How It Works

1. **SPA Routing** — Navigation links use `data-nav` attributes and hash-based URLs (`#home`, `#standings`, etc.). Clicking a link hides all sections and shows the target, updates the active nav state, and pushes a new browser history entry.

2. **Scoreboard Bar** — Game data is embedded in JavaScript and rendered as inline-styled cards in a horizontally scrollable track.

3. **Standings & Stats** — Team and player data are defined as JavaScript arrays/objects and rendered into HTML tables and grids on page load.

4. **Team Cards** — A logo mapping object (`teamLogoMap`) associates each team name with its SVG logo path. Cards are generated dynamically for both conferences.

5. **Predictions** — On first navigation to the Predictions section, the app fetches `formatted_predictions_percent.json` via the Fetch API, parses the response, and dynamically generates team probability cards. Conference filter buttons re-render the grid with filtered data.

---

## Customization

- **Update standings data** — Edit the `eastTeams` and `westTeams` arrays in the `<script>` section of `index.html`.
- **Update stat leaders** — Edit the `statsData` object in `index.html`.
- **Update predictions** — Modify `formatted_predictions_percent.json` or `predictions.json` with new data.
- **Add/change team logos** — Place new SVG files in the `assets/` folder and update the `teamLogoMap` object.
- **Adjust styling** — Modify CSS custom properties in the `:root` selector or individual component styles in the `<style>` block.
