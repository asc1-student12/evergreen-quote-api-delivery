# Deploy Review: Evergreen marketing site (S3)

Reviewed Day 3 (Sun 8 Nov 2026) by Scott Cannon. No AWS account used; live deploy not run.

## Checks
- `bash -n deploy/deploy-to-s3.sh`: parses OK
- Read `infrastructure.md`, `bucket-policy.json`, `iam-policy.json`

## Who can read
Anyone on the internet, read-only, objects only (`Principal: *`, `s3:GetObject`). Cannot list the bucket.

## Who can write
Only an identity granted the IAM policy: `PutObject`, `DeleteObject`, `ListBucket`, scoped to one bucket with no wildcards. `DeleteObject` is justified: the script uses `aws s3 sync --delete`, which removes files no longer in the site.

## What is done well
- Least privilege on both policies.
- The script refuses to run while the bucket name still contains CHANGE-ME (lines 17-18).

## Finding: the bucket is named four ways in four files
- `deploy-to-s3.sh`: evergreen-quote-site-CHANGE-ME (placeholder)
- `bucket-policy.json`: BUCKET-NAME (placeholder)
- `infrastructure.md`: YOUR-BUCKET-NAME (placeholder)
- `iam-policy.json`: evergreen-quote-site (hard-coded)

S3 bucket names are globally unique, so each deployer sets their own. But the IAM policy grants write only to the exact name evergreen-quote-site. Set the script to any other bucket and the deploy fails with AccessDenied. Nothing checks that the four agree; the script guard protects only the script.

## Questions for the team
1. Should the IAM policy take the same placeholder as the others, so all four are set together? Or should one value be generated into all four?
2. Who holds the deploy credential? `DeleteObject` lets it remove the whole live site; it should be the CI role, not a personal account.

## Related
The site quotes auto 35 / 50000 at $400 vs the API at $450 (risk register R10).
