# Daily Paper Content Protocol Design

Date: 2026-05-23
Project: `D:\Project\red_paper`
Status: approved design

## 1. Purpose

This project is a 7-day trial of a daily paper-to-content protocol.

It is not a general reading plan. The goal is to turn one readable paper per day into reusable thinking assets and one publishable Chinese short essay.

The trial answers one question: can the user and Codex reliably complete a heavy daily production unit built around paper reading, Q-A extraction, rank reduction, and content drafting?

## 2. Trigger

The user starts each daily run by sending one paper.

Accepted inputs:

- PDF file
- Local file path
- arXiv link with accessible full text
- HTML full text
- Markdown full text
- DOI or paper title only if Codex can use it to locate readable full text

If readable full text cannot be obtained, the run does not start. Abstract-only work is not allowed for this protocol.

Codex does not choose papers proactively during the 7-day trial. There are no reminders or recurring automations.

## 3. Output Location

All outputs live inside this project, not in `~/Documents/notes/`, even when skills such as `ljg-paper` or `ljg-qa` normally default there.

Each paper gets one daily folder:

```text
D:\Project\red_paper\
  daily\
    YYYY-MM-DD--paper-short-name\
      meta.md
      paper.md
      qa.md
      rank.md
      content.md
```

The project root also keeps:

```text
D:\Project\red_paper\index.md
```

## 4. Execution Order

The daily order is fixed:

```text
paper.md -> qa.md -> rank.md -> content.md -> meta.md -> index.md
```

This order matters. `content.md` must be downstream of the paper reading, Q-A chain, and rank reduction. It should not be written from first impression alone.

## 5. Daily Artifacts

### 5.1 `paper.md`

`paper.md` uses the full `ljg-paper` style.

It should read like a reusable thinking note, not an abstract summary. It should cover:

- the concrete problem the paper addresses
- the old route or default assumption the paper challenges
- the paper's new opening
- the core mechanism or method
- the key concepts needed to understand the paper
- the main findings
- any counterintuitive side finding
- the transferable insight
- a plain-language review of whether the work is worth taking seriously

The body is in Chinese. Original English paper title, authors, venue, DOI, and necessary term names may remain in English metadata.

### 5.2 `qa.md`

`qa.md` uses the full `ljg-qa` style.

It is written for the user's own later review, not for mass publication. It should contain 5-7 hard questions that reconstruct the paper's argument chain.

Questions should cut into:

- why the argument works
- where the method differs from the old route
- what the tradeoff is
- where the claim stops holding
- what the paper makes easier to see

Avoid schoolbook questions such as "What is X?" unless the answer carries a real argumentative load.

Each answer should include:

- conclusion
- formalized relation
- reasoning steps
- boundary condition

### 5.3 `rank.md`

`rank.md` uses `ljg-rank` every day.

Codex chooses the rank target from the paper itself. Depending on the paper, the target may be:

- the small field behind the paper
- the core mechanism
- a cluster of phenomena the paper explains
- the most content-worthy question behind the paper

The goal is not to list key points. The goal is to find the independent generators that can reproduce the relevant phenomena.

The file should end with a pure ASCII structure diagram. Unicode box drawing and arrows are not used.

### 5.4 `content.md`

`content.md` is the daily publishable Chinese short essay.

Minimum required structure:

```text
# Title

Core claim:

300-800 word publishable essay
```

Voice: plain-language explanatory.

The essay should normally move through:

1. a concrete confusion or everyday situation
2. the mechanism the paper helps explain
3. how the mechanism changes the reader's understanding of ordinary life
4. what the reader can take away

It does not need to chase viral copywriting. It must be clear enough for an intelligent non-specialist to understand and retell.

### 5.5 `meta.md`

`meta.md` records the run state:

```text
# Meta

- Date:
- Input source:
- Paper title:
- Authors:
- Venue / year:
- DOI / URL:
- Start time:
- End time:
- Duration:
- Status: done / debt / repaired
- ljg-rank used: yes

Quality score:
- Overall: [1-5]/5
- paper.md: [1-5]/5
- qa.md: [1-5]/5
- content.md: [1-5]/5
- Biggest issue:
```

Quality scores are diagnostic, not motivational. They identify whether the weak link was reading, argument reconstruction, or publishable writing. `rank.md` is assessed through the overall score and the biggest-issue note rather than a separate subscore during this trial.

## 6. Index

`index.md` is updated after each daily run.

Minimum columns:

```text
| Date | Paper | Topic | Folder | Core claim | Status |
```

Allowed status values:

- `done`: completed on the intended day
- `debt`: unfinished and carried forward
- `repaired`: previously unfinished but later completed

## 7. Debt Rule

If a day is unfinished, the next day starts by completing the previous unfinished paper before handling a new paper.

There is no debt cap during this 7-day trial. This is intentionally strict and risky. The trial is testing whether the full heavy protocol can survive real use without adding a scheduling system.

## 8. Completion Definition

A daily run is complete only when all of the following are true:

1. `paper.md` can help the user recover the paper's core idea six months later.
2. `qa.md` reconstructs the paper's argument through a 5-7 question chain.
3. `rank.md` identifies transferable generators rather than restating the paper.
4. `content.md` contains a publishable 300-800 word Chinese essay.
5. `meta.md` records source, time, status, scores, and biggest issue.
6. `index.md` has the day's row.

## 9. Seven-Day Review

After 7 days, review the protocol using actual output rather than intention.

Review questions:

- How many runs were fully completed?
- What was the average duration?
- Which artifact caused the most friction?
- Did `content.md` produce publishable writing or only explanations?
- Did `rank.md` generate useful transfer, or did it become forced?
- Should the protocol continue unchanged, be lightened, or split into standard and heavy days?
- Should future versions add theme seasons, reminders, weekly synthesis, a paper queue, publishing channels, or memory-vault synchronization?

Long-term system design is explicitly out of scope until the 7-day trial produces evidence.

## 10. Non-Goals

This design does not include:

- automatic paper selection
- daily reminders
- a long-term topic season
- publishing automation
- weekly synthesis
- memory-vault updates after every paper
- abstract-only paper work
- output to `~/Documents/notes/`

Memory-vault updates should happen only when a paper directly advances an existing durable problem in `D:\jishanObs\AgentMemory\problems.md`.
