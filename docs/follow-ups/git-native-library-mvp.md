---
date: 2026-04-24
author: Alexander Towell (queelius)
status: brainstorm seed (NOT IMPLEMENTED)
type: follow-up
---

# Follow-up: git-native library MVP

Captured during the *Your Blog Will Outlive Your Database* essay drafting.
This is a brainstorm seed for a future conversation, not a plan or spec.
The library is intentionally out of scope for the current essay-drafting
work; the current work finishes the essay first.

## Goal

Build the library that powers the essay's jigsaw demo at `/arcade/jigsaw` on
metafunctor.com, and make it reusable by the author for adding
participation features to a Hugo blog over time.

## Single confirmed user

queelius (Alex Towell, metafunctor.com). Other adopters welcome later, but
the design serves him first. "No one would use it" was the prior worry; one
real user collapses that calculus.

## Scope (MVP)

Vertical slice: build the jigsaw demo end-to-end. The substrate library
falls out of it organically as the demo stabilizes.

In the MVP:
- Browser-side TypeScript library (the runtime is the browser, so JS/TS is
  the obvious choice; WASM is a possibility later if a non-JS lang is
  needed in-browser, but JS/TS keeps the build chain simple)
- GitHub OAuth flow (browser-based; PKCE flow if available)
- Commit-on-place via the GitHub commit API
- Validation hook (pre-commit check that the puzzle move is correct
  against the source image)
- Conflict handling (two readers grab the same piece, second client retries)
- Hugo template / shortcode for embedding the jigsaw at `/arcade/jigsaw`
- AI image generation pipeline (weekly fresh image, generated server-side
  on a cron)
- Counter rendering: the "47 people" number in the essay's opening reads
  from `git log --since="last Monday 00:00 UTC" --format='%an' | sort -u
  | wc -l` (cumulative-this-week, monotonic, never zero after first
  contributor)

Out of MVP scope:
- Multiple git hosts (GitHub only at first; GitLab and Gitea later)
- Multiple widget types (jigsaw only at first; comments, reactions later)
- Local-file backend via the File System Access API (deferred)
- Fine-grained ACL (post-hoc moderation only)
- Right-to-be-forgotten tooling (acknowledged structural cost; deferred)

## Architecture: protocol + clients

The library is two layers, conceptually:

1. **The protocol.** Structured-commit message format, OAuth flow,
   validation contract, host API mapping. Language-agnostic. This is the
   durable artifact.
2. **The clients.** TypeScript (primary, browser, user-facing) and Python
   (secondary, scripting and automation). Both produce and consume the
   same protocol.

The TypeScript client is what the blog embeds. The Python client is for
tasks the author does outside the browser: seeding a new puzzle, harvesting
commit data for analysis, running the AI image generation cron, or batch
operations.

Future clients (Go, Rust, shell) are straightforward once the protocol is
written down.

## Repos

Three candidates for repo organization, to decide in the future brainstorm:

1. **Single TS repo.** `github.com/queelius/git-native` (TypeScript only at
   first; Python added later as a second package or a separate repo).
2. **Two repos with mirrored APIs.** `git-native` (TypeScript) and
   `git-native-py` (Python). Independent release cadences, simpler tooling
   per repo.
3. **Monorepo with language subdirectories.** `git-native/{ts,py}/` inside
   one repo. Coordinated releases, but mixed-language tooling.

Recommendation for the future brainstorm: option 2 (two repos), unless the
protocol is changing fast enough that monorepo coordination is worth it.

The jigsaw demo lives in its own repo: `github.com/queelius/git-jigsaw`.
It depends on `git-native` (TypeScript).

## Distribution

- TypeScript: npm package, name `git-native` (check availability before
  committing)
- Python: PyPI package, name to be decided (`git-native` may collide on
  PyPI; alternative is `commit-as-write` or `git-native-py`)

## License

