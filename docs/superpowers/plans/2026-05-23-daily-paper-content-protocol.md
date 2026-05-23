# Daily Paper Content Protocol Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build the local project scaffold that lets `D:\Project\red_paper` run the approved 7-day daily paper-to-content protocol.

**Architecture:** This is a file-backed workflow, not an app. The implementation creates a root index, a daily output directory, reusable Markdown templates, and a runbook that tells Codex exactly how to process each paper with `ljg-paper`, `ljg-qa`, and `ljg-rank` while keeping all outputs inside this project.

**Tech Stack:** Markdown, PowerShell validation commands, Git.

---

## Scope Check

The approved spec describes one coherent workflow: a 7-day daily paper-to-content protocol. It does not need to be split into separate subsystem plans.

This implementation deliberately does not add reminders, automatic paper selection, publishing automation, or a script that tries to read papers. Those are non-goals until the 7-day trial produces evidence.

## File Structure

Create or modify these files:

- Create: `D:\Project\red_paper\index.md`
  - Responsibility: track each daily paper run in one row.
- Create: `D:\Project\red_paper\daily\.gitkeep`
  - Responsibility: keep the empty daily output directory in Git before the first run.
- Create: `D:\Project\red_paper\templates\meta.md`
  - Responsibility: metadata, timing, status, and quality score template for each run.
- Create: `D:\Project\red_paper\templates\paper.md`
  - Responsibility: project-local `ljg-paper` output skeleton.
- Create: `D:\Project\red_paper\templates\qa.md`
  - Responsibility: project-local `ljg-qa` output skeleton.
- Create: `D:\Project\red_paper\templates\rank.md`
  - Responsibility: project-local `ljg-rank` output skeleton.
- Create: `D:\Project\red_paper\templates\content.md`
  - Responsibility: publishable short essay skeleton.
- Create: `D:\Project\red_paper\RUNBOOK.md`
  - Responsibility: daily operating instructions for Codex and the user.

## Task 1: Create Index and Daily Directory

**Files:**
- Create: `D:\Project\red_paper\index.md`
- Create: `D:\Project\red_paper\daily\.gitkeep`

- [ ] **Step 1: Create the root index**

Create `D:\Project\red_paper\index.md` with this exact content:

```markdown
# Red Paper Daily Index

This index tracks the 7-day daily paper-to-content trial.

| Date | Paper | Topic | Folder | Core claim | Status |
|---|---|---|---|---|---|
```

- [ ] **Step 2: Create the daily directory keeper file**

Create `D:\Project\red_paper\daily\.gitkeep` as an empty file.

- [ ] **Step 3: Verify the files exist**

Run:

```powershell
Test-Path -LiteralPath 'D:\Project\red_paper\index.md'
Test-Path -LiteralPath 'D:\Project\red_paper\daily\.gitkeep'
```

Expected output:

```text
True
True
```

- [ ] **Step 4: Commit Task 1**

Run:

```powershell
git add -- index.md daily/.gitkeep
git commit -m "Add daily protocol index"
```

Expected result: Git creates a commit containing only `index.md` and `daily/.gitkeep`.

## Task 2: Create Daily Artifact Templates

**Files:**
- Create: `D:\Project\red_paper\templates\meta.md`
- Create: `D:\Project\red_paper\templates\paper.md`
- Create: `D:\Project\red_paper\templates\qa.md`
- Create: `D:\Project\red_paper\templates\rank.md`
- Create: `D:\Project\red_paper\templates\content.md`

- [ ] **Step 1: Create `templates\meta.md`**

Create `D:\Project\red_paper\templates\meta.md` with this exact content:

```markdown
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
- Status: done
- ljg-rank used: yes

Quality score:
- Overall: [1-5]/5
- paper.md: [1-5]/5
- qa.md: [1-5]/5
- content.md: [1-5]/5
- Biggest issue:

Notes:
```

- [ ] **Step 2: Create `templates\paper.md`**

Create `D:\Project\red_paper\templates\paper.md` with this exact content:

