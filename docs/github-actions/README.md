# Study notes of GitHub Actions

[GitHub Actions](https://docs.github.com/en/actions)

## Actions

```yaml
jobs:
  stale:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/stale@v3
```

The `actions/stale@v3` is actually a github repo which define how to do the action. [stale](https://github.com/actions/stale)

## Events

### scheduled events

Scheduled events trigger a workflow run at a specified time. They use the **POSIX cron syntax** .

[reference to cron syntax](https://crontab.guru/)

### Webhook events

> These types of events trigger a workflow when GitHub webhook events – such as issue and pull request creation, update and deletion, deployment, page_build, and others – are created. This is an introductory idea of what webhook events are, and it is not a comprehensive list of webhook events that can trigger workflows.

[Events which trigger workflow](https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows#webhook-events)

## Runners

There are two kind of runners:

- GitHub-hosted runners
- Self-hosted runners

```yaml
jobs:
  build:
    runs-on: macos-latest
```

Other alias can be used in **runs-on** field

- windows-latest or windows-2019
- ubuntu-20.04
- ubuntu-latest or ubuntu-18.04
- ubuntu-16.04
- macOS-11.0
- macOS-latest or macOS-10.5

  [Self-hosted runners](https://docs.github.com/en/actions/hosting-your-own-runners/configuring-the-self-hosted-runner-application-as-a-service)
