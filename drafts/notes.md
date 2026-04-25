# Notes

## Prior art scan (Task 4, 2026-04-24)

### Direct coinages

#### `"git-native publishing"`

No results using this exact phrase as a coined term or named category. Search returned:

- https://learning.postman.com/docs/agent-mode/native-git -- Postman's "Native Git" feature: local-first API spec editing synced to their cloud. Uses "native git" as a product feature name, not a publishing category.
- https://apigit.com/native-git-repository -- APIGit: API specs stored in a repo. Same product-feature framing; no claim to a named category.
- https://gitbook.com/docs/getting-started/quickstart -- GitBook: collaborative docs platform. Uses git for versioning but does not call itself "git-native."
- https://github.com/stefanha/git-publish -- git-publish: patches as git tags. Niche developer workflow tool; no category claim.
- https://dylan-k.github.io/Palabra/process.html -- Palabra: a git-based writing process for publishers. Describes a workflow, not a coined term.

**Verdict:** The exact phrase "git-native publishing" is absent from the web as a coined term or claimed category. No one has planted this flag.

#### `"git-based publishing"`

The phrase appears descriptively but is not coined as a named category. Results are largely about GitHub Pages, CI/CD deployment pipelines, and Quarto. No essay or project has claimed "git-based publishing" as the name for a design space.

- https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site -- GitHub Pages docs use "publishing source" in a Git context; purely procedural.
- https://docs.posit.co/connect/admin/integrations/git-repositories/ -- Posit Connect: deploy from a Git repo; again procedural.
- https://quarto.org/docs/publishing/github-pages.html -- Quarto to GitHub Pages; workflow docs, no category claim.

**Verdict:** Used as a lowercase descriptor in deployment docs, never as a coined category. No prior claim.

#### `"git as a CMS"`

This framing is well-established and has been the industry's way of describing git-backed CMSs since roughly 2018 to 2021. Multiple vendors and bloggers use it explicitly.

- https://decapcms.org/blog/git-based-cms-definition-features-best-practices/ -- Decap CMS's own blog post defining the category "git-based CMS." Industry-standard framing.
- https://cloudcannon.com/git-cms/ -- CloudCannon markets itself as "A Git-based CMS for visual editing"; landing page uses "git cms" as a URL slug.
- https://craftercms.com/blog/2021/07/what-is-a-git-based-cms -- Crafter CMS blog post explaining the "git-based CMS" category; well-cited 2021 definition.
- https://www.netlify.com/blog/2021/08/31/how-git-can-power-an-exciting-future-for-content-management/ -- Netlify: "Why Git is the Future of Content Management." Close to the essay's thesis but narrowed to CMS tooling and operator workflows, not the durability/symmetry argument.
- https://strapi.io/blog/git-based-vs-api-first-cms -- Strapi's comparison of "git-based vs API-first CMS"; positions git-based as one of two headless CMS architectures.

**Verdict:** "Git as a CMS" and "git-based CMS" are established terms in the Jamstack/headless-CMS industry. They describe the content-management workflow (editors commit content via a UI backed by Git). They do NOT address the durability asymmetry between reads and writes, do NOT treat the commit as a general-purpose write primitive for reader interaction, and do NOT make the vocabulary claim (git ops as a superset of REST verbs). The essay's claim is distinct: it names the *substrate* category, not the *editor-tooling* category.

#### `"commit-as-write"`

Zero results using this exact phrase as a coined term. Search returned:

