# Task List (Reference Shape)

> The real task list lives on your GitHub Project board. This file is the **shape**: what each issue should look like before it leaves your hands. Link to the board from `vision-brief.md`.

## Issue template

```
Title: [AREA] short verb-first description

Who it's for: <user>. What they get: <thing>. Why it matters: <outcome>.

Done criteria
- [ ] Observable thing 1
- [ ] Observable thing 2
- [ ] Observable thing 3

Out of scope
- Anything that is *related* but explicitly not in this issue.

Linked decisions / risks
- (links to decision memos or risk-register rows if applicable)
```

## Suggested starter tasks (you may add, split, or drop)

| # | Title | Area | Priority |
|---|---|---|---|
| 1 | Seed the database and inspect it in mongosh | DATA | P0 |
| 2 | Set the service name via .env | CONFIG | P1 |
| 3 | Apply sponsor rate decision in premium.js | CONFIG | P0 |
| 4 | Assemble the quote routes; run the safety net; apply the kit one-line fix | API | P0 |
| 5 | Mount GraphQL; run a query and the mutation in the explorer | GRAPHQL | P0 |
| 6 | Build and run the container image | CONTAINER | P0 |
| 7 | Enable GitHub Actions CI workflow | CI | P0 |
| 8 | Review the site deploy artifacts (script + both policies) | SITE | P0 |
| 9 | Demonstrate the API on the local cluster (dry-run first) | K8S | P0 |
| 10 | Open PR from delivery/lead → main | REVIEW | P0 |
| 11 | Document one Copilot-assisted step + critique | AI | P2 (stretch) |
