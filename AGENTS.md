# ba-artifacts — shared conventions for all agents in this repo

This repo is shared by three agents in sequence: **brd-agent → frd-agent → uat-generator**. Each
agent's specific job is defined in its own Multica "Instructions" field, not here. This file holds
the rules that apply to all three, no matter which one is running.

## Folder structure

```
ba-artifacts/
├── charter.md              ← the project description (read-only input)
├── scope_agreement.md      ← what's being built right now (read-only input)
├── templates/
│   ├── BRD_template.txt    ← blank form for brd-agent's output
│   └── SRS_template.txt    ← blank form for frd-agent's output
├── raw/                    ← first drafts — whichever agent runs writes ONLY here
└── approved/               ← human-checked — no agent writes here, ever
```

## Universal rules (apply to every agent)

1. **You may only write inside `raw/`.** Never create, edit, or delete anything inside `approved/`
   — that folder is entirely human-controlled.
2. **You may only read approved input from `approved/`.** Never read another agent's file from
   `raw/` as a substitute for the approved version, even if it looks complete. If the `approved/`
   file(s) you need don't exist yet, stop and report that you're blocked — don't guess or proceed
   with unapproved data.
3. `charter.md`, `scope_agreement.md`, and everything in `templates/` are read-only reference
   material. Never modify them.
4. All JSON output must be valid — no comments, no trailing commas — since it's consumed
   programmatically by the next agent and by other teams.
5. If information you need is missing from your inputs, do not block on it — write "To be defined"
   / an empty value as appropriate, and list it in an `open_questions` section of your JSON output
   (or append to `raw/open_questions.json` if that file is part of your job) so a human can resolve
   it later.
6. Never invent facts, rules, or data that weren't given anywhere in your inputs.
7. After writing your output files, commit them together with a clear message
   (`raw: <agent-name> output for <project>`), post a summary comment on the issue listing every
   file you wrote and any open questions, end the comment with exactly:
   `Awaiting human review before this can move to approved/.`, and set the issue status to
   `in_review`. Never move anything to `approved/` yourself — that is a human action.