---
date: 2026-04-24
author: Alexander Towell (queelius)
status: design, awaiting user review
type: essay-design
---

# Design Spec: *Your Blog Will Outlive Your Database*

A plant-the-flag essay claiming the term **git-native publishing**, with an
embedded weekly jigsaw puzzle as the embodied argument.

## Identity

| Field | Value |
|---|---|
| **Working title** | *Your Blog Will Outlive Your Database (It Doesn't Have To)* |
| **Category being named** | git-native publishing |
| **Primitive being named** | commit-as-write |
| **Format** | Single essay, ~2,500 to 3,500 words |
| **Audience** | Tech-literate readers of metafunctor.com: programmers, indie-web folks, durability/local-first sympathizers |
| **Publication target** | metafunctor.com (Hugo); likely under `content/posts/` rather than as a series |
| **Goals (user-confirmed)** | (a) stake a claim / name the thing; (b) provoke discussion; (e) say a true thing about the web that's interesting |
| **Non-goals** | Recruit collaborators (d); document design space for personal reference (c); function as an implementation spec for the demo |

## Thesis (T2)

> Your reader's words evaporate while your writer's words endure. Markdown won
> the durability war by being boring. But every time we add interactivity, we
> drag back the database, and durability dies. Git is the missing symmetric
> write substrate, and its operational vocabulary is strictly richer than
> REST's.

Two coupled claims:

1. **Durability claim:** Reads on the open web are durable; writes are not.
   Closing the asymmetry requires a write substrate as durable as the read
   substrate. Git already is one.
2. **Vocabulary claim:** REST's CRUD verbs are a strict subset of git's
   operations. Once commits carry structured payloads in their messages,
   the commit log is a free, signed, replicated event store. No database
   required.

## Outline

### 0. Cold open: the puzzle (200 to 400 words)
- "There's a puzzle at the bottom of this page. Right now, N people are solving it."
- Establish stakes (every move is a commit, history will outlive the operator).
- Pivot: *"Now let me tell you why your forum threads from 2008 are gone."*

### 1. The asymmetry (300 to 500 words)
- 2008 blog post still renders. 2008 forum thread, gone.
- Markdown won the durability war by being boring.
- Every time we add interactivity, the database comes back, and durability dies.
- Name the asymmetry: **reads are durable; writes are not.**

### 2. Why this happened (300 to 400 words)
- The read path won (markdown, SSGs, CDN-cached HTML).
- The write path stayed in the 1995 mold: server with mutable state, owned by an operator who can disappear.
- Every Wordpress reincarnation (Ghost, Substack, Notion, Medium, Decap, Tina) reproduced the same architectural mistake.
- Even Jamstack: static frontend + SaaS backend = same failure mode, extra steps.

### 3. The missing primitive (300 to 400 words)
- We need a write substrate as durable as the read substrate.
- It's been sitting in `.git/` the whole time: append-only Merkle log, content-addressed, signed, fully replicated, forkable.
- Name the unit of change: **commit-as-write**.
- Name the category: **git-native publishing**, what you get when commit-as-write is your default.

### 4. Git's vocabulary is strictly richer than REST's *(headlined section, 400 to 600 words)*
- REST gives us GET/POST/PUT/PATCH/DELETE on resources.
- Git gives all of those, plus: **branch, tag, merge, fork, signed commit, submodule**. REST has no native equivalent for these.
- Include the comparison table from brainstorm (REST verb / Git op / what git adds; with empty-LHS rows for branch/tag/merge/fork/sig/submodule).
- Bridge to event sourcing and CQRS: commits are domain events; working tree is the projection; same log feeds many apps via different projections.
- The structured-commit move: commit message body as a typed payload (`op:`, `target:`, `actor:`, `ts:`). The log becomes a free event store. No schema layer.

### 5. The jigsaw, a worked example (400 to 500 words)
- Return to the puzzle from §0.
- Each piece-placement is a commit with a structured message: `op: place / piece: 042 / slot: [3,7] / actor: queelius`.
- **Validation:** pre-commit hook rejects wrong placements; the puzzle has a verifier (most multi-author systems can't validate writes).
- **Conflict scenario:** two readers grab piece 42 at once, first commit wins, second client retries (git's optimistic concurrency, free).
- **Why jigsaws specifically:** moves commute (CmRDT-shaped); participation is visceral; the *visible* assembly is the demo.
- **AI-generated images:** weekly fresh image (DALL-E / gpt-image), no reverse-search spoilers, sustained novelty.
- The solving history *is* the git log. Fork it, study it, every contributor is in there forever.

### 6. Honest limits (200 to 300 words)
- This isn't Twitter throughput. ~500 commits/week, not /second. **Substrate for participation, not for high-frequency mutable state.**
- GitHub dependency is contingent, not essential. Any git host works; even a local file via File System Access API.
- No fine-grained ACL: moderation is post-hoc (revert, rebase), not pre-hoc.
- Right-to-be-forgotten cuts against append-only history. Real tension, real cost. Name it, don't dodge it.
- The argument isn't "this beats everything"; it's "this is the durable substrate we've been missing."

### 7. The claim, and the invitation (150 to 300 words)
- Plant the flags: **git-native publishing**; **commit-as-write**.
- I'm not selling a product. I'm naming a category that doesn't have one and should.
- If you've already built something in this shape, tell me. I want to know.
- The puzzle is at `/jigsaw`. Place a piece. Your name will be in the commit log forever. So will mine.

## Key prose / craft decisions

- **Voice:** essayistic, not academic. First-person allowed. Connect to durability concerns shared with `the-long-echo` series and `longecho` project, but don't require those as prior reading.
- **Tables and code blocks are welcome.** The vocabulary table (§4) and one structured-commit example are load-bearing.
- **Diagrams:** none required for v1. The puzzle itself is the visual.
- **Length:** target 3,000 words. Compress §2 if blowing past 3,500.
- **Opening sentence is doing heavy work.** It gets a separate revision pass.

## Demo dependencies referenced (out of scope for *this* essay)

The essay assumes the jigsaw demo exists at `/jigsaw` by publication. The
demo's design and implementation are a **separate project** with its own
spec, plan, and build cycle. This essay is the *announcement and frame*;
the demo's spec covers piece-slicer, OAuth flow, commit format, validation
hook, Hugo template, AI image pipeline, and weekly-rotation cron.

If publication is desired before the demo ships, fall back to a short live
GitHub-OAuth demo (any commit-on-write toy) for §5. Flag in §0 if so.

## Risks

- **R1: overlap with prior coinages.** Possible existing uses of "git-native publishing." Pre-publication: literature search (Decap, Tina, "git-backed CMS," "local-first" canon, IPFS publishing, Beaker, Solid). If a near-equivalent exists, cite it and refine the claim.
- **R2: under-cooked limits section.** §6 has to be honest enough to disarm the obvious objections (rate limits, ACL, GDPR) without becoming a design doc. Watch length.
- **R3: vocabulary section gets too long.** §4 is the technical heart but can sprawl. Keep the table tight; resist temptation to enumerate every git op.
- **R4: the demo isn't ready by publication.** Mitigated by fallback above; ideally the demo lands first and §0 references real numbers.

## Out of scope

- The implementation of the jigsaw demo (separate project)
- The implementation of any reusable JS write-substrate library (Layer 0; not the MVP)
- A series of follow-up essays (may happen later; not committed here)
- Any business / monetization framing
