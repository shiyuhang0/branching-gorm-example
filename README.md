# branching-gorm-example

> **Warning:** This repo is only for testing. Please don't use it in production.

This repo is a gorm example of CI/CD workflow powered by the TiDB Serverless branch. With it, you can test with the branch (a fork of TiDB Serverless cluster) rather than the production cluster in every PR.

Fork this repo and connect to your own TiDB Serverless following the [Branch GitHub Integration](https://docs.pingcap.com/tidbcloud/branch-github-integration) to have a try.

## About this repo

This repo is based on [gorm playground](https://github.com/go-gorm/playground), with some changes:
- A tidb dialect is added to the repo to test the TiDB Cloud.
- The [gormigrate](https://github.com/go-gormigrate/gormigrate) is used in `RunMigrations` to help migration.
- Delete some useless files like GitHub actions, docker-compose, etc.

This repo has been connected to a TiDB Serverless using the [Branching GitHub integration](https://docs.pingcap.com/tidbcloud/branch-github-integration). This brings database branches to your GitHub workflows, and a TiDB Cloud App will automatically manage database branches for you in the pull request.

## CI workflow

The repo has a [GitHub action](./.github/workflows/tests.yml) to run the test on the created TiDB Serverless branch.

This action uses the [wait-for-tidbcloud-branch](https://github.com/tidbcloud/wait-for-tidbcloud-branch) to get branch connection information and pass it by environment variables. We can do it because the repo accepts the `GORM_DSN` environment variable as connection information. See the [code](https://github.com/shiyuhang0/branching-gorm-example/blob/9639f553418456fd1ebb1d933923fba131c98b6b/db.go#L52) for more details.

## CD workflow

As for CD workflow including DDL, we work well with native frameworks.

Take go as an example, you can use the [gormigrate](https://github.com/go-gormigrate/gormigrate) to manage your database migrations. Any DDL changes can be applied to the branch when you test and the production cluster when you merge. Don't worry about the influence of production business, the TiDB Serverless cluster supports online DDL without blocking your business.

## Build your CI/CD pipeline

If you want to build your own example, follow the [Branch GitHub Integration↗︎](https://docs.pingcap.com/tidbcloud/branch-github-integration)
