# Incident Response: quote rejections and a red CI run on main

**Date:** Day 3 (Sun 8 Nov 2026), ~14:00
**From:** Scott Cannon, Delivery Lead
**Channel:** #incidents

## What the CI log says, in plain English

The CI run on `main` failed at the test step: the "widen the age range" hotfix changed the age minimum to 110 while the maximum stayed at 100, so every test that creates a real quote gets a 400, and the run produced no build. Checkout, setup, the database service and the install all passed; only the safety net fired.

## Message posted

Thanks, support. Two things are true at once and I don't want to assume they are one problem.

**What I observed.** Customers get a 400 on every age tried ("age (34) is less than minimum allowed value (110)"), and CI on `main` has been red since the age-range hotfix about 40 minutes ago. The failing step is the test suite: the two tests that create real quotes get the same rejection at ages 52 and 35. That run produced no build, and a red run ships nothing. So whatever customers are hitting reached them some other way.

**What I'm asking.** Can the API on-call engineer confirm what is actually deployed in front of customers right now, and whether that change went out around the pipeline, for example a deploy from a branch or a manual change? And can whoever owns the hotfix confirm what the age change was meant to do? The diff sets the minimum to 110, while the maximum stays 100.

**Who owns the next step.** API on-call owns what is deployed and any rollback decision. The hotfix owner owns a corrected change, through CI. I own Thursday's merge decision and the sponsor and support updates, so nobody else has to answer two audiences.

**Air cover.** The site deploy review is parked, and I will move today's check-in if you need the time. Nobody needs to rush a fix to protect my delivery: my branch is green and does not contain the hotfix. And the tests did their job here. They refused to approve a change that would reject every customer; the question is how that change got past them.

## Why I routed rather than fixed

The diff points at an obvious one-line cause. Changing it myself would skip the owner, skip CI, and leave the more serious question unanswered: how a change the pipeline rejected reached customers at all.
