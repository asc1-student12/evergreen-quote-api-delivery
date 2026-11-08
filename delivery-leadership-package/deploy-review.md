# Deploy Review: Evergreen marketing site (S3)

Reviewed Day 3 (Sun 8 Nov 2026) by Scott Cannon. No AWS account used; live deploy not run.

## Checks
- `bash -n deploy/deploy-to-s3.sh`: parses OK
- Read `infrastructure.md`, `bucket-policy.json`, `iam-policy.json`

## Who can read
Anyone on the internet, read-only, objects only (`Principal: *`, `s3:GetObject`). Cannot list the bucket.

## Who can write
Only an identity granted the IAM policy: `PutObject`, `DeleteObject`, `ListBucket` on `evergreen-quote-site` only. Least privilege: one bucket, three actions, no wildcards.

## Questions for the team
1. The bucket policy uses the placeholder `BUCKET-NAME` while the IAM policy names `evergreen-quote-site`. Is the placeholder substituted at deploy time? If not, the read policy targets a bucket that does not exist.
2. `DeleteObject` lets the deploy credential remove the whole site. Who holds it? It should be the CI role, not a personal account.

## Related
The site quotes auto 35 / 50000 at $400 vs the API at $450 (risk register R10).