```markdown
# Paper

## Metadata

- Original title:
- Chinese working title:
- Authors:
- Venue / year:
- DOI / URL:
- Source file:

## Problem

Use one concrete example to make the reader feel the problem before naming the theory.

## Old Route

Explain the prior assumption, default method, or common interpretation that this paper pushes against.

## New Opening

State the opening the paper creates: what did the authors notice that makes another route possible?

## Mechanism

Explain the method or argument in Chinese. Keep formulas out of the main explanation unless they are translated into ordinary language.

## Key Concepts

### Concept 1

- One-sentence meaning:
- How it appears in the paper's example:
- Why the paper needs it:

### Concept 2

- One-sentence meaning:
- How it appears in the paper's example:
- Why the paper needs it:

### Concept 3

- One-sentence meaning:
- How it appears in the paper's example:
- Why the paper needs it:

## Findings

Summarize the strongest results, including concrete numbers when the paper provides them.

## Counterintuitive Side Finding

If the paper has one, explain it. If it does not, write: "This paper does not have a strong counterintuitive side finding."

## Transferable Insight

Write the one thought worth carrying away from the paper.

## Review Judgment

Judge whether the paper is worth taking seriously, where it is strong, and where its boundary is.
```

- [ ] **Step 3: Create `templates\qa.md`**

Create `D:\Project\red_paper\templates\qa.md` with this exact content:

```markdown
# Q-A

## Q1:

**Conclusion:**

**Formalized relation:**

**Reasoning steps:**

**Boundary:**

## Q2:

**Conclusion:**

**Formalized relation:**

**Reasoning steps:**

**Boundary:**

## Q3:

**Conclusion:**

**Formalized relation:**

**Reasoning steps:**

**Boundary:**

## Q4:

**Conclusion:**

**Formalized relation:**

**Reasoning steps:**

**Boundary:**

## Q5:

**Conclusion:**

**Formalized relation:**

**Reasoning steps:**

**Boundary:**
```

- [ ] **Step 4: Create `templates\rank.md`**

Create `D:\Project\red_paper\templates\rank.md` with this exact content:

````markdown
# Rank

## Rank Target

Name whether this file is reducing the paper's small field, core mechanism, phenomenon cluster, or content-worthy question.

## Basic Assumptions

State the assumptions the target quietly stands on.

## Phenomena To Regenerate

- 
- 
- 
- 
- 

## Root Rank

Explain the few independent generators that can reproduce the phenomena above.

## Transfer

Explain what this rank lets the user see or write outside this paper.

## ASCII Structure

```text
[draw with ASCII only: + - | / \ > < v ^ * = ~ . : # [ ] ( ) _ , ; ! " and spaces]
```
````

- [ ] **Step 5: Create `templates\content.md`**

Create `D:\Project\red_paper\templates\content.md` with this exact content:

```markdown
# Title

Core claim:

## Draft

Write 300-800 Chinese words.

Start from a concrete confusion. Explain the paper's mechanism in plain Chinese. End with what the reader can now understand or do differently.
```

- [ ] **Step 6: Verify all templates exist**

Run:

```powershell
$files = @(
  'D:\Project\red_paper\templates\meta.md',
  'D:\Project\red_paper\templates\paper.md',
  'D:\Project\red_paper\templates\qa.md',
  'D:\Project\red_paper\templates\rank.md',
  'D:\Project\red_paper\templates\content.md'
)
$files | ForEach-Object { "{0} {1}" -f (Test-Path -LiteralPath $_), $_ }
```

Expected output:

```text
True D:\Project\red_paper\templates\meta.md
True D:\Project\red_paper\templates\paper.md
True D:\Project\red_paper\templates\qa.md
True D:\Project\red_paper\templates\rank.md
True D:\Project\red_paper\templates\content.md
```

- [ ] **Step 7: Commit Task 2**

Run:

```powershell
git add -- templates/meta.md templates/paper.md templates/qa.md templates/rank.md templates/content.md
git commit -m "Add daily artifact templates"
```

Expected result: Git creates a commit containing only the five template files.

## Task 3: Create the Daily Runbook

