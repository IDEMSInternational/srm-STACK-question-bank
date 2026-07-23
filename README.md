# SRM STACK Question Bank

STACK question XML files adapted from Peter K. Dunn's *SRM-Textbook*
([PeterKDunn/SRM-Textbook](https://github.com/PeterKDunn/SRM-Textbook)) — an
open statistics/research-methods textbook.

Questions here are authored by a multi-agent AI pipeline (Concierge →
Planner → Author/Reviewer build loop → Planner review), then reviewed
before being committed. The pipeline itself lives in the separate
`stack-agents-michele` repo, not here — this repo only holds the final,
approved question output.

## Structure

```
questions/<category>/<question_name>/
    <question_name>.xml               ← the STACK question (Moodle XML)
    <question_name>_description.md    ← living description of the question's current state
    <question_name>_logs.md           ← append-only record of what each agent did and why
```

## Rules

- Every question must have ≥2 test cases (correct + at least one wrong answer)
- Wrong-answer test inputs use offsets from the correct answer (e.g. `ta+1`), never independent random values
- Committing is always a human decision — agents never commit directly

## Source content

Questions are based on material from the *SRM-Textbook*, © Peter K. Dunn
(source repo license: see [PeterKDunn/SRM-Textbook/COPYING](https://github.com/PeterKDunn/SRM-Textbook/blob/main/COPYING)).
