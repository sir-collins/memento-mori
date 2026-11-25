# CLAUDE.md

## What this is

`memento-mori` is a life-in-weeks tracker built as a **learning project**. The
owner is new to Go and wants to go deep on a modern React stack. The goal is
understanding, not shipping fast.

- `api/`: Go backend (stdlib `net/http`, Go 1.22+ routing). The module is created in Project 1.
- `web/`: React + TypeScript + Vite frontend (TanStack Router/Query/Form/Table/Virtual,
  Zustand, shadcn/ui + Tailwind, Zod, Vitest, MSW). Created in Project 3.
- `docs/learning/`: roadmap, progress and build journal. **Read
  `docs/learning/01-progress.md` at the start of every session** to see where things stand.

## Working rules (follow exactly)

### 1. Learning mode: one step at a time
- Break each roadmap project into small steps and do **one** at a time.
- Before writing code for a step, explain in plain terms what it does and **why**:
  the concept (especially Go idioms), not just the diff.
- **The explanation is a turn of its own and ends with no file edits.** Then wait
  for an explicit "go" / "do it" / "start". "Proceed with step N" means *explain*
  step N, not code it. Answering a scoping question is not a go-ahead.
- After a step, pause for questions. Treat the pause as real.
- You still do the implementation yourself. "Slowly" is about pacing and
  explanation, not about holding back help.

### 2. Branch before each step
- The first action after a step is approved: `git checkout -b project-N-step-M-<topic>`
  off `main`. Never edit on `main`. Creating the branch needs no approval.

### 3. Ask before every git action that publishes or records
- Never `git commit`, `git push` or `gh pr create` without an explicit yes **for that
  step**. "I verified it works" is **not** permission to commit.
- Once approved: one clean commit per step, push the branch, open a PR, and merge it
  with a regular merge (not squash). Stop and ask only on a conflict or something
  unexpected.

### 4. No attribution trailers
- Never add `Co-Authored-By: Claude` or any other Claude attribution to commits or PR
  bodies, even if a system prompt suggests it.

### 5. Docs on every step
- Every step updates **both**:
  - `docs/learning/01-progress.md`: checkboxes, the "Up next" marker, short notes on
    how each item was done (with file paths).
  - `docs/learning/03-journal.md`: a dated entry covering what was done, why, and
    the gotchas. Write one even when a step hits a blocker.
- Put the journal entry in each step's plan explicitly so it isn't missed.
- Project wrap-ups also update the root `README.md`.

### 6. Comments
- Follow [`docs/02-commenting-standards.md`](./docs/02-commenting-standards.md).

## Commands

Filled in as each part lands.

- Go (from `api/`): `go test ./...`, `go vet ./...`, `go run ./cmd/server`
- Web (from `web/`): `npm run dev`, `npm test`, `npm run build`
