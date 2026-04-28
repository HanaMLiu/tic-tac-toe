# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository

- **GitHub**: https://github.com/HanaMLiu/tic-tac-toe
- **Default branch**: `main` — tracked against `origin/main`
- Push changes with `git push`

## Running the Game

Open `tictactoe.html` directly in any web browser. There is no build step, server, or dependencies.

## Architecture

The entire project is a single self-contained file (`tictactoe.html`) with three sections:

- **CSS** (lines 7–107): Dark-themed layout using CSS Grid for the board, with transitions and a `@keyframes pulse` animation for winning cells.
- **HTML** (lines 110–132): Score display, status line, 9 `.cell` divs (each with `data-i` index 0–8), and a restart button.
- **JavaScript** (lines 135–end): All game logic.

### Key JS Internals

| Symbol | Purpose |
|---|---|
| `WINS` | Array of 8 winning index triples |
| `board` | Array(9) of `null \| 'X' \| 'O'` |
| `current` | Active player (`'X'` or `'O'`) |
| `gameOver` | Boolean; blocks clicks after a result |
| `score` | `{ X, O, Draw }` persisted across rounds |
| `init()` | Resets board/current/gameOver; preserves `score` |
| `checkWinner()` | Returns `{ winner, line }`, `{ winner: 'Draw' }`, or `null` |

Cell click handler on each `.cell` is the single entry point for all gameplay: it updates `board`, the DOM, calls `checkWinner()`, and either ends the game or advances `current`.
