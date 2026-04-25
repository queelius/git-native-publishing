# Your Blog Will Outlive Your Database

(it doesn't have to)

## 0. The puzzle

Scroll to the bottom of this page. There's a jigsaw puzzle there, and right
now 47 people are working on it with you. Some of them placed a piece an hour
ago. One placed a piece while you were reading this sentence. You can see the
picture assembling itself, tile by tile, toward something that isn't quite
resolved yet.

Here is the thing that makes this unusual: every piece placement is a git
commit. When you drag a tile into position and it clicks into place, a commit
lands in a public repository. It carries your GitHub username, a timestamp,
and a structured record of which piece went where. The whole puzzle's solving
history is a git log. That log is not stored in a database that I control. It is not behind a
paywall or an API rate limit. It is not going to disappear if I stop paying
for a server. Every person who has ever touched this puzzle is in that log,
and the log will exist as long as one copy of the repository exists somewhere.
Someone can fork it tonight. Someone can clone it in 2035. The history does
not belong to me; it belongs to the commits, which means it belongs to
everyone who made one.

The standard way to build a
puzzle like this would be a database table: `piece_id`, `slot_x`, `slot_y`,
`user_id`, `timestamp`. The table lives on a server. The server is somebody's
responsibility. When that person gets tired or goes broke or moves on, the
table disappears, and the history disappears with it. Every comment thread,
every leaderboard, every "who solved it first" record: gone.

Your forum threads from 2008 are gone.

## 1. The asymmetry

But your 2008 blog post still renders.

If someone published it as static HTML or Markdown on a personal domain and kept
paying eight dollars a year for hosting, the URL still works. The page still
loads. The words are still there. You can read it right now on a browser that
didn't exist when it was written, running on hardware the author never imagined,
fetched over a protocol version that postdates the post itself. None of that
matters. The file is a file.

Markdown won the durability war by being boring. There is no schema to migrate.
No application server to restart. No vendor to outlive. A `.md` file is a text
file; a text file from 2008 is as readable today as it was then. The boring-ness
is the point. When a format makes no demands on its environment, the environment
can change freely around it. People who chose flat files in 2006 were not
visionaries; they were lazy in the exact right way.

The forum did not have that option. A phpBB community lives only while someone tends the server. The moment the
hosting bill bounces or the moderator takes a new job, the state goes with them. Not just the
posts, but the replies, the edits, the votes, the relationships between pieces of
content. All of it lived in a database that required an operator. When the
operator left, the database closed.

And this is not just about old forums. It is the same story for every layer of
interactivity we add to a page today. Want comments? You need mutable state. Want
reactions, edits, collaborative cursors, presence indicators? Each one needs a
write path, and every write path needs a server, and every server needs someone
responsible for it. The content stays up. The interactions disappear.

*Reads are durable; writes are not.*

The question is why we ever stopped building things that work that way.

## 2. Why this happened

## 3. The missing primitive

## 4. Git's vocabulary is strictly richer than REST's

## 5. The jigsaw, a worked example

## 6. Honest limits

## 7. The claim, and the invitation
