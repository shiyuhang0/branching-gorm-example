# tidbcloud-branch-gorm-example

> **Warning:** This repo is only for testing. Please don't use it in production.

This repo is a gorm example of CI/CD workflow powered by TiDB Serverless branch. With it, you can test with the branch (a fork of TiDB Serverless cluster) rather than the production cluster in every PR.

Open a new PR or commit in this [example PR](https://github.com/shiyuhang0/tidbcloud-branch-gorm-example/pull/4) to have a try. Note that only 5 branches are allowed now, see [TiDB Serverless branches](https://docs.pingcap.com/tidbcloud/branch-overview) for more details.

## About this repo

This repo is based on [gorm playground](https://github.com/go-gorm/playground), with some changes:
- A tidb dialect is added to the repo to test the TiDB Cloud.
- An environment variable `GORM_TEST` is added. Migrations will not be run with the `branch` value of `GORM_TEST`.
- Delete some useless files like github actions, docker compose, etc.

This repo has been connected to a TiDB Serverless using the [Branching GitHub integration](https://docs.pingcap.com/tidbcloud/branch-github-integration). This brings database branches to your GitHub workflows, a TiDB Cloud App will automatically manage database branches for you in the pull request.

## CI workflow

The repo has a [GitHub action](./.github/workflows/tests.yml) to run the test on the created TiDB Serverless branch.

This action uses the [wait-for-tidbcloud-branch](https://github.com/tidbcloud/wait-for-tidbcloud-branch) to get branch connection information and pass it by environment variables. We can do it because the repo accept the `GORM_DSN` environment variable as connection information. See the [code](https://github.com/shiyuhang0/tidbcloud-branch-gorm-example/blob/9639f553418456fd1ebb1d933923fba131c98b6b/db.go#L52) for more details.

## CD workflow

As for CD workflow including DDL, we strongly advocate for the utilization of native frameworks.


## Build your CI/CD pipeline

If you want to build your own example, follow the [Branch GitHub Integration↗︎](https://docs.pingcap.com/tidbcloud/branch-github-integration)

## Example
