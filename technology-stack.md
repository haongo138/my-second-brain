---
type: Type
_favorite_index: 1
_favorite: true
_icon: layers
_color: "#8b5cf6"
_order: 1
_list_properties_display:
  - primary_language
  - related_to
_sort: "property:primary_language:asc"
template: |
  ---
  type: Technology Stack
  primary_language: []
  related_to: ""
  ---

  # 

  Short description of what this stack is for and who it suits.

  ## Architecture

  - **Backend**: 
  - **Frontend**: 
  - **Database**: 
  - **Deploy**: 

  ## Languages

  - 

  ## Backend

  - 

  ## Frontend

  - 

  ## Database

  - 

  ## Shared Tooling

  - 

  ## Observability

  - 

  ## CI/CD

  - 

  ## Notes

  - 
---

# Technology Stack

A Technology Stack collects the languages, tools, and libraries I reach for first when working in a given ecosystem. Each stack note is keyed by one or more **primary languages** and lists my favorite components for that ecosystem.

The default template is **fullstack-friendly**: it includes sections for backend, frontend, database, and the cross-cutting concerns that show up in any real app. For a single-language stack (e.g. a Rust CLI toolkit), delete the sections that don't apply and keep the rest lean.

## How to use

Create one note per stack, named after the dominant ecosystem (e.g. `rust-stack.md`, `fullstack-go-nextjs-postgres.md`). Fill in the sections below with your current favorites — keep it short, opinionated, and easy to update as preferences shift.

## Properties

- **primary_language** — One or more languages this stack centers around. Use a YAML list of wikilinks (e.g. `[[go]]`, `[[typescript]]`). Single-language stacks still use a list with one entry.
- **related_to** — Other stacks, projects, or notes this stack connects to.

## Sections

- **Architecture** — One-line summary of each tier (backend / frontend / database / deploy) so the shape of the system is visible at a glance.
- **Languages** — All languages in play (primary + companions like SQL, Bash, Dockerfile).
- **Backend** — Server-side framework, HTTP, persistence drivers, workers. Skip for frontend-only stacks.
- **Frontend** — Framework, UI primitives, data layer, forms, auth. Skip for backend-only stacks.
- **Database** — Engine, migrations, pooling, extensions, backups. Skip if there's no DB.
- **Shared Tooling** — Cross-cutting CLIs, package managers, task runners, env management.
- **Observability** — Tracing, metrics, error tracking, analytics.
- **CI/CD** — Pipelines, release tooling, deploy targets.
- **Notes** — Free-form rationale, tradeoffs, opinionated decisions, or links to deeper writeups.

For a single-language stack, you can collapse **Backend** / **Frontend** / **Database** into a single **Tools** + **Libraries** pair if that fits better — the template is a starting point, not a contract.
