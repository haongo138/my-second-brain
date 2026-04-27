---
type: Type
_icon: rocket
_color: "#f59e0b"
_order: 5
_list_properties_display:
  - role
  - tech_stack
  - end_date
_sort: "property:end_date:desc"
---

# Project Experience

A Project Experience captures one project you've worked on during your software engineering career — without tying it to a specific company. Each note is a self-contained, CV-ready entry built around the *work itself*: the problem, your contributions, the stack, and the outcomes. This format keeps your portfolio focused on what you actually built and learned, independent of where you built it.

## How to use

Create one note per project inside `project-experiences/`, named after the project: e.g. `project-experiences/realtime-chat-platform.md`, `project-experiences/legacy-payments-migration.md`. Use a descriptive, anonymized name when needed — e.g. `b2b-billing-rewrite` instead of the internal product name. If the project has a public name (open source, personal project) feel free to use it.

Keep entries written in past tense (or present tense for ongoing work), with verbs that emphasize impact: *led*, *shipped*, *reduced*, *scaled*, *introduced*, *migrated*. Numbers beat adjectives. Focus on the *work*, the *scope*, and the *outcomes* — not on where it happened.

## Properties

- **role** — Your role *on this project* (e.g. `Tech Lead`, `Backend Engineer`, `Solo Developer`). May differ from your formal job title.
- **domain** — Industry or problem space (e.g. `Fintech`, `Developer Tools`, `E-commerce`, `Healthcare`). Useful for filtering experience by sector.
- **scope** — Rough sizing: `Solo`, `Small team (2–5)`, `Medium (6–15)`, `Large (16+)`. Signals collaboration scale on a CV.
- **start_date** — `YYYY-MM` format. Sortable; renders cleanly on a CV.
- **end_date** — `YYYY-MM` for finished projects, `Present` for ongoing.
- **status** — `Shipped`, `Ongoing`, `Archived`, `Cancelled`. Be honest — cancelled projects can still showcase strong work.
- **tech_stack** — YAML list of wikilinks to `Technology Stack` notes used here (e.g. `[[technology-stacks/fullstack-go-nextjs-postgres]]`).
- **related_to** — Other notes this project connects to: follow-up projects, people, lessons.

## Sections

- **Summary** — One or two sentences. The "elevator pitch" version of this project. Should stand alone on a CV.
- **Problem & Context** — What problem this project solved, and the constraints around it (scale, deadline, legacy system, regulatory pressure). Sets up *why* the work mattered.
- **My Contributions** — What *you* specifically did. Be precise about the boundary between your work and the team's. 3–6 action-verb-led bullets.
- **Key Achievements** — Impact-focused bullets with metrics where possible. This is the section recruiters read.
- **Tech & Tools** — Project-specific specifics (which database, which queue, which deploy target). Cross-reference broader stacks via the `tech_stack` property.
- **Lessons Learned** — What you'd do differently, what surprised you, what scaled vs. what didn't. Useful for interview storytelling.
- **Notes** — Private context: things you can't share publicly (real client name, internal politics, why the project was canned). Strip anything sensitive before publishing externally.

## CV / Interview prep tips

- Treat **Key Achievements** as your source-of-truth for resume bullets. Edit them until each one stands alone — a recruiter scanning for 6 seconds should still get the impact.
- Numbers and scope sell. *"Reduced p95 latency from 800ms → 120ms across 14 services"* beats *"Improved performance"*.
- For each project, prep a 2-minute STAR-format story (Situation, Task, Action, Result) in **Lessons Learned**. Interviewers will ask "tell me about a project where…".
- Use the **Notes** section for context that's useful for *you* but not for outside readers — keep the rest of the note shareable as-is.
