# Delivery Review: Evergreen Quote API

**Scott Cannon · Delivery Lead (solo) · Phase 3 capstone · 5 minutes**

The presented version is the one-page PDF in this folder: [delivery-review-one-page.pdf](delivery-review-one-page.pdf).

## Slide 1: Delivery goal and did we hit it?

**Goal:** By Thursday 12 November, the assembled Evergreen Quote API (REST and GraphQL over MongoDB, with schema validation and a green test suite) is merged to main through a reviewed pull request with a green CI run, and demonstrated giving the same answers from a container and from three replicas on a local Kubernetes cluster.

**Hit?** ☑ Yes

**Why:** Every clause is checkable in the repository. PR 17 is squash-merged; the CI run on the merge commit is green; the container answered identically to the dev server; three API pods and a database ran behind one Service; and a fresh clone passes all nine tests with no manual steps.

## Slide 2: What shipped

- REST (list, fetch by id, create) and GraphQL with an explorer, over MongoDB; the schema rejects age 5, type "boat" and type "renters" with a 400 naming the field.
- A container image, a CI pipeline, the site and deploy folders, and the cluster manifests.
- Nine tests, including one I wrote and one Copilot drafted.

The API on main:

    $ curl http://localhost:3000/
    {"message":"Evergreen Quote API","status":"ok"}
    $ curl http://localhost:3000/api/quotes/q1
    {"_id":"q1","type":"auto","age":41,"coverageAmount":50000,"monthlyPremium":96,"tags":["renewal"],...}

- Merged PR: https://github.com/asc1-student12/evergreen-quote-api-delivery/pull/17
- Green CI on the merge commit: https://github.com/asc1-student12/evergreen-quote-api-delivery/actions/runs/42621154479
- Merge commit tagged `phase-3`

## Slide 3: Two key decisions

**Decision 1: renters coverage is next round, not this week.** The partner called it "one more dropdown option." I measured it instead of estimating: the API rejected renters with a 400, and the code had coverage types in seven files, plus a rate that does not exist and only the sponsor can set. *Why it mattered:* the platform team confirmed the API was not internet-exposed this week, so a yes bought the partner nothing by Thursday and cost us untested pricing changes two days before a merge.

**Decision 2: GO WITH CONDITIONS on the merge, while main was red.** My branch was green; main was red from a hotfix. Those are different facts about different code. I held the merge until main was green and the team confirmed how a change the pipeline had rejected reached customers. *Why it mattered:* at re-evaluation I found my main had never run CI at all, so I treated the merge commit's own run as the real gate. It went green.

## Slide 4: Risks and the injects

**Top risk (R1): AI-drafted code returns plausible, wrong answers.** On Day 2 the AI-drafted handler returned a tidy 201 pricing $50,000 of coverage at 35 cents a month. The test that checks the status passed; only the test that does the arithmetic caught it.

**Inject #1:** renters deferred with a costed answer; base-image CVE accepted for this week (moderate, not internet-exposed, patched tag next week), logged with a rebuild condition. Four specific asks of the sponsor, one with a deadline. See [status-update.md](status-update.md) and [decision-memo.md](decision-memo.md).

**Inject #2:** I read the red run as the tests doing their job (they refused a schema that rejected every customer) and named the contradiction: a red run ships nothing, so whatever customers hit got there another way. I routed that question to API on-call rather than fixing the validator. See [incident-response.md](incident-response.md) and [go-no-go.md](go-no-go.md).

**Also found, not handed out:** the site quotes $400 where the API quotes $450 for the same inputs (two rate tables); the deploy files name the S3 bucket four ways, one of them hard-coded; and CI warns of a deprecated action runtime and a floating runner label.

## Slide 5: What I'd do differently next round

- **Check what is running before debugging what is written.** Twice a stale process looked like a code bug: a server that missed a reload, then a container left running under an old image. Process start times and `docker ps` settled both.
- **Treat warnings with dates as scheduled work.** The CI warnings were green-build maintenance with deadlines. I logged them; next round I would size them on day one.
- **Make every AI-drafted test check content, not just status.** Copilot's test passed for any 400. I proved that by breaking it, but the pattern should be caught in review, not by experiment.
- **Assume the environment can disappear.** The lab VM shut down mid-review. Nothing was lost only because I pushed at every block boundary; I would keep that as a rule.

## Q&A prep: likely questions

- **"The cluster returned an empty list. Isn't that a bug?"** No: same image, different environment, different data. The cluster's database was created minutes earlier. The name came through the Deployment's environment variable; data never travels with an image.
- **"Why not just fix the min/max typo during the incident?"** Because the more important question wasn't the typo. It was how a change the pipeline rejected reached customers at all. Fixing it myself would have skipped the owner, skipped CI, and buried that question.
- **"Your CI is green. Is the product correct?"** Green proves the tests pass. Copilot's test passes for the wrong reason too, and the site and API disagree on price while every test is green.
- **"Why do the seeded quotes have timestamps now and didn't on Day 1?"** The Day 1 seed went straight into the database through mongosh; the Day 4 reset went through Mongoose, which adds timestamps. Same data, different route in.
