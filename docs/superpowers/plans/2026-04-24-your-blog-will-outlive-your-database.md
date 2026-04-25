# *Your Blog Will Outlive Your Database* Drafting Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Draft, revise, and prepare for publication the plant-the-flag essay specified in `docs/superpowers/specs/2026-04-24-git-native-publishing-essay-design.md`.

**Architecture:** Single-file markdown drafting in `drafts/essay.md` against a section skeleton. Supporting artifacts (REST/git comparison table, structured-commit examples) built once in `drafts/scratch.md` and dropped into the relevant sections. Soul voice check at the file-write boundary catches em-dashes and AI tells. Final draft moves to `~/github/repos/metafunctor/content/posts/`.

**Tech Stack:** Markdown, Hugo (publication target), soul plugin's `check-banned-phrases.sh` hook (voice gate), `wc -w` for length checks.

---

## File structure

| Path | Purpose |
|---|---|
| `drafts/scaffolding.md` | Section skeleton with headings, bullet outlines from spec, length budgets. Read-only reference. |
| `drafts/scratch.md` | Workspace for the comparison table, structured-commit examples, candidate opening lines. |
| `drafts/essay.md` | The single-file growing draft. This is what gets published. |
| `drafts/notes.md` | Process notes, prior-art scan results, things to fix in revision. |
| `~/github/repos/metafunctor/content/posts/2026-XX-XX-your-blog-will-outlive-your-database.md` | Final destination for publication. |

## Voice constraint (applies to every drafting step)

The soul plugin's `check-banned-phrases.sh` hook fires on PostToolUse for Write and blocks the save if it detects banned phrases. The hook is the authoritative voice check. The two most common categories it flags are: (1) the long horizontal dash punctuation (use commas, periods, colons, semicolons, or parentheses instead); (2) common AI-prose tells. Consult the soul plugin's `SKILL.md` for the current list. Attempting to save with a banned phrase will surface the specific term in the error message; rewrite the flagged passage and re-save.

---

## Task list

### Task 1: Scaffold the drafting workspace

**Files:**
- Create: `drafts/scaffolding.md`
- Create: `drafts/scratch.md`
- Create: `drafts/essay.md`
- Create: `drafts/notes.md`

- [ ] **Step 1: Create the drafts directory.**

```bash
mkdir -p drafts
```

- [ ] **Step 2: Create `drafts/scaffolding.md` by copying the spec's "Outline" section verbatim.** This becomes the read-only reference for what each section must contain. Do not draft prose into this file.

- [ ] **Step 3: Create `drafts/scratch.md` with three top-level headings.**

```markdown
# Scratch

## Comparison table (REST vs git) for §4

(table goes here, built in Task 2)

## Structured-commit examples for §4 and §5

(examples go here, built in Task 3)

## Candidate opening lines for §0

(brainstormed in Task 13)
```

- [ ] **Step 4: Create `drafts/essay.md` with just the working title and seven section headings.** No prose yet.

```markdown
# Your Blog Will Outlive Your Database

(it doesn't have to)

## 0. (cold open)

## 1. The asymmetry

## 2. Why this happened

## 3. The missing primitive

## 4. Git's vocabulary is strictly richer than REST's

## 5. The jigsaw, a worked example

## 6. Honest limits

## 7. The claim, and the invitation
```

- [ ] **Step 5: Create empty `drafts/notes.md`.**

- [ ] **Step 6: Commit.**

```bash
git add drafts/
git commit -m "Scaffold drafting workspace for essay"
```

---

### Task 2: Build the REST-vs-git comparison table for §4

**Files:**
- Modify: `drafts/scratch.md`

The spec calls this the "load-bearing artifact" of §4. Build it once here; it gets dropped into §4 in Task 9.

- [ ] **Step 1: Draft the 11-row table in `drafts/scratch.md` under "Comparison table".** Three columns: REST/DB verb | Git operation | What git adds. Use `(none)` in the LHS column for git ops with no REST equivalent.

```markdown
| REST/DB verb | Git operation | What git adds that REST/SQL can't |
|---|---|---|
| `POST` (create) | `commit` (new file) | signed, time-stamped, cryptographically attributed |
| `PUT` (replace) | `commit` (overwrite) | prior versions preserved automatically |
| `PATCH` (partial) | `commit` (line-level diff) | the diff *is* the structured patch, no separate schema |
| `DELETE` | `commit` (remove) or `revert` | reversible; deletion is a record, not an erasure |
| `GET` | read working tree | or read any historical state, by hash |
| `(none)` | `branch` | parallel / private / proposed state, native |
| `(none)` | `tag` | named / canonical / published version |
| `(none)` | `merge` | consensus and reconciliation as first-class ops |
| `(none)` | `fork` | take all your data and leave, lossless |
| `(none)` | signed commit | authentication baked into the data layer |
| `(none)` | `submodule` | composable embedded references across repos |
```