**Files:**
- Create: `D:\Project\red_paper\RUNBOOK.md`

- [ ] **Step 1: Create `RUNBOOK.md`**

Create `D:\Project\red_paper\RUNBOOK.md` with this exact content:

````markdown
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
````

- [ ] **Step 2: Verify the runbook references local output**

Run:

```powershell
Select-String -Path 'D:\Project\red_paper\RUNBOOK.md' -Pattern 'D:\\Project\\red_paper|~/Documents/notes|ljg-paper|ljg-qa|ljg-rank'
```

Expected: output includes all three skills, the local project path, and the instruction not to write daily artifacts to `~/Documents/notes/`.

- [ ] **Step 3: Commit Task 3**

Run:

```powershell
git add -- RUNBOOK.md
git commit -m "Add daily paper runbook"
```

Expected result: Git creates a commit containing only `RUNBOOK.md`.

## Task 4: Validate the Scaffold Against the Spec

**Files:**
- Verify: `D:\Project\red_paper\index.md`
- Verify: `D:\Project\red_paper\daily\.gitkeep`
- Verify: `D:\Project\red_paper\templates\meta.md`
- Verify: `D:\Project\red_paper\templates\paper.md`
- Verify: `D:\Project\red_paper\templates\qa.md`
- Verify: `D:\Project\red_paper\templates\rank.md`
- Verify: `D:\Project\red_paper\templates\content.md`
- Verify: `D:\Project\red_paper\RUNBOOK.md`

- [ ] **Step 1: Verify required files exist**

Run:

```powershell
$required = @(
  'D:\Project\red_paper\index.md',
  'D:\Project\red_paper\daily\.gitkeep',
  'D:\Project\red_paper\templates\meta.md',
  'D:\Project\red_paper\templates\paper.md',
  'D:\Project\red_paper\templates\qa.md',
  'D:\Project\red_paper\templates\rank.md',
  'D:\Project\red_paper\templates\content.md',
  'D:\Project\red_paper\RUNBOOK.md'
)
$missing = $required | Where-Object { -not (Test-Path -LiteralPath $_) }
if ($missing.Count -eq 0) { 'PASS: all required files exist' } else { $missing }
```

Expected output:

```text
PASS: all required files exist
```

- [ ] **Step 2: Verify the runbook has no disallowed automation**

Run:

```powershell
Select-String -Path 'D:\Project\red_paper\RUNBOOK.md' -Pattern 'reminder|automation|auto-select|publish automation|schedule'
```

Expected: no output.

- [ ] **Step 3: Verify the templates do not contain unresolved marker words**

Run:

```powershell
$markers = @('TB' + 'D', 'TO' + 'DO', 'FIX' + 'ME', '待' + '定', '待' + '补', 'place' + 'holder')
$pattern = $markers -join '|'
rg -n $pattern D:\Project\red_paper\templates D:\Project\red_paper\RUNBOOK.md D:\Project\red_paper\index.md
```

Expected: no output.

- [ ] **Step 4: Verify Git is clean**

Run:

```powershell
git status --short
```

Expected: no output.

If there is output, inspect it. Commit only intentional scaffold files. Do not include unrelated local files.

## Task 5: First Daily Run Smoke Test

**Files:**
- Create during first real paper run: `D:\Project\red_paper\daily\YYYY-MM-DD--paper-short-name\meta.md`
- Create during first real paper run: `D:\Project\red_paper\daily\YYYY-MM-DD--paper-short-name\paper.md`
- Create during first real paper run: `D:\Project\red_paper\daily\YYYY-MM-DD--paper-short-name\qa.md`
- Create during first real paper run: `D:\Project\red_paper\daily\YYYY-MM-DD--paper-short-name\rank.md`
- Create during first real paper run: `D:\Project\red_paper\daily\YYYY-MM-DD--paper-short-name\content.md`
- Modify during first real paper run: `D:\Project\red_paper\index.md`

- [ ] **Step 1: Wait for user paper input**

Do not choose a paper proactively. Wait for the user to provide a readable paper input.

