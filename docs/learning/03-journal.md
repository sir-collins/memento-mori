# Build journal

A chronological log of how this app got built: what we did, why we did it
that way, and what tripped us up. `01-progress.md` tracks *what's done*. This
file tracks *how we got there*.

## 2026-11-25: Project 0, setting up

The idea came out of a conversation with an LLM: a *memento mori* tracker
that shows a whole life as a grid of weeks. It suits a first Go project
because the core is pure, deterministic date maths, and that's easy to
unit-test before any HTTP, database or UI gets involved.

**Stack decisions**

- **Go with the standard library only** for the backend. Go 1.22 added
  method and path-parameter routing to `net/http`, so a framework (Gin, Echo,
  Chi) would mostly hide the things worth learning: handlers, middleware as
  plain function wrapping, explicit errors.
- **A deep React stack** for the frontend, on purpose: TanStack
  Router/Query/Form/Table/Virtual, Zustand for client state, shadcn/ui,
  Zod. The split to learn is *server state* (TanStack Query owns whatever came
  from the API) vs *client state* (Zustand owns settings the user typed).
- **Monorepo** (`api/` + `web/` in one repo) so a feature that touches both
  sides lands as one branch and one PR, and so Project 6 can `embed` the
  built frontend into the Go binary.

**Carrying the working rules over.** The rules from n-fundamentals-pro
(explain before coding, a branch per step, ask before every commit/push/PR,
no attribution trailers, progress + journal on every step) lived in Claude
memories tied to that project's folder. A session in a new folder doesn't
see them, so they're now in this repo's `CLAUDE.md`.

**Gotcha: Go compiled from source.** `brew install go` on this Intel Mac
found no prebuilt bottle for this macOS version and compiled Go from source,
which took several minutes instead of seconds. Nothing was broken. It just
looked like a hang.

**Lesson:** for project rules to survive, they need to live in the project
(`CLAUDE.md`), not in tool memory tied to one folder.

## 2026-11-25: Project 0, publishing to GitHub

All the setup files went into `main` as a single commit
(`Add initial project structure and documentation`) instead of the planned
"initial commit + setup PR". That's fine for a repo's first commit: there's
no `main` on the remote yet for a PR to target. The repo is public at
`sir-collins/memento-mori`. This wrap-up (ticking the last box) is the first
change that goes through the normal branch → PR → merge flow.

**Gotcha: `gh repo create` needs a visibility flag when run non-interactively.**
Run via `!` inside Claude Code, `gh` can't show its prompts, so it fails with
"`--public`, `--private`, or `--internal` required". Pass the flag (and
`--push` to push `main` in the same command).