MIT. (Default for queelius's published packages.)

## Essay relationship

The essay (this repo's `drafts/essay.md`) does NOT depend on the library
existing at publish time. The §7 closer optionally points to the library
repo as a credibility signal, but the essay stands on its own as the
category-naming artifact.

The jigsaw demo at `/arcade/jigsaw` does depend on the library being functional
by the time the demo is publicly linked. If the demo is not ready by essay
publish, §0 falls back to a more abstract opening (per the essay spec's
fallback note).

## Open questions for the future brainstorm

- Repo organization (above).
- Name collisions on npm and PyPI; pick before public push.
- Which OAuth flow specifically (GitHub Apps with PKCE for purely
  browser-side use; or a tiny serverless function to hold the client
  secret).
- How does the validation hook know what is correct? The source image
  lives in the puzzle repo; the hook references it. Mechanism details to
  decide.
- Conflict UX: silent retry on the client, or surface the conflict to the
  user with a "you were beaten to that piece" message.
- Identity beyond GitHub (deferred but worth noting; OIDC providers,
  domain-bound identities, etc.).
- How granular is the protocol versioning. The structured-commit message
  format will evolve.

## Companion project: git-native-fastapi

A FastAPI server that wraps git as a REST API. Goal: provide standard
REST-style backends for various projects on the blog, with GitHub as the
storage substrate.

Why: many tools, libraries, and external integrations expect a REST
surface. The FastAPI adapter translates HTTP verbs to git operations
using the §4 mapping from the essay (POST becomes a commit creating a new
file, GET reads from the working tree, PATCH commits a partial diff,
DELETE commits a removal or revert, and so on). This demonstrates that
you can have a conventional REST surface AND a git-native backend at the
same time. It also makes the essay's vocabulary table *operational*: a
reader can see the abstract mapping running live.

Scope (rough):
- A small FastAPI app exposing CRUD over a configured git repository
- Endpoint handlers translate to commit / read operations
- Optional pluggable validation hooks per endpoint
- Auth: GitHub OAuth pass-through, or service-account commits via a token
- Read endpoints can serve from a built static cache for speed

Where it lives: separate repo, `github.com/queelius/git-native-fastapi`
(or `gnp-rest`, name to be picked).

Relationship to the TS / Python clients: the FastAPI app is itself a
client of the protocol (it uses the same commit format). Other apps and
external services can consume the FastAPI endpoints if they prefer REST
over committing directly.

The FastAPI adapter is partly demonstrative (it shows the essay's
vocabulary mapping at work) and partly practical (it gives the blog a
standard REST surface for projects that need one).

## Companion vision: arcade with multiple games

The jigsaw is the first git-native game on metafunctor.com. The author
plans more (checkers, async word puzzles, collaborative cipher cracking,
etc.). Existing repos at `~/github/beta/arcade-lobby/` and
`~/github/beta/arcade-grid/` may already contain relevant prior work
worth reviewing when this brainstorm begins.

The arcade has three substrates, picked per-game for what each does well:

| Layer | Tech | Examples |
|---|---|---|
| Async game state | git-native (this library) | Jigsaw; async word puzzles; collaborative cipher cracking; anything where moves commute and don't need millisecond latency |
| Real-time game state | WebRTC peer-to-peer or WebSocket | Checkers (when played live); anything where players need each other's moves immediately |
| Lobby and chat | WebRTC data channels or thin WebSocket service; lobby state itself can be git-native | Presence, game discovery, ambient chat alongside play |

This layered approach is consistent with the essay's §6 limits:
git-native publishing is the substrate for participation, not for
high-frequency state. Real-time games and chat live on substrates picked
for those needs.

URL structure: `/arcade/` is the multi-game hub. Individual games live
at `/arcade/jigsaw`, `/arcade/checkers`, etc. The essay's canonical URL
for the jigsaw demo is `/arcade/jigsaw` (committed at publication time).

The arcade itself is a separate project. The git-native library
described in the rest of this doc powers the async-game-state layer; the
lobby and real-time-game layers are different projects with different
brainstorms.

## App organization within a repo (vocabulary constraint)

When deploying multiple git-native apps on a single blog (jigsaw,
comments, reactions, etc.), the question is how to organize their data.

Option A: **one repo per app.** Each app owns its own repo
(`github.com/queelius/jigsaw-data`, `.../comments-data`, etc.). Maximum
isolation; easy to fork or back up individually; straightforward auth
scoping per app.

Option B: **one repo per blog**, with apps as subdirectories
(`github.com/queelius/metafunctor-data/{jigsaw,comments,reactions}/`).
Single auth scope, single backup, all blog data in one place.

**Vocabulary constraint:** apps must NOT be namespaced by git branches.
The essay's §4 table commits "branch" to mean *parallel / private /
proposed state*. Using branches to mean "the comments app's data"
overloads the term and quietly contradicts the essay's argument. Apps
are paths, not branches.

**Recommended:** Option B (one repo per blog, subdirectories per app).
Reasons:

- Operationally simpler (one repo to manage, one auth flow per blog)
- Path-based naming integrates cleanly with the structured-commit
  protocol (the `target:` field already takes a path)
- Branches stay reserved for their git-semantic meaning (the FastAPI
  adapter can offer a real branch-as-draft endpoint if desired)
- Future cross-app interactions (a stats dashboard reading from multiple
  app paths) become trivial

The library should make Option B the default but support Option A by
configuration (point the client at a specific repo per app instance).

## Library bootstrap on an existing repo

The library should be capable of constructing the backend on an existing
GitHub repository, not just a fresh one. Concretely:

- Given a repo URL and an app path, the library creates the directory
  structure if absent, writes a config marker (`/{app}/.gnp-config.json`
  or similar), and is ready to accept commits.
- Existing repo content is undisturbed.
- Multiple apps can be bootstrapped into the same repo by calling the
  setup flow with different app paths.

This means the user can point git-native at their existing
`metafunctor.com` Hugo content repo and add a `/jigsaw/` subdirectory
without creating a new repo or migrating anything.

## Why this is captured here

The essay-drafting conversation surfaced the library decisions in real
time. The intent is captured here so a future conversation can pick it up
without losing context. The library project is its own brainstorm, plan,
and build cycle; that work happens in `~/github/repos/git-native/` (or
similar), in a separate session, after the essay ships. The FastAPI
adapter is a separate project after that.
