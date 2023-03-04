# mikbot-workflow

Reusable workflow for mikbot projects

# Using

```yml
jobs:
  mikbot:
    uses: mikbot/mikbot-workflow/.github/workflows/mikbot-workflow.yml@v1.0.6
    with:
      run-maven-publish: true
    secrets:
      GCP_ACCOUNT_KEY: ${{ secrets.GCP_ACCOUNT_KEY }}
      JFROG_USER: ${{ secrets.JFROG_USER }}
      JFROG_PASSWORD: ${{ secrets.JFROG_PASSWORD }}
      SIGNING_KEY: ${{ secrets.SIGNING_KEY }}
      SIGNING_KEY_PASSWORD: ${{ secrets.SIGNING_KEY_PASSWORD }}
```

# Parameters

| Name                       | Type    | Description                               | Default | Required |
|----------------------------|---------|-------------------------------------------|---------|----------|
| `run-maven-publish`        | Boolean | Run `gradle publish` at the end of build  | false   | false    |
| `update-plugin-repository` | Boolean | Push plugins to GCS repository            | true    | false    |
| `update-binary-repository` | Boolean | Push bot binary to GCS repository         | false   | false    |
| `discord-webhook`          | Boolean | Send Gradle Build scan to Discord webhook | false   | false    |

# Secrets

The following secrets can be specified
using [GitHub Secrets](https://docs.github.com/de/actions/security-guides/encrypted-secrets)

| Name                 | Type            | Description                                | Default | Required                                                            |
|----------------------|-----------------|--------------------------------------------|---------|---------------------------------------------------------------------|
| BUILDCACHE_USER      | String          | Gradle Build Cache user                    | null    | false                                                               |
| BUILDCACHE_PASSWORD  | String          | Gradle Build Cache password                | null    | if `BUILDCACHE_USER` is specified                                   |
| DISCORD_WEBHOOK      | String          | Discord Webhook URL to push build scans to | null    | if `discord-webhook` is true                                        |
| GCP_ACCOUNT_KEY      | String (base64) | ServiceAccountKey.json of GCS bucket       | null    | if `update-plugin-repository` or `update-binary-repository  is true |
| JFROG_USER           | String          | Maven username                             | null    | if `run-maven-publish` is true                                      |
| JFROG_PASSWORD       | String          | Maven password                             | null    | if `run-maven-publish` is true                                      |
| SIGNING_KEY          | String          | Signing key                                | null    | if `run-maven-publish` is true                                      |
| SIGNING_KEY_PASSWORD | String          | Signing key password                       | null    | if `run-maven-publish` is true                                      |