- [ ] **Step 2: Confirm readable full text exists**

If the user provides a local file, run:

```powershell
$paperPath = Read-Host 'Paste the exact full local paper path'
Test-Path -LiteralPath $paperPath
```

Expected output:

```text
True
```

If the user provides a URL, open or fetch enough of the source to confirm it contains readable full text. If only an abstract is available, stop and ask the user for PDF, HTML full text, Markdown, or another readable full-text source.

- [ ] **Step 3: Create the daily folder**

Use the current date and a short lowercase paper slug:

```powershell
$date = Get-Date -Format 'yyyy-MM-dd'
$slug = Read-Host 'Enter a short lowercase paper slug'
$folder = "D:\Project\red_paper\daily\$date--$slug"
New-Item -ItemType Directory -Force -Path $folder | Out-Null
```

Expected: directory exists.

- [ ] **Step 4: Create the five daily files from templates**

Copy the templates into the daily folder:

```powershell
$date = Get-Date -Format 'yyyy-MM-dd'
$slug = Read-Host 'Enter the same short lowercase paper slug'
$folder = "D:\Project\red_paper\daily\$date--$slug"
Copy-Item -LiteralPath 'D:\Project\red_paper\templates\meta.md' -Destination (Join-Path $folder 'meta.md')
Copy-Item -LiteralPath 'D:\Project\red_paper\templates\paper.md' -Destination (Join-Path $folder 'paper.md')
Copy-Item -LiteralPath 'D:\Project\red_paper\templates\qa.md' -Destination (Join-Path $folder 'qa.md')
Copy-Item -LiteralPath 'D:\Project\red_paper\templates\rank.md' -Destination (Join-Path $folder 'rank.md')
Copy-Item -LiteralPath 'D:\Project\red_paper\templates\content.md' -Destination (Join-Path $folder 'content.md')
```

Expected: all five files exist in the daily folder.

- [ ] **Step 5: Run the actual paper workflow**

Replace the copied template content with real output in this order:

```text
paper.md -> qa.md -> rank.md -> content.md -> meta.md -> index.md
```

Use `ljg-paper`, `ljg-qa`, and `ljg-rank` instructions when creating the first three files.

- [ ] **Step 6: Verify the first daily run**

Run:

```powershell
$date = Get-Date -Format 'yyyy-MM-dd'
$slug = Read-Host 'Enter the same short lowercase paper slug'
$folder = "D:\Project\red_paper\daily\$date--$slug"
$files = 'meta.md','paper.md','qa.md','rank.md','content.md' | ForEach-Object { Join-Path $folder $_ }
$files | ForEach-Object { "{0} {1}" -f (Test-Path -LiteralPath $_), $_ }
Select-String -Path 'D:\Project\red_paper\index.md' -Pattern $date
```

Expected: all five file checks print `True`, and the index contains the date row.

- [ ] **Step 7: Commit the first daily run**

Run:

```powershell
$date = Get-Date -Format 'yyyy-MM-dd'
$slug = Read-Host 'Enter the same short lowercase paper slug'
git add -- index.md "daily/$date--$slug/"
git commit -m "Add daily paper run for $date"
```

Expected result: Git creates a commit containing the first daily paper folder and the updated index.

## Self-Review Notes

Spec coverage:

- Trigger and accepted inputs are implemented in `RUNBOOK.md`.
- Project-local output is implemented by `daily/`, templates, and `RUNBOOK.md`.
- The four-artifact order is implemented in `RUNBOOK.md` and the first-run smoke test.
- `meta.md` and `index.md` requirements are implemented by templates and the root index.
- No reminders, auto-selection, publishing automation, or abstract-only work is added.

Marker scan:

- Future-run commands collect the daily path and slug at execution time.
- The implementation files created by this plan should not contain unresolved marker words.

Type consistency:

- Status values match the spec: `done`, `debt`, `repaired`.
- Quality score fields match the approved design: overall plus `paper.md`, `qa.md`, and `content.md`.
- `rank.md` is included as a daily artifact and affects overall score rather than receiving a separate subscore.
