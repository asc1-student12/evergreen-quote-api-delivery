# Delivery Goal: Evergreen Quote API

## Goal

> By Thursday 12 November, the assembled Evergreen Quote API, REST and GraphQL
> over MongoDB, with schema validation and a green test suite is merged to
> main through a reviewed pull request with a green CI run, and demonstrated
> giving the same answers from a container and from three replicas on a local
> Kubernetes cluster.

**Spoken version:** *Thursday: merged with green CI, same answers from a
container and from three pods on a cluster.*

## "Done" looks like

- The API answers every documented route: list, fetch by id, create with a computed premium.
- The same data answers through GraphQL, with the explorer at `/explorer`.
- `npm test` passes; the safety net holds.
- The containerized API serves the same answers as the dev server, and the CI run on the merge commit is **green**.
- The cluster demo shows three API pods behind one Service.
- A reviewed PR is merged, branch deleted.
- `delivery-leadership-package/` is complete and committed.

## Out of scope (this week)

- No authentication, no real rate engine, no live AWS deploy unless the instructor calls a live window.
- No wiring of the marketing site to the API.
- No refactoring of the provided pieces and no mid-week toolchain upgrades.