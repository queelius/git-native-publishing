# Scratch

## Comparison table (REST vs git) for §4

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

## Structured-commit examples for §4 and §5

**§4 generic example:**

```
op: react
target: posts/your-blog-will-outlive-your-database
value: 🔥
actor: queelius
ts: 2026-04-24T22:45:00Z
```

**§5 jigsaw example:**

```
op: place
piece: 042
slot: [3, 7]
actor: queelius
ts: 2026-04-24T22:47:13Z
```

## Candidate opening lines for §0

(brainstormed in Task 13)

---

## Title and opening alternates (Task 13)

### Opening sentence candidates

The current §0 opening is: *"Scroll to the bottom of this page."* (followed by: *"There's a jigsaw puzzle there, and right now 47 people are working on it with you."*)

The opening sentence must pull the reader forward into the puzzle scene, not spoil the asymmetry (reads durable / writes not) that §1 reveals, and sound like a person writing, not a product page.

---

**Option 1 (Scene, direct second-person command, variant of the default):**

> There are 47 people at the bottom of this page, and they are waiting for you to place a tile.

What it does well: Keeps the second-person urgency of the original but leads with the social fact (people, not scroll command). The number 47 is concrete and specific; the word "waiting" creates mild obligation. Earns the next sentence because the reader wants to know what "place a tile" means.

What it risks: The phrasing "waiting for you" may feel slightly manipulative to some readers; the social pressure could read as cheap.

- **Earns the next sentence:** 3
- **Sounds essayistic:** 2
- **Sets up the asymmetry without spoiling it:** 3

---

**Option 2 (Paradox / counterintuitive observation):**

> The most durable thing on the web is a text file from 2008, and the most fragile is last week's conversation.

What it does well: States the essay's core tension in one sentence without naming git, databases, or any mechanism. It is declarative and specific (2008, last week), and the contrast between "text file" and "conversation" gestures at the read/write gap. Does not explain itself, which makes the reader want §1.

What it risks: Starts with the conclusion before the demo. The reader has not yet been shown the jigsaw puzzle, so the claim lands without evidence, and §1 may feel redundant.

- **Earns the next sentence:** 2
- **Sounds essayistic:** 3
- **Sets up the asymmetry without spoiling it:** 1

---

**Option 3 (Question):**

> Why is your 2008 blog post still up, but the forum thread you replied to that same week is gone?

What it does well: Asks the essay's exact question in plain language. Familiar situation, familiar loss. The reader almost certainly has a personal instance of this (their own forum posts, a phpBB thread they remember). Creates forward pull by withholding the answer.

What it risks: Telegraphs §1 too precisely. The reader who already knows the answer (flat files vs. databases) may feel the essay is confirming what they know rather than showing them something.

- **Earns the next sentence:** 2
- **Sounds essayistic:** 2
- **Sets up the asymmetry without spoiling it:** 2

---

**Option 4 (Anecdote, personal):**

> I wanted to add a comment section to this essay, and the shortest path took me through a database I would eventually abandon.

What it does well: First-person, specific, mundane. The problem is recognizable: every writer who has built a static site has hit this wall. "Eventually abandon" is honest and slightly funny. The reader wants to know what the longer path looked like.

What it risks: Opens with a minor complaint, which can feel small for an essay that wants to name a category. The puzzle demo is nowhere in sight, and the opening defers the most interesting material.

- **Earns the next sentence:** 2
- **Sounds essayistic:** 3
- **Sets up the asymmetry without spoiling it:** 2

---

**Option 5 (Direct quote of an imagined reader):**

> "Just use Disqus" is the standard answer, and the standard answer is why your readers' words from 2015 are gone.

What it does well: Opens with a familiar dismissal and immediately reframes it as a symptom, not a solution. The phrase "your readers' words" makes the loss personal to the writer-reader. Creates forward pull by turning a cliche into a problem statement.

What it risks: Starting with a quote-that-isn't-really-a-quote can feel like a rhetorical setup. The reader may not have "just use Disqus" as their specific reference point; Disqus is dated enough that a younger audience may not register it.

- **Earns the next sentence:** 2
- **Sounds essayistic:** 3
- **Sets up the asymmetry without spoiling it:** 2

---

**Option 6 (Claim / declarative):**

> Every piece of interactivity you add to a static site drags a database back in, and that database is someone's responsibility to keep alive.

What it does well: States the essay's structural diagnosis in one sentence. "Drags back in" is a precise verb for the pattern §2 describes. "Someone's responsibility" immediately implies what happens when that someone leaves. The sentence is complete and specific without being dry.

What it risks: Skips the demonstration entirely. The jigsaw puzzle is not mentioned; the reader has no reason to believe the claim before seeing the counter-example. Better as a thesis restatement inside the essay than as an opening move.

