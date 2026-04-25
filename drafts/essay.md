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

## 2. Why this happened

## 3. The missing primitive

## 4. Git's vocabulary is strictly richer than REST's

## 5. The jigsaw, a worked example

## 6. Honest limits

## 7. The claim, and the invitation
