# Go / No-Go: Merge Decision

> Copy to `delivery-leadership-package/go-no-go.md`. Make this call **from** the CI result, not in spite of it.

**Date / time:**
**Decision:** ☐ GO   ☐ NO-GO   ☐ GO WITH CONDITIONS

## CI evidence

- Latest run on `delivery/lead`: _green / red_  ·  link: _paste URL_
- Workflow file: `.github/workflows/ci.yml`
- What the workflow actually checked: _name the steps_

## What "GO" would mean

- Merge `delivery/lead` → `main`, squash, delete branch.
- Tag the merge commit `phase-3`.

## What "NO-GO" would mean

- Hold the merge until: _condition_.
- Owner of that condition: _name_.
- Re-evaluate at: _time_.

## My call

_2–3 sentences. State the call. Name the *one* thing that drove it. Name what would flip it._