- [ ] **Step 2: Read the table aloud.** The cumulative argument is that REST is a strict subset. Each row in the rightmost column should make a sharp point. If a row reads as filler, drop it. Six strong rows beats eleven mixed.

- [ ] **Step 3: Verify no em-dashes in the table.** Use parentheses or comma constructions only.

- [ ] **Step 4: Commit.**

```bash
git add drafts/scratch.md
git commit -m "Build REST-vs-git comparison table for §4"
```

---

### Task 3: Build the structured-commit examples for §4 and §5

**Files:**
- Modify: `drafts/scratch.md`

Two example commit messages with the same shape (a typed payload), one generic for §4 and one jigsaw-specific for §5. Same field structure twice ties the sections together visually.

- [ ] **Step 1: Draft the §4 generic example in scratch.md.**

```
op: react
target: posts/your-blog-will-outlive-your-database
value: 🔥
actor: queelius
ts: 2026-04-24T22:45:00Z
```

- [ ] **Step 2: Draft the §5 jigsaw example.**

```
op: place
piece: 042
slot: [3, 7]
actor: queelius
ts: 2026-04-24T22:47:13Z
```

- [ ] **Step 3: Verify both are concrete (real-looking values, not `FOO BAR`).** Concrete examples carry the argument; abstract ones don't.

- [ ] **Step 4: Commit.**

```bash
git add drafts/scratch.md
git commit -m "Build structured-commit examples for §4 and §5"
```

---

### Task 4: Prior-art scan (mitigates spec risk R1)

**Files:**
- Modify: `drafts/notes.md`

R1 in the spec is that "git-native publishing" may already be coined. Spend ~20 minutes searching to confirm or refute. If a near-equivalent exists, the essay cites and refines rather than ignoring.

- [ ] **Step 1: Web-search the exact phrases.** Record top hits in `drafts/notes.md` under "Prior art scan":
  - `"git-native publishing"`
  - `"git-based publishing"`
  - `"git as a CMS"`
  - `"commit-as-write"`
  - `"git-backed comments"`

- [ ] **Step 2: Search for adjacent canon.** Note what's been said and by whom:
  - "local-first software" (Ink & Switch, 2019)
  - Decap CMS, TinaCMS, Forestry
  - Utterances, Giscus
  - Solid (Berners-Lee), Remote Storage
  - IPFS publishing, Beaker Browser, Hyper

- [ ] **Step 3: If a near-equivalent of the claim exists, do not pivot the essay.** Plan to cite it in §3 ("X said Y; here's what's still missing") and refine the claim. Add a citation note in `notes.md` with the URL.

- [ ] **Step 4: Commit.**

```bash
git add drafts/notes.md
git commit -m "Prior-art scan for git-native publishing claim"
```

---

### Task 5: Draft §0 (cold open, the puzzle)

**Files:**
- Modify: `drafts/essay.md` §0

**Spec reference:** Outline §0, target 200 to 400 words.

**Must land:**
1. There is a puzzle on this page right now.
2. Every move in that puzzle is a git commit.
3. The puzzle's history will outlive the operator.
4. Pivot at the end: "now let me tell you why your forum threads from 2008 are gone."

**Voice notes:** Most sensory and emotional section in the essay. Earn the reader's attention with a concrete number (pick one: 12, 47, 73). The pivot sentence is the hinge into §1; sharpen it. If the demo isn't ready by publication, fall back to the alternative §0 in the spec.

- [ ] **Step 1: Re-read spec §0 and §1.** §0 should prime the asymmetry framing in §1.

- [ ] **Step 2: Draft 200 to 400 words into `drafts/essay.md` under "0. (cold open)".** Lead with the puzzle. Pivot at the end.

- [ ] **Step 3: Word count check.**

```bash
awk '/^## 0\./{flag=1;next} /^## 1\./{flag=0} flag' drafts/essay.md | wc -w
```

Expected: 200 to 400. If outside, revise.

- [ ] **Step 4: Voice scan.** Read aloud. The soul hook will run on the next save and flag any banned phrase in its error message. If you want to pre-check, save the file first as a no-op edit and watch the hook output. Rewrite anything flagged.

