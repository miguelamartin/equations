# Math Learning App — Design Spec

**Date:** 2026-03-11
**Target user:** 12-year-old Spanish-speaking girl learning pre-algebra
**Platform:** Web app (browser), single `index.html` file

---

## Overview

A gamified math practice web app delivered as a single self-contained `index.html`. No build tools, no dependencies, no server required. Progress persists via `localStorage`. The entire UI is in Spanish.

---

## Features

### Problem Types (by level)

| Level | Type | Example |
|-------|------|---------|
| 1–2 | One-step equations | `x + 5 = 12` |
| 3–4 | Two-step equations | `2x + 3 = 11` |
| 5–6 | Negatives & fractions | `3x - 7 = 2`, `x/2 + 1 = 5` |
| 7–8 | Parentheses | `2(x + 3) = 14`, `3(2x - 1) = 15` |
| 9–10 | Variables on both sides | `3x + 2 = x + 10` |
| 11+ | Combined complexity | `2(x + 3) - x = 4x - 1` |

Problems are procedurally generated (randomized coefficients/constants within each level's constraints).

### Gamification

- **Points:** earned per correct answer (more points at higher levels)
- **Streak:** daily streak counter — resets if a day is skipped
- **Levels:** unlock every 10 correct answers; harder problem types unlock at higher levels
- **Level-up animation:** visual celebration when leveling up

### Feedback

- **Correct:** green confirmation + brief Spanish explanation of the solution steps
- **Wrong:** red indicator + the correct answer shown + a short hint in Spanish

### Progress Persistence

Saved to `localStorage` (no login required):
- Total points
- Current level
- Daily streak + last played date

---

## Architecture

Single `index.html` with three embedded sections:

### HTML Structure
- Header: app title, level badge, points counter, streak counter
- Main: problem display area, answer input field, submit button
- Feedback zone: result message + explanation
- Next button: advances to the next problem

### CSS
- Clean, friendly, colorful design suitable for a 12-year-old
- Color-coded feedback: green for correct, red for wrong
- Responsive layout (works on desktop and tablet)

### JavaScript Modules (in a single `<script>` tag, organized into logical sections)

1. **State** — current level, points, streak, last played date; loaded from and saved to `localStorage`
2. **Problem Generator** — generates randomized equations based on current level; returns `{ display, answer, explanation }`
3. **Answer Checker** — parses user input, compares to correct answer (handles decimals and fractions)
4. **Scoring** — updates points, checks for level-up, updates streak
5. **UI Controller** — renders problem, handles submit, shows feedback, triggers level-up animation

---

## UX Flow

1. App loads → reads `localStorage` → shows current level, streak, points
2. Generates first problem → displays equation
3. User types answer → submits (Enter key or button)
4. Immediate feedback shown (correct/wrong + explanation)
5. "Siguiente" button appears → user advances to next problem
6. Every 10 correct answers → level-up celebration + harder problems unlock
7. On each new day → streak increments (or resets if a day was skipped)

---

## Out of Scope

- User accounts or server-side storage
- Multiple user profiles
- Lessons or instructional content (practice only)
- Mobile-specific optimizations (web-first, responsive)
