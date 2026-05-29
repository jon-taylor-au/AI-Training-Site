
# CLAUDE.md — Sparke Helmore AI Training Platform

## What This Project Is

A self-paced, gamified AI literacy training platform for law firm staff. Delivered as a **single HTML file** (`index.html`). No build pipeline. No dependencies. Vanilla JS only.

The audience ranges from tech-naive to tech-comfortable law firm staff. Tone is direct and professional — not corporate e-learning.

---

## Hard Technical Constraints

These are non-negotiable. Never violate them.

- **Single HTML file** — everything (HTML, CSS, JS) in one `index.html`
- **No frameworks** — no React, Vue, Alpine, or any JS library
- **No external dependencies** — no CDN imports, no npm, nothing
- **No localStorage or sessionStorage** — ever, for any reason
- **API key** — entered by user on first load, stored in a JS variable only, never persisted
- **En-AU spelling** throughout all UI copy (e.g. "colour", "organisation", "recognise")
- **Mobile-responsive** layout
- **CSS-only animations** — no JS animation libraries

---

## Visual Design Tokens

### Sparke Helmore Brand Palette

| Name | Hex | Use |
|---|---|---|
| Primary | `#d95e00` | Headings, accents, XP pills, unlocked node borders |
| Primary-Alt | `#ec7a08` | Hover/brighten state, active module glow |
| Accent | `#aa1948` | Escape Room (boss module) only |
| Dark | `#37424a` | Page background, header/sidebar backgrounds |
| Mid | `#8f8f8f` | Captions, dividers, secondary text |
| Light | `#f2f2f2` | Card surfaces, completed-module backgrounds |
| White | `#ffffff` | Text on dark backgrounds |
| Success | `#5b8f22` | Completed checkmarks |

Secondary accents (use sparingly, one per context max):
- Teal `#007ea3`
- Purple `#693a77`
- Aqua `#00afd8`
- Green `#5b8f22`

Persistent header: platform title ("Sparke AI Training"), XP counter, badge shelf (10 slots, greyed until earned).
Progress bar across top: shows X/9 complete (8 modules + escape room).

---

## Build Approach

Build in stages. Complete and verify each stage before starting the next. The file will be large — do not attempt to rewrite the entire file in one pass. Use targeted edits (str_replace or equivalent) when modifying existing code.

Stage order is defined in `02_staged_build_instructions.md`. Follow it exactly.

---

## Project Files (Read-Only Reference)

All four files are in the project directory. Read them before starting any stage.

| File | Purpose |
|---|---|
| `01_master_brief.md` | Overall spec, design tokens, gamification system |
| `02_staged_build_instructions.md` | Stage-by-stage build instructions — follow this |
| `03_prescripted_content.md` | All module copy, quiz questions, scenario text — use verbatim |
| `04_api_prompts_reference.md` | Exact system prompts for all 3 API calls — use verbatim |

---

## Module Overview

| # | Title | API? |
|---|---|---|
| 1 | What Is AI Actually Doing? | No |
| 2 | Writing a Good Prompt | Yes — API Call #1 |
| 3 | Productive Friction | No |
| 4 | What Not to Put In | No |
| 5 | Knowing When AI Is Wrong | No |
| 6 | AI for Your Actual Job | No |
| 7 | LYRA: Prompt Optimisation | Yes — API Call #2 |
| 8 | Legal Prompt Library | No |
| ER | The Escape Room | Yes — API Call #3 (Stage 4 only) |

Modules unlock sequentially. Module 1 unlocked on load. Escape Room locked until all 8 modules complete.

---

## Gamification System

### XP Awards
| Event | XP |
|---|---|
| Complete any module (1–8) | +100 |
| Module 2 bonus (score ≥ 28/40) | +50 |
| Module 7 bonus (score ≥ 28/40) | +50 |
| Each escape room stage (×4) | +50 |
| Escape room completion bonus | +200 |

### Badges (in order)
First Contact · Prompt Apprentice · Friction Fighter · Vault Keeper · Hallucination Hunter · Role Player · LYRA Certified · Legal Eagle · Escape Artist · Full Stack Human

---

## API Implementation Rules

All three API calls use identical config:
- Endpoint: `https://api.anthropic.com/v1/messages`
- Model: `claude-sonnet-4-20250514`
- `max_tokens: 1000`
- Returns JSON only — parse with `JSON.parse()`, strip accidental markdown fencing first
- Wrap in try/catch — on failure, show "Something went wrong — please try again." and preserve user input
- Show loading state during call ("Evaluating your prompt...")

**API Call #1** — Module 2: user writes a prompt, scored on Role/Context/Task/Constraints (each /10). Returns preview, scores, feedback, improved prompt.

**API Call #2** — Module 7: user rewrites a weak prompt using LYRA. Scored on Deconstruct/Diagnose/Develop/Deliver (each /10). Returns scores, feedback, LYRA-optimised version.

**API Call #3** — Escape Room Stage 4: LYRA-quality prompt evaluated against same 4 stages. Threshold is 30/40 to unlock. Returns `unlocked: true/false`. Never override this in the UI — it is the gate.

Full system prompts for all three calls are in `04_api_prompts_reference.md`. Use them verbatim.

---

## Key Behaviours to Never Break

- Never write API key to any storage
- Never override API scores or `unlocked` status in the UI
- Never lose user input on API error — always preserve textarea content
- Never use a JS animation library
- Never import anything from a CDN
- Always use en-AU spelling
- Always follow stage order from `02_staged_build_instructions.md`

---

## Current Build Status

- [x] Stage 1 — Shell and Navigation (Winding Path / Direction B layout)
- [ ] Stage 2 — Module 1
- [ ] Stage 3 — Module 2 (API Call #1)
- [ ] Stage 4 — Module 3
- [ ] Stage 5 — Module 4
- [ ] Stage 6 — Module 5
- [ ] Stage 7 — Module 6
- [ ] Stage 8 — Module 7 (API Call #2)
- [ ] Stage 9 — Module 8
- [ ] Stage 10 — Escape Room (API Call #3)
- [ ] Stage 11 — Completion State and Polish

Update this checklist as each stage is completed.