- [ ] **Step 5: Commit.**

```bash
git add drafts/essay.md
git commit -m "Draft §0 cold open"
```

---

### Task 6: Draft §1 (the asymmetry)

**Files:**
- Modify: `drafts/essay.md` §1

**Spec reference:** Outline §1, target 300 to 500 words.

**Must land:**
1. 2008 blog post still renders; 2008 forum thread is gone.
2. Markdown won the durability war by being boring.
3. Adding interactivity drags the database back, and durability dies with it.
4. Name the asymmetry: "reads are durable; writes are not."

**Voice notes:** Direct, slightly sad. Resist hand-wraving generalities. Use one or two concrete examples (a specific 2008-era forum, a specific blog still alive). The naming sentence is bold; let it stand on its own line.

- [ ] **Step 1: Re-read spec §1 and §2** (so §1 ends in a way that lets §2 pick up the diagnosis).

- [ ] **Step 2: Draft 300 to 500 words into §1.**

- [ ] **Step 3: Word count check.**

```bash
awk '/^## 1\./{flag=1;next} /^## 2\./{flag=0} flag' drafts/essay.md | wc -w
```

Expected: 300 to 500.

- [ ] **Step 4: Voice scan.** Same `grep` from Task 5.

- [ ] **Step 5: Commit.**

```bash
git add drafts/essay.md
git commit -m "Draft §1 the asymmetry"
```

---

### Task 7: Draft §2 (why this happened)

**Files:**
- Modify: `drafts/essay.md` §2

**Spec reference:** Outline §2, target 300 to 400 words.

**Must land:**
1. The read path won (markdown, SSGs, CDN-cached HTML).
2. The write path stayed in the 1995 mold (server with mutable state, owned operator).
3. Every Wordpress reincarnation (Ghost, Substack, Notion, Medium, Decap, Tina) reproduced the same architectural mistake.
4. Even Jamstack: static frontend + SaaS backend = same failure mode, extra steps.

**Voice notes:** Sharper edge here. This is the paragraph the Hacker News critics will quote. Don't punch down at any specific product; the point is the *shape* they all share.

- [ ] **Step 1: Re-read spec §2.**

- [ ] **Step 2: Draft 300 to 400 words into §2.**

- [ ] **Step 3: Word count check.**

```bash
awk '/^## 2\./{flag=1;next} /^## 3\./{flag=0} flag' drafts/essay.md | wc -w
```

Expected: 300 to 400.

- [ ] **Step 4: Voice scan.** Same `grep`.

- [ ] **Step 5: Commit.**

```bash
git add drafts/essay.md
git commit -m "Draft §2 why this happened"
```

---

### Task 8: Draft §3 (the missing primitive)

**Files:**
- Modify: `drafts/essay.md` §3

**Spec reference:** Outline §3, target 300 to 400 words.

**Must land:**
1. We need a write substrate as durable as the read substrate.
2. It's been sitting in `.git/` the whole time: append-only Merkle log, content-addressed, signed, fully replicated, forkable.
3. Plant the primitive: **commit-as-write** (the unit of change is a git commit, not a SQL row).
4. Plant the category: **git-native publishing** is what you get when commit-as-write is your default.

**Voice notes:** This is the *naming* moment of the essay. Bold both terms when first introduced. If the prior-art scan from Task 4 turned up close cousins, cite them here in one sentence and explain the refinement.

- [ ] **Step 1: Re-read spec §3 and the prior-art notes from Task 4.**

- [ ] **Step 2: Draft 300 to 400 words into §3.** Boldface `**commit-as-write**` and `**git-native publishing**` on first introduction.

- [ ] **Step 3: Word count check.**

```bash
awk '/^## 3\./{flag=1;next} /^## 4\./{flag=0} flag' drafts/essay.md | wc -w
```

Expected: 300 to 400.

- [ ] **Step 4: Voice scan.** Same `grep`.

- [ ] **Step 5: Commit.**

```bash
git add drafts/essay.md
git commit -m "Draft §3 the missing primitive"
```

---

### Task 9: Draft §4 (git's vocabulary is strictly richer than REST's, headlined section)

**Files:**
- Modify: `drafts/essay.md` §4
- Read: `drafts/scratch.md` (table from Task 2 and example from Task 3)

**Spec reference:** Outline §4, target 400 to 600 words. This is the technical heart of the essay.

