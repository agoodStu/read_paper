# Red Paper Runbook

This project runs a 7-day daily paper-to-content protocol.

## Trigger

The user sends one readable paper.

Accepted inputs:

- PDF
- local file path
- arXiv full text
- HTML full text
- Markdown full text
- DOI or paper title only when readable full text can be found

If readable full text cannot be obtained, do not start the daily run.

## Daily Output Folder

Create one folder:

```text
daily/YYYY-MM-DD--paper-short-name/
```

Inside it, create:

```text
meta.md
paper.md
qa.md
rank.md
content.md
```

Use the files in `templates/` as starting shapes, but replace all instructional text with the day's real output.

## Required Skill Order

Use these skills in this order:

1. `ljg-paper` for `paper.md`
2. `ljg-qa` for `qa.md`
3. `ljg-rank` for `rank.md`
4. Plain Chinese content drafting for `content.md`

All output stays inside `D:\Project\red_paper`. Do not write daily artifacts to `~/Documents/notes/`.

## Execution Order

```text
paper.md -> qa.md -> rank.md -> content.md -> meta.md -> index.md
```

## Output Standards

`paper.md` must be a full paper thinking note, not an abstract.

`qa.md` must contain 5-7 hard questions that reconstruct the argument chain.

`rank.md` must reduce the paper's best target: small field, core mechanism, phenomenon cluster, or content-worthy question. End with a pure ASCII structure diagram.

`content.md` must contain:

- title
- core claim
- 300-800 Chinese words

The content voice is plain-language explanatory.

## Debt Rule

If a paper is unfinished, the next day starts by finishing the previous paper before handling a new paper.

There is no debt cap during the 7-day trial.

## Index Update

After each daily run, append one row to `index.md`:

```markdown
| Date | Paper | Topic | Folder | Core claim | Status |
```

Allowed statuses:

- `done`
- `debt`
- `repaired`

## Meta Scoring

Fill `meta.md` after the four content artifacts are complete.

Use:

```text
Quality score:
- Overall: [1-5]/5
- paper.md: [1-5]/5
- qa.md: [1-5]/5
- content.md: [1-5]/5
- Biggest issue:
```

`rank.md` affects the overall score and the biggest-issue note.

## Memory Rule

Only update `D:\jishanObs\AgentMemory\problems.md` when the paper directly advances an existing durable problem. Do not update memory for generic paper notes.
