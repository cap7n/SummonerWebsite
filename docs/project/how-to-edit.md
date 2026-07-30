# How to Edit This Wiki

The wiki is plain Markdown in `docs/`, built with [MkDocs Material](https://squidfunk.github.io/mkdocs-material/). Same setup as the TowerDrop wiki.

## Quick edits

Edit any `.md` file in `docs/`, commit, push to `main`. GitHub Actions rebuilds and deploys the site automatically (see `.github/workflows/deploy.yml`) in about a minute.

Adding a page: create the `.md` file, then add it to the `nav:` section of `mkdocs.yml`.

## Preview locally

```bash
pip install mkdocs-material
mkdocs serve
```

Open http://127.0.0.1:8000 — live-reloads on save.

## House style

- **Record decisions, not dreams.** Undecided things get a `!!! warning "Not decided"` box or go to [Open Questions](open-questions.md).
- Status pills for backlog items: `<span class="pill done">DONE</span>` — classes: `done wip todo idea check risk parked`.
- Answered questions move from Open Questions to the [Decision Log](decisions.md) *with the why*.
- Dates absolute (2026-07-30), never "yesterday".

## Useful blocks

```markdown
!!! note "Title"
    Callout box.

!!! warning "Not decided"
    The honesty box.

??? info "Collapsed details"
    Click-to-expand.
```
