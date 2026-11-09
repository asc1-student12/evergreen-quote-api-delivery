# Copilot-Assisted Step and Critique

**Date:** Sun 8 Nov 2026 (Day 3)
**Author:** Scott Cannon, Delivery Lead
**Tool:** GitHub Copilot in VS Code (the approved assistant for this program)
**Prompt:** "Draft one more test for this file: a POST to /api/quote with a missing field (no coverageAmount) returns 400."

## What it produced

One test, appended to `test/api.test.mjs`. It posts `{ type: "home", age: 40 }` with no `coverageAmount` and asserts the response status is 400.

## Critique

Copilot got the mechanics right: it followed the file's conventions exactly, and it sent a body that was valid apart from the one missing field, which isolates the thing under test. The suite went from 8 to 9 passing. What it got wrong is subtler: it checks only the status code, never the reason. I proved this rather than assuming it. Changing the expected status to 201 made the test fail, so the assertion is live. But changing the body to an invalid type as well still passed, because the test cannot tell a 400 for a missing `coverageAmount` from a 400 for anything else. That is the same weakness that let Sunday's status-only test pass the 35-cent premium bug. I would ship it, because it adds real coverage and can fail, but I would not call it complete.

## Accepted, adapted, or rejected

**Accepted as written.** I did not rewrite Copilot's output; this week's edit scope is assembly, and the lab asks to keep or delete. The gap goes into Thursday's pull request as a review question: should this test also check that the error names `coverageAmount`?

## What in the pipeline checks Copilot's output?

CI runs the test on every push, so it checks that Copilot's test **passes**. Nothing in the pipeline checks that it is a **good** test: a test that passes for the wrong reason is green in CI. Breaking it on purpose, twice, was the check. The safety net that caught Sunday's AI-drafted defect also ran today's AI-drafted test, but deciding whether that test deserves to be in the net was human work.

## Data handling

Copilot saw only the prompt and the open test file. No customer data, credentials or production configuration were involved; the repo's `.env` holds only a localhost database address and the service name.
