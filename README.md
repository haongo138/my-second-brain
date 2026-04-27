# second_brain

A personal [Tolaria](https://github.com/refactoringhq/tolaria) vault — a folder of Markdown files with YAML frontmatter forming a personal knowledge graph.

Currently focused on **project experience** notes for portfolio and CV use, plus reusable **technology stack** references.

## Structure

```
.
├── AGENTS.md                # Vault conventions for AI agents
├── CLAUDE.md                # Claude Code shim (points at AGENTS.md)
├── note.md                  # Type definition: Note
├── type.md                  # Type definition: Type
├── project-experience.md    # Type definition: Project Experience
├── technology-stack.md      # Type definition: Technology Stack
├── project-experiences/     # Individual project write-ups
├── technology-stacks/       # Reusable stack notes
└── views/                   # Saved views (*.yml)
```

## Conventions

- One Markdown note per file, kebab-case filenames.
- The first H1 in the body is the display title; the `type:` frontmatter field assigns the note type.
- Type definitions live at the vault root.
- Relationships use `[[wikilinks]]` in frontmatter (e.g. `related_to`, `belongs_to`).
- Saved views live in `views/*.yml`. Filename = view id.
- Frontmatter keys starting with `_` are Tolaria-managed — leave them alone.

See [AGENTS.md](./AGENTS.md) for the full convention reference.

## Note types

| Type | Purpose |
|------|---------|
| Note | General-purpose documents |
| Type | Defines shared metadata for a category of notes |
| Project Experience | Employer-agnostic, project-centric portfolio entries |
| Technology Stack | Reusable stack/tooling references |

## Saved views

- `project-experiences.yml` — all Project Experience notes
- `shipped-projects.yml` — projects with `status: Shipped`
- `ongoing-projects.yml` — projects still in flight
- `surroundfi.yml` — SurroundFi-related notes (hub view)
