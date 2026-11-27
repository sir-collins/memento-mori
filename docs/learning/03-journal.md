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

## 2026-11-28: Project 0, rebuilding on WSL

The Intel Mac crashed, so the project moved to WSL2 (Ubuntu 26.04) on a
fresh clone. The repo itself was safe on GitHub, which is the whole point
of publishing early. Only the tools had to come back. git, `gh` (already
logged in), node and npm were present; Go was the one gap.

**Why the official tarball, not `apt install golang`.** Ubuntu's Go package
often lags behind the current release. A Go toolchain is just one
self-contained folder, so go.dev's recommended install is: download the
tarball, check its SHA-256 against the one go.dev publishes, unpack it into
`/usr/local/go`, and put it on `PATH`. Upgrading later is "delete the folder,
unpack the new one". We matched the Mac's version (1.27.4).

**GOROOT vs GOPATH.** `GOROOT` (`/usr/local/go`) is where Go *itself* lives:
compiler and standard library. `GOPATH` (`~/go`) is where Go keeps
downloaded modules and, in `~/go/bin`, binaries from `go install`. That's
why both `bin` folders went onto `PATH` in `~/.bashrc`. Since Go modules,
your own code does *not* need to live inside GOPATH.

**Gotcha: `sudo` doesn't work through Claude Code's `!` prefix.** `!`
runs commands without an interactive terminal, so sudo fails with "A
terminal is required to authenticate". Anything that asks for a password
has to run in a separate WSL terminal.

**Gotcha: a wrapped paste becomes two commands.** The long scratchpad path
wrapped onto a second line when pasted, so bash tried to *execute* the
tarball ("Permission denied"). The fix was to move the file to
`~/Downloads` so the command fits on one line.

**Deferred:** `golangci-lint` gets installed in Project 1, when linting
comes up on the roadmap.
