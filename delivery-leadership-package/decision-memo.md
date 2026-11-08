# Decision Memo: Renters coverage is next round, not this week

**Date:** Sun 8 Nov 2026 (Day 2)
**Author:** Scott Cannon, Delivery Lead
**Decision area:** Inject #1, scope request from a partner aggregator

## Context

A partner aggregator wants renters coverage quotable through the API by Thursday, describing it as "just one more dropdown option." The delivery goal is unchanged: an assembled, tested, containerized API, merged with a green build. I checked the request against the running service before answering, rather than estimating.

## Options considered

1. **Yes, by Thursday.** Gives the partner what they asked for. But the API refuses renters today: a test quote returns a 400, "renters is not a valid enum value." A yes means changing the quote schema, adding a renters rate that does not exist and that only the sponsor can set, and adding a test proving renters prices correctly. This week's work is assembly only; these are new code changes, made two days before a merge.
2. **Yes, but only the API.** Smaller: the schema, the rate and a test, without the website. Rejected because the partner still could not use it this week: the platform team confirms the API is not internet-exposed until after this week.
3. **Next round, with a costed answer now.** No new code this week; the delivery goal is protected; the partner gets a specific plan instead of a box.

## Recommendation

Option 3. Renters is not quotable this week. I give the partner the exact list of what changes and a next-round slot, and I need a renters rate from the sponsor before that slot can start.

## Why

The partner cannot send traffic this week whatever we decide, so a yes buys them nothing by Thursday and costs us untested pricing changes two days before a merge. On Sunday morning this same API quoted $50,000 of coverage at 35 cents a month and looked perfectly correct doing it. I will not add a new premium path the week we ship without the test that would catch that.

## What would change my mind

If the sponsor confirms a renters rate **and** that the API will be partner-reachable this week, I would take Option 2 on Tuesday morning, before CI is enabled, and move the site's deploy review to next round. I need that by 11:00 Tuesday 10 November.

## How the cost was known

Not estimated: measured. A renters quote returns a 400 today, the same rejection a "boat" quote got this morning: the schema already treats renters as an unknown coverage type. A search of the code finds coverage types in seven places: the schema (`Quote.js`), the rate table (`premium.js`, which has no renters row), both seed scripts, and the website's dropdown, script and sample data. GraphQL needs no change, because it passes the type through and lets the one schema decide. A new test is required; no existing test needs editing.