**Must land:**
1. REST gives us GET/POST/PUT/PATCH/DELETE on resources.
2. Git gives all of those plus branch, tag, merge, fork, signed commit, submodule. REST has no native equivalent.
3. Drop in the comparison table from `drafts/scratch.md`.
4. Bridge to event sourcing and CQRS: commits are domain events, working tree is the projection, same log feeds many apps.
5. The structured-commit move: drop in the §4 generic example from `drafts/scratch.md`. The log becomes a free event store. No schema layer.

**Voice notes:** Most technical section. Show, don't claim. The table does heavy lifting; the surrounding prose should set it up and unpack it, not duplicate it. The structured-commit example needs one sentence of context before and one after.

- [ ] **Step 1: Re-read spec §4 and the table/example in scratch.md.**

- [ ] **Step 2: Draft 400 to 600 words into §4.** Pull the table and the example from `drafts/scratch.md`. Write the framing prose around them.

- [ ] **Step 3: Word count check** (excluding the table itself, since tables inflate word counts misleadingly).

```bash
awk '/^## 4\./{flag=1;next} /^## 5\./{flag=0} flag' drafts/essay.md | grep -v "^|" | wc -w
```

Expected: 400 to 600 in prose (the table is on top of that).

- [ ] **Step 4: Voice scan.** Save and let the soul hook run. Technical sections are most prone to AI tells; rewrite anything the hook flags and re-save until it's silent.

- [ ] **Step 5: Verify the table renders cleanly.** Check the markdown table syntax.

- [ ] **Step 6: Commit.**

```bash
git add drafts/essay.md
git commit -m "Draft §4 git's vocabulary is strictly richer"
```

---

### Task 10: Draft §5 (the jigsaw, a worked example)

**Files:**
- Modify: `drafts/essay.md` §5
- Read: `drafts/scratch.md` (jigsaw example from Task 3)

**Spec reference:** Outline §5, target 400 to 500 words.

