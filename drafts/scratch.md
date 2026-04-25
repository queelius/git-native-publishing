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

(examples go here, built in Task 3)

## Candidate opening lines for §0

(brainstormed in Task 13)
