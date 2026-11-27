# Progress

Tracking status against [00-roadmap.md](./00-roadmap.md).

## Project 0: Setup (done)

- [x] Install Go via Homebrew: `go1.27.4 darwin/amd64` (built from source, no bottle)
- [x] Repo at `~/Projects/memento-mori`, monorepo layout (`api/`, `web/`, `docs/`)
- [x] `CLAUDE.md` with the working rules (learning mode, branch per step,
      ask before git actions, no attribution trailers, docs on every step)
- [x] `docs/02-commenting-standards.md`, adapted for Go doc comments + TSDoc
- [x] Roadmap, progress and journal in `docs/learning/`
- [x] GitHub repo `sir-collins/memento-mori` (public). Everything landed on `main`
      as one commit; `gh repo create --public --source=. --remote=origin --push`
      published it. This wrap-up went through branch `project-0-step-1-setup-wrapup` + PR
- [x] Rebuilt the dev environment on WSL2 (Ubuntu 26.04, x86_64) after the Intel
      Mac died: re-cloned to `~/projects/memento-mori`; git, gh (logged in),
      node 26/npm 11 were already present. Go `go1.27.4 linux/amd64` installed from
      the official go.dev tarball (SHA-256 verified) into `/usr/local/go`;
      `~/.bashrc` adds `/usr/local/go/bin` and `$HOME/go/bin` to `PATH`.
      `golangci-lint` deferred until Project 1 needs it

## Project 1: Go Foundations & the Pure Domain ← up next

## Project 2: JSON API

## Project 3: Frontend Foundation

## Project 4: Interactive Grid

## Project 5: Persistence & Notes

## Project 6: Ship It

## Project 7: Stretch (v2)
