# Evergreen Quote API: Vision Brief

## Product
**Name:** Evergreen Quote API (Phase 3 service delivery)
**Delivery week:** Phase 3 capstone, Fri 6 Nov to Fri 13 Nov 2026 (Wed 11 Nov off, Veterans Day)
**Delivery Lead:** Scott Cannon (solo)
**Engineering team (represented by):** https://github.com/asc1-student12/evergreen-quote-api-delivery
**GitHub Project board:** https://github.com/users/asc1-student12/projects/3

## Who is the customer?
Three internal teams, each blocked in a different way today. The **website team**
needs a quote service to call: right now the page computes a premium in the
browser and forgets it as soon as the visitor leaves. The **partner-integration
pilot** needs quotes without scraping our site, and wants to choose which fields
come back. The **operations team** needs anything we hand them to be tested in a
pipeline, packaged as a container, and runnable on the Kubernetes platform. If
they cannot rebuild it, they cannot run it. Behind all three sits the first-time
insurance shopper from Phases 1 and 2, who benefits when every channel quotes
the same number. 

## What pain does Evergreen Quote remove?
"I got a price yesterday. Where did it go?" Phases 1 and 2 shipped a page that
calculates a number and keeps nothing: refresh it and the quote is gone, and no
other channel can see it. The API gives a quote somewhere to live. It is stored,
it can be fetched again by id, and the premium is computed once, in one place,
for every channel. Partners stop asking us for a price; they ask the service.
And invalid quotes, such as an applicant aged five or a coverage type that does
not exist, are refused before they ever reach the database, instead of being
discovered later in a report.

## What does "good" look like at end of the week?
- `curl /api/quotes` returns exactly the six quotes we seeded and inspected by
  hand, and a new quote returns 201 with a premium matching the sponsor's rates
  (auto, age 35, $50,000 coverage: $450 per month).
- Invalid input is rejected with a 400 that names the field and the rule.
- GraphQL returns the same data, and a quote created through GraphQL appears
  through REST: two doors, one database.
- The test suite is green in CI on the merge commit, and the container answers
  identically to the dev server.
- Three API replicas and one database run behind one Service on a local
  Kubernetes cluster, rebuilt from the manifests in the repo.

## What are we explicitly NOT doing this week?
- No authentication or authorization.
- No real rate engine: the rate table is a placeholder the sponsor sets.
- No live AWS deploy, CloudFront, EKS or multi-region work, unless the
  instructor calls a live window; the deploy artifacts are reviewed, not run.
- No wiring of the marketing site to the API; the site keeps its own script
  this week.
- No refactoring of the provided pieces and no mid-week toolchain upgrades. The
  one code change is the kit's own one-line fix.

## How will we know if it worked?
- 7 of 7 tests pass on the CI run for the merge commit; zero merges on red.
- 100% of documented routes return their documented status codes (200, 201,
  400, 404), checked by hand with curl against the merged `main`.
- A fresh clone of `main` installs and passes `npm test` with no manual steps,
  and the cluster demo can be torn down and rebuilt from `k8s/` alone.