**Must land:**
1. Return to the puzzle from §0 (callback closes the frame).
2. Each piece-placement is a commit with a structured message. Drop in the §5 example from `drafts/scratch.md`.
3. Validation: pre-commit hook rejects wrong placements (the puzzle has a verifier; most multi-author systems can't validate writes).
4. Conflict scenario: two readers grab piece 42 at once, first commit wins, second client retries (git's optimistic concurrency, free).
5. Why jigsaws specifically: moves commute (CmRDT-shaped); participation is visceral; the visible assembly is the demo.
6. AI-generated images: weekly fresh image, no reverse-search spoilers, sustained novelty.
7. The solving history *is* the git log. Fork it, study it, every contributor is in there forever.

**Voice notes:** This is where the essay re-grounds in the concrete. After the abstract §4, §5 should feel like coming home. Use the same "op:/target:/actor:" shape from §4 so the reader sees the structural rhyme.

- [ ] **Step 1: Re-read spec §5 and the jigsaw example in scratch.md.**

- [ ] **Step 2: Draft 400 to 500 words into §5.** Pull the example from `drafts/scratch.md`.

- [ ] **Step 3: Word count check.**

```bash
awk '/^## 5\./{flag=1;next} /^## 6\./{flag=0} flag' drafts/essay.md | wc -w
```

Expected: 400 to 500.

- [ ] **Step 4: Voice scan.** Same `grep`.

- [ ] **Step 5: Commit.**

```bash
git add drafts/essay.md
git commit -m "Draft §5 the jigsaw worked example"
```

---

### Task 11: Draft §6 (honest limits)

**Files:**
- Modify: `drafts/essay.md` §6

**Spec reference:** Outline §6, target 200 to 300 words.

**Must land:**
1. Not Twitter throughput. ~500 commits/week, not /second. Substrate for *participation*, not high-frequency mutable state.
2. GitHub dependency is contingent, not essential. Any git host works; even local file via File System Access API.
3. No fine-grained ACL: moderation is post-hoc (revert, rebase), not pre-hoc.
4. Right-to-be-forgotten cuts against append-only history. Real tension, real cost. Name it; don't dodge it.
5. The argument isn't "this beats everything"; it's "this is the durable substrate we've been missing."

**Voice notes:** Sober and direct. This section is the essay's credibility gate: if it doesn't pre-empt the obvious objections, the comments section will. Each limit gets one or two crisp sentences. No throat-clearing.

- [ ] **Step 1: Re-read spec §6.**

- [ ] **Step 2: Draft 200 to 300 words into §6.**

- [ ] **Step 3: Word count check.**

```bash
awk '/^## 6\./{flag=1;next} /^## 7\./{flag=0} flag' drafts/essay.md | wc -w
```

Expected: 200 to 300.

- [ ] **Step 4: Voice scan.** Same `grep`.

- [ ] **Step 5: Commit.**

```bash
git add drafts/essay.md
git commit -m "Draft §6 honest limits"
```

---

### Task 12: Draft §7 (the claim, and the invitation)

**Files:**
- Modify: `drafts/essay.md` §7

**Spec reference:** Outline §7, target 150 to 300 words.

**Must land:**
1. Plant the flags: **git-native publishing**; **commit-as-write**.
2. Not selling a product. Naming a category that doesn't have one and should.
3. If you've already built something in this shape, tell me. I want to know.
4. The puzzle is at `/jigsaw`. Place a piece. Your name will be in the commit log forever. So will mine.
5. (One-sentence self-referential note: this essay's source markdown is in git too; the whole argument is demonstrated by the artifact.)

**Voice notes:** Short, direct, slightly intimate. The closing line should resonate. The self-referential note is optional but adds weight; cut if it feels forced.

- [ ] **Step 1: Re-read spec §7 and §0 (the closing should rhyme with the opening).**

- [ ] **Step 2: Draft 150 to 300 words into §7.**

- [ ] **Step 3: Word count check.**

```bash
awk '/^## 7\./{flag=1} flag' drafts/essay.md | wc -w
```

Expected: 150 to 300.

- [ ] **Step 4: Voice scan.** Same `grep`.

- [ ] **Step 5: Commit.**

```bash
git add drafts/essay.md
git commit -m "Draft §7 the claim and the invitation"
```

---

### Task 13: Title and opening sentence revision pass

**Files:**
- Modify: `drafts/essay.md` (title and §0 opening)
- Modify: `drafts/scratch.md` (candidate-line workspace)

The spec flags the opening sentence as "doing heavy work, gets a separate revision pass." The working title may also benefit from one more pass.

- [ ] **Step 1: In `drafts/scratch.md` under "Candidate opening lines for §0", brainstorm 5 to 7 alternative opening sentences.** Write each as a complete sentence. Vary the entry point: question, scene, claim, anecdote, paradox.

- [ ] **Step 2: For each candidate, ask three questions in your head: does it earn the next sentence? does it sound like me? does it set up the asymmetry without spoiling it?** Score one to three on each. Pick the highest combined.

- [ ] **Step 3: Replace the existing opening sentence in `drafts/essay.md` §0 with the chosen line.**

- [ ] **Step 4: Brainstorm 3 to 5 working-title variants in scratch.md.** Current default: *Your Blog Will Outlive Your Database (It Doesn't Have To)*. Variants might compress, sharpen, or invert. Pick one. Update the title in `drafts/essay.md`.

- [ ] **Step 5: Commit.**

```bash
git add drafts/essay.md drafts/scratch.md
git commit -m "Revise opening sentence and title"
```

---

### Task 14: Full read-through, cohesion, and length sweep

**Files:**
- Modify: `drafts/essay.md` (cohesion edits across sections)

The whole essay now exists. Read it end to end as a reader would.

- [ ] **Step 1: Read `drafts/essay.md` straight through, no skipping.** Note transitions that feel rough, sentences that contradict an earlier claim, places where you say the same thing twice.

- [ ] **Step 2: Fix the transitions.** §0 to §1 is the most important (the "now let me tell you" pivot). §4 to §5 is the second-most important (the abstract-to-concrete return).

- [ ] **Step 3: Total word count.**

```bash
wc -w drafts/essay.md
```

Expected: 2,500 to 3,500. If over 3,500, the spec's compress-target is §2 (why this happened). If under 2,500, the most under-served section is usually §4 (vocabulary); add depth there.

- [ ] **Step 4: Voice scan over the full file.** Save the essay and let the soul hook run on the entire file. If the hook flags any phrase, rewrite that passage and re-save until the hook is silent.

- [ ] **Step 5: Verify all section bullets from the spec are landed.** Open the spec side-by-side with the essay. For each "Must land" bullet in the outline, find the sentence(s) in the essay that hit it. Note any gaps in `drafts/notes.md`.

- [ ] **Step 6: Fix any gaps from Step 5.**

- [ ] **Step 7: Commit.**

```bash
git add drafts/essay.md drafts/notes.md
git commit -m "Cohesion pass and length sweep"
```

---

### Task 15: User review gate

**Files:** none

The draft is complete. Hand it to the user before any move toward publication.

- [ ] **Step 1: Print the draft path and total word count.** Tell the user the draft is ready for their read.

- [ ] **Step 2: Wait for user response.** If they request changes, loop back to whichever section task is implicated and re-run that task's steps. If they approve, proceed to Task 16.

---

### Task 16: Move to metafunctor and prepare for publication

**Files:**
- Create: `~/github/repos/metafunctor/content/posts/2026-XX-XX-your-blog-will-outlive-your-database.md`

The essay lives in two places at publication: this repo (the design and drafting history) and the metafunctor repo (the published post). The metafunctor copy gets Hugo frontmatter.

- [ ] **Step 1: Decide the publication date.** Update YYYY-MM-DD in the filename and in the frontmatter `date` field.

- [ ] **Step 2: Create the post file in metafunctor with Hugo frontmatter.**

```yaml
---
title: "Your Blog Will Outlive Your Database"
subtitle: "(It Doesn't Have To)"
date: 2026-XX-XX
author: "Alexander Towell"
tags: ["git-native-publishing", "local-first", "static-sites", "durability"]
canonical_url: "https://metafunctor.com/posts/your-blog-will-outlive-your-database/"
description: "Your reader's words evaporate while your writer's words endure. There's a missing primitive: writes that are as durable as the reads. Git is that primitive, and it's been sitting in plain sight."
draft: true
---

(paste essay body here)
```

- [ ] **Step 3: Paste the body of `drafts/essay.md` (everything after the title) into the new metafunctor file.**

- [ ] **Step 4: Build the metafunctor site locally and view the post in a browser.** Confirm the table renders, the structured-commit examples render, no broken markdown.

```bash
cd ~/github/repos/metafunctor
hugo serve -D
```

Open the local URL for the post in a browser. Verify visually.

- [ ] **Step 5: Add a backlink in this repo's `drafts/essay.md`** noting the published location and date. This keeps the design repo self-aware about where the essay went.

- [ ] **Step 6: Commit in both repos.** In persist:

```bash
git add drafts/essay.md
git commit -m "Mark essay as published; backlink to metafunctor"
```

In metafunctor (separate repo, separate commit):

```bash
cd ~/github/repos/metafunctor
git add content/posts/2026-XX-XX-your-blog-will-outlive-your-database.md
git commit -m "Add essay: Your Blog Will Outlive Your Database"
```

- [ ] **Step 7: Flip `draft: false` in the metafunctor frontmatter when ready to publish.** Ask the user before doing this. Then push metafunctor.

---

### Task 17 (optional): Cross-post setup via crier

**Files:** none in this repo

If cross-posting to dev.to, Hashnode, Bluesky, Mastodon (per the user's `crier` workflow):

- [ ] **Step 1: Confirm with the user which platforms to cross-post to.**

- [ ] **Step 2: For each platform, use the crier MCP tools** (`crier_publish` with two-step confirmation) to schedule or execute the cross-post. Short-form platforms (Bluesky, Mastodon) need a rewrite; ask the user if they want you to draft those, or if they'll handle them.

- [ ] **Step 3: Verify the canonical URL on each platform points back to metafunctor.**

- [ ] **Step 4: Update `drafts/notes.md` in this repo with the cross-post log** (platform, date, URL).

```bash
git add drafts/notes.md
git commit -m "Log cross-posts"
```

---

## Self-review

I checked the plan against the spec:

**1. Spec coverage:** Every section in the spec's Outline (§0 through §7) has a dedicated drafting task (Tasks 5-12). The two load-bearing artifacts (comparison table, structured-commit examples) have their own tasks (Tasks 2 and 3). Risk R1 (prior-art) has a task (Task 4). The "key prose / craft decisions" (voice, length, opening sentence revision pass) are addressed in Tasks 13 and 14. Demo dependency is correctly marked out of scope; Task 5 notes the fallback to a non-jigsaw demo if needed. Publication path covered in Task 16.

**2. Placeholder scan:** No "TBD", no "fill in details", no "similar to Task N". Each section task spells out the specific bullets that must land, the length budget, and the voice notes. Word count and voice grep commands are concrete.

**3. Type consistency:** Section numbering (§0 through §7) is consistent across all tasks. The two artifacts in scratch.md (table, examples) are referenced consistently in Tasks 9 and 10. File paths match throughout.

**4. Ambiguity:** Task 5 has a known fallback (non-jigsaw demo if jigsaw isn't ready) which is intentional contingency, not ambiguity. Task 16 frontmatter assumes a slug pattern that the user can adjust.

No issues to fix.