- **Earns the next sentence:** 2
- **Sounds essayistic:** 3
- **Sets up the asymmetry without spoiling it:** 1

---

**Option 7 (Scene, sensory / present-tense):**

> Right now, while you read this, 47 people are placing pieces of a jigsaw puzzle at the bottom of this page, and every move they make is a git commit.

What it does well: Combines the scene-setting of the current default with the reveal of the commit mechanism in one breath. "Right now, while you read this" creates simultaneous presence across all readers. The puzzle and the mechanism are both in the sentence, so the reader's curiosity shifts immediately to "why does that matter?"

What it risks: Giving away "git commit" before §3 names the mechanism. The essay's structure lets the reader feel the problem (§0-§2) before naming the solution (§3); this sentence short-circuits that by leading with the answer.

- **Earns the next sentence:** 3
- **Sounds essayistic:** 3
- **Sets up the asymmetry without spoiling it:** 2

---

**Recommended:** Option 1, because it keeps the visceral scene entry of the default while leading with the social fact (other people are already there) rather than a scroll command, and it does not give away the mechanism before §3 earns it.

---

### Title candidates

The current default title is: *Your Blog Will Outlive Your Database (It Doesn't Have To)*

---

**Title A (the current default):**

> Your Blog Will Outlive Your Database (It Doesn't Have To)

What it does well: The main clause states the durability asymmetry as a known fact; the parenthetical inverts it immediately, creating productive dissonance. "Your blog" and "your database" are both second-person and concrete. The essay delivers exactly on both halves: yes, flat files outlive databases, and no, the write path doesn't have to be disposable.

What it risks: "Your database" is slightly misleading: most personal bloggers don't own the database, they rent it via a service. The parenthetical can read as hedging rather than as a reversal.

- **Memorable:** 3
- **Searchable / linkable:** 3 (slug: `your-blog-will-outlive-your-database`)
- **Earns its claim:** 3

---

**Title B (compressed, leads with the category name):**

> Git-Native Publishing (And Why Your Writes Keep Dying)

What it does well: Names the coined category in the title, making the essay immediately findable by anyone who searches the term later. The subtitle is direct: "your writes keep dying" is the asymmetry problem in casual language.

What it risks: Cold-opening on a coined term the reader has never heard. "Git-native publishing" means nothing to someone arriving from a link; the subtitle has to carry all the entry-weight. The subtitle is also slightly breathless and mixes register with the clean category name.

- **Memorable:** 2
- **Searchable / linkable:** 3 (slug: `git-native-publishing`)
- **Earns its claim:** 3

---

**Title C (inverts the framing, question-led):**

> What If Your Readers' Words Were as Durable as Your Posts?

What it does well: Poses the asymmetry as a question, making the reader the subject. "Your readers' words" is more specific than "writes" or "interactivity." The question form implies the answer exists and the essay delivers it, which it does.

What it risks: The question form can read as soft or blog-post generic. It does not name the mechanism (git) or the category, so it could be a post about any alternative comment system. Less unique, harder to remember, harder to find.

- **Memorable:** 1
- **Searchable / linkable:** 2 (slug: `what-if-your-readers-words-were-as-durable-as-your-posts`)
- **Earns its claim:** 2

---

**Title D (sharpens the contrast, drops the parenthetical):**

> Reads Are Durable. Writes Are Not. (And What To Do About It)

What it does well: Leads with the named asymmetry from §1 verbatim. The two declarative sentences side by side are punchy. The parenthetical promises a constructive answer, not just a complaint.

What it risks: "Reads" and "Writes" are technical terms that readers outside the web-dev world won't parse on first glance. The subtitle adds length without adding specificity. The essay's most interesting material (the git mechanism, the puzzle demo) is invisible.

- **Memorable:** 2
- **Searchable / linkable:** 2 (slug: `reads-are-durable-writes-are-not`)
- **Earns its claim:** 3

---

**Title E (leads with the demo, earns the abstraction):**

> 47 People Are Solving This Puzzle in a Git Repository

What it does well: Specific number, concrete activity, surprising location. Anyone who sees this title has at least one question ("why?"), which is exactly what the essay answers. The title doubles as the opening claim and as a description of the demo itself.

What it risks: Reads as a novelty title rather than a theory title. "Git repository" narrows the audience sharply to readers who know what git is. The title does not signal that the essay makes a broader claim about web durability; a reader might expect a tutorial on hosting collaborative tools.

- **Memorable:** 3
- **Searchable / linkable:** 2 (slug: `47-people-are-solving-this-puzzle-in-a-git-repository`)
- **Earns its claim:** 2

---

**Recommended:** Title A (the current default), because it states the asymmetry problem and its reversal in one breath, the slug is clean and will compound well when "git-native publishing" is cited later, and the essay delivers on both halves of the title's implied promise.