- Oracle Database's `COMMIT WRITE` clause (asynchronous redo-log behavior) -- unrelated.
- Conventional Commits spec (https://www.conventionalcommits.org/en/v1.0.0/) -- structured commit messages; adjacent but does not treat a commit as a reader-facing write operation.
- General "how to write a commit message" tutorials -- not relevant.

**Verdict:** The term "commit-as-write" as a named primitive is absent from the web. No prior claim.

#### `"git-backed comments"`

This pattern exists in the wild, documented as a folk practice since at least 2012 to 2013:

- https://gist.github.com/4676585 -- "Git(Hub)-backed comments system" gist (2012/2013): comments as JSON files in a repo, PRs used as the moderation queue. Earliest use of "git-backed" in this context.
- https://github.com/imsun/gitment -- Gitment: comments via GitHub Issues (2017). A working implementation.
- https://utteranc.es/ -- Utterances: comments via GitHub Issues (2018, actively maintained). Well-known in static-site circles.
- https://giscus.app/ -- Giscus: comments via GitHub Discussions (2021, actively maintained).

**Verdict:** "Git-backed comments" as a descriptor exists and is used by the projects above. However, it is a narrow application, not a framework or category claim. No one has generalized it to a design philosophy or named a category around it.

---

### Adjacent canon

#### local-first software (Ink & Switch, 2019)

- URL: https://www.inkandswitch.com/essay/local-first/
- Authors: Martin Kleppmann, Adam Wiggins, Peter van Hardenberg, Mark McGranaghan. Published at Onward! 2019.
- What it is: Seven ideals for software that keeps data on-device, works offline, allows collaboration, and gives users long-term ownership. Uses CRDTs (via Automerge) as the enabling technology.
- What it covers: Durability from the user's perspective, data ownership, offline-first. The canonical prior work for the durability argument.
- What it leaves out: Git specifically; the commit as a write primitive; the read/write asymmetry on the *web* (its framing is about app data, not published web content); the vocabulary comparison with REST.

#### Decap CMS (formerly Netlify CMS)

- URL: https://decapcms.org/
- What it is: Open-source React app that wraps the Git workflow for content editors on static sites. Transferred from Netlify to community stewardship in 2023.
- What it covers: Git as an editorial workflow tool for site *operators*; markdown content storage in a repo.
- Gap: Treats Git as a backend for the operator's writing, not as a write substrate for reader participation. Comments, votes, and user-generated content are out of scope.

#### TinaCMS

- URL: https://tina.io/
- What it is: Open-source, Git-backed headless CMS with visual inline editing. Originally created by Forestry.io; later acquired by SSW.
- What it covers: Same category as Decap: Git-backed editing UI for site operators.
- Gap: Same as Decap. No reader-write story; no durability-of-participation argument.

#### Forestry.io (pivot to TinaCMS)

- URL: https://tina.io/forestry (migration guide)
- What it is: Forestry.io was a Git-based CMS that shut down in 2023, directing users to TinaCMS (which Forestry's team built).
- Note: The Forestry-to-Tina lineage is significant context for the "git-based CMS" category's commercial history.

#### Utterances (GitHub-issues-backed comments)

- URL: https://utteranc.es/
- What it is: Lightweight JS widget that stores blog comments as GitHub Issues threads. Auth via GitHub OAuth.
- What it covers: Proves the concept that reader writes can live in a Git host without a separate database.
- Gap: Issues are not commits; the write is to GitHub Issues, not to the repo's commit log. No structured-payload convention; no append-only merkle semantics.

#### Giscus (GitHub Discussions-backed comments)

- URL: https://giscus.app/
- What it is: Like Utterances but backed by GitHub Discussions instead of Issues. No ads, no tracking, open source.
- What it covers: Same use case as Utterances; more actively maintained.
- Gap: Same as Utterances: writes go to Discussions, not to the commit log.

#### Solid (Tim Berners-Lee, pods)

- URL: https://solidproject.org/
- What it is: W3C-adjacent decentralized web project. Users own "pods" (personal data stores) hosted wherever they choose; apps request access via OAuth.
- What it covers: Data ownership and portability; decentralized identity; unhosted storage.
- Gap: Requires a running Solid pod server; no content-addressing, no append-only history, no fork semantics. Git's operational vocabulary (branch, merge, tag, fork) has no equivalent.

#### Remote Storage (5apps protocol)

- URL: https://remotestorage.io/
- What it is: Open protocol (IETF draft) for per-user, unhosted storage. HTTP PUT/GET/DELETE to a user-chosen storage provider; OAuth auth. Championed by 5apps.
- What it covers: Separating app from user data; unhosted web apps.
- Gap: Mutable key-value store over HTTP; no history, no content-addressing, no commit semantics. REST-shaped, not git-shaped.

#### IPFS publishing tools

- URL: https://ipfs.tech/
- What it is: Content-addressed, peer-to-peer file system. IPFS addresses are hashes of content; IPNS adds a mutable name layer.
- What it covers: Content-addressing and decentralized hosting; immutable content links; used by some Web3 / NFT publishing workflows.
- Gap: Read-heavy; write path is upload-and-pin, not a structured commit log. No history semantics native to IPFS itself (no merge, no branch, no fork); no structured-payload convention for reader events.

#### Beaker Browser / Hyper

- URL: https://github.com/beakerbrowser/beaker (archived 2022)
- What it is: Experimental peer-to-peer browser built on the Dat/Hypercore protocol. Users could publish and fork websites directly from the browser without a server.
- What it covers: Peer-to-peer web publishing; built-in fork semantics; no central host required.
- Gap: Project was archived in December 2022; Hypercore protocol continues under Holepunch but browser/publishing tooling is dormant. Used a custom P2P protocol, not Git. No commit-log as event store.

---

### Synthesis

1. **Is "git-native publishing" claimed in any meaningful way?** No. The exact phrase does not appear as a coined term or named category anywhere on the web. The closest is the well-established industry term "git-based CMS," which covers editorial tooling for site operators, not the broader design-space claim the essay is making.

2. **Is "commit-as-write" claimed in any meaningful way?** No. The phrase is absent from the web as a coined term. The only near-collision is Oracle's SQL `COMMIT WRITE` clause, which is unrelated.

3. **Which adjacent works are closest to the essay's claim?** The Ink & Switch local-first essay (2019) is the closest philosophical ancestor; it makes the durability and ownership argument but does not focus on Git or the web's read/write asymmetry. Utterances and Giscus demonstrate the proof-of-concept (reader writes stored in a Git host without a database) but do not generalize or name a category. The "git-based CMS" industry (Decap, Tina, Crafter, CloudCannon) occupies a narrow slice: Git as editorial workflow for operators.

4. **Citation sentence for the essay's §3:** "The Jamstack community has spent several years building the 'git-based CMS' category (Decap, Tina, CloudCannon), which proves that Git can replace a database for editorial writes; what none of those tools address is the symmetric problem: reader writes, the participation layer, the commits that belong to your audience rather than your team."

5. **Does any finding require rewriting the essay's plan?** No. All findings fit within the existing §3 framing. The essay should (a) acknowledge the "git-based CMS" category as the closest existing term and explain what it does not cover, (b) nod to Ink & Switch local-first as the philosophical predecessor, and (c) note Utterances/Giscus as proof-of-concept implementations that stop short of the full claim. No new section is needed; these acknowledgments slot naturally into §3 ("The missing primitive").

---

### Action items for the drafting

- In §3, briefly acknowledge "git-based CMS" as the existing term and distinguish: that category solves operator writes; this essay claims the *substrate* layer, which also covers reader writes.
- Credit Ink & Switch local-first essay (2019) as the philosophical ancestor of the durability argument; note that local-first uses CRDTs rather than Git.
- Mention Utterances/Giscus in §3 or §5 as demonstrations that reader writes can live in a Git host without a database, but clarify they use Issues/Discussions, not the commit log.
- Do not use the phrase "git-based CMS" as if it were equivalent to "git-native publishing"; the essay's claim is wider.
- The essay can state plainly that "git-native publishing" and "commit-as-write" are original coinages; no prior art requires defensive attribution.
