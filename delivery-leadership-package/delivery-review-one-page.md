# Evergreen Quote API: Phase 3 Delivery Review

**Scott Cannon · Delivery Lead (solo) · Phase 3 capstone · One-page presentation**

### Delivery goal: hit

> By Thursday 12 November, the assembled Evergreen Quote API (REST and GraphQL over MongoDB, with schema validation and a green test suite) is merged to main through a reviewed pull request with a green CI run, and demonstrated giving the same answers from a container and from three replicas on a local Kubernetes cluster.

| Evidence | Result |
|---|---|
| Merged PR | [PR 17](https://github.com/asc1-student12/evergreen-quote-api-delivery/pull/17), squash-merged, tagged `phase-3` |
| CI on the merge commit | [Green, run 42621154479](https://github.com/asc1-student12/evergreen-quote-api-delivery/actions/runs/42621154479), the first CI run main has ever had |
| Tests | 9 of 9, locally, in CI, and from a fresh clone |
| Container | Same answers as the dev server |
| Cluster | 3 API pods and 1 database Running, zero restarts; a home quote for age 45 and $200,000 returned $2,700 through the Service |

### Two key decisions

**Renters coverage is next round, not this week.** The partner called it "one more dropdown option." I measured instead of estimating: the API rejected renters with a 400, and coverage types lived in seven files, plus a rate only the sponsor can set. The API was not internet-exposed this week, so a yes bought the partner nothing by Thursday. ([decision-memo.md](decision-memo.md))

**GO WITH CONDITIONS while main was red.** My branch was green; main was red from a hotfix. Different facts about different code. I held until main was green and the team confirmed how a change the pipeline had rejected reached customers. At re-evaluation I found my main had never run CI, so I treated the merge commit's run as the real gate. It went green. ([go-no-go.md](go-no-go.md))

### Risks and injects

**Top risk: AI-drafted code returns plausible, wrong answers.** The AI-drafted handler returned a tidy 201 pricing $50,000 of coverage at **35 cents a month**. The status-code test passed; only the arithmetic test caught it. ([risk-register.md](risk-register.md))

**Inject #1:** renters deferred with a costed answer; base-image CVE accepted for this week with a rebuild condition; four specific asks of the sponsor, one with a deadline. ([status-update.md](status-update.md))

**Inject #2:** I framed the red run as the tests doing their job, and named the contradiction: **a red run ships nothing**, so customers' rejections came another way. I routed that question to API on-call instead of fixing the validator. ([incident-response.md](incident-response.md))

**Found, not handed out:** the site quotes **$400** where the API quotes **$450** (two rate tables) · the S3 bucket is named **four ways across four files**, one hard-coded ([deploy-review.md](deploy-review.md)) · CI warns of a deprecated action runtime and a floating runner label · a Copilot-drafted test passes for **any** 400 ([copilot-critique.md](copilot-critique.md)).

### What I'd do differently

- **Check what is running before debugging what is written.** A missed reload and a container left on an old image both looked like code bugs.
- **Make AI-drafted tests check content, not just status.** Catch it in review, not by experiment.
- **Treat warnings with dates as scheduled work**, sized on day one.
- **Assume the environment can disappear.** The VM shut down mid-review; nothing was lost because I pushed at every block boundary.
