# Stakeholder Status Update: Evergreen Quote API

**To:** Priya Ramanathan, Project Sponsor
**From:** Scott Cannon, Delivery Lead
**Date:** Sun 8 Nov 2026 (Day 2)

## What shipped today

- The quote API is assembled and answering: list, fetch by id, and create, all reading the six quotes we seeded and inspected on Day 1.
- The schema rejects bad quotes before they reach the database: age 5 and coverage type "boat" both return a 400 naming the field and the rule.
- **The tests caught a defect the demo could not see.** The AI-drafted create handler returned a tidy 201 with a premium of 35 cents for $50,000 of coverage. The kit's one-line fix is applied; all tests pass, and the same request now returns the correct premium.
- Your decisions are live: the service reports its name, and rates are auto 90 / home 135 / life 70 (auto, age 35, $50,000: $450).
- GraphQL is mounted: a quote created through it appears through REST.

## What slipped (and why)

- Nothing against the delivery goal.
- **Renters coverage is next round, not this week** (decision memo attached). The API rejects renters today; a yes needs a schema change, a rate, and a new test. And the partner could not reach the API this week anyway: the platform team says it is not internet-exposed until next week.

## What's next (Tuesday)

- Package the API as a container and confirm it gives the same answers.
- Turn on CI so every push runs the tests automatically.
- Review the website's S3 deploy artifacts.
- A documented go/no-go on Thursday's merge, made from the CI result.

## Ship or hold on the base image

**Ship this week on `node:22-alpine`.** The finding is moderate severity, the API is not internet-exposed, and this week it runs only on my VM and a local cluster. The patched tag arrives in the platform team's window next week; changing the Dockerfile mid-week would be an unplanned change the day before CI starts gating us. I have logged the upgrade as an issue to rebuild and re-test when the patch lands.

## What I need from you

1. **Tell the partner renters is next round**, with the plan in the memo. From you it is a priority call; from me it reads as a delivery team saying no.
2. **A renters rate**, by the start of next round. It is a pricing decision, not an engineering one.
3. **If you want renters this week regardless**, I need the rate and confirmation that the API will be partner-reachable **by 11:00 Tuesday 10 November**. After that, the answer defaults to next round.
4. **Written confirmation from the platform team** that the API stays off the internet until the patched image is in. My ship call depends on it.
