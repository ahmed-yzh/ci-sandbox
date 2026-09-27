# ci-sandbox

A throwaway repo for learning GitHub Actions and environments. No company code
lives here.

## What it shows

1 workflow, `.github/workflows/pipeline.yml`, with 4 jobs:

| Job | Runs when | Environment | Approval |
| --- | --- | --- | --- |
| `checks` | every push and pull request | none | no |
| `deploy-dev` | push to `dev` | `dev` | no |
| `deploy-staging` | push to `staging` | `staging` | no |
| `deploy-production` | push to `main` | `production` | yes, a required reviewer |

The deploy jobs only print what they would do. Nothing is deployed anywhere.

Each environment has:

- a deployment branch rule, so only its own branch can use it
- a variable `APP_URL` with a fake address
- a secret `DEMO_SECRET` with a fake value, to show that GitHub hides secrets in logs as `***`

## Try it

1. Push a change to `dev`. Watch `checks`, then `deploy-dev`.
2. Merge `dev` into `staging`. Watch `deploy-staging`.
3. Merge `staging` into `main`. `deploy-production` stops and waits. Open the run and press "Review deployments", then approve.
4. Break it on purpose: make `checks` fail, and see that no deploy job runs.
