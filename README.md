# CloudExpat Cost Report Action

[![GitHub Marketplace](https://img.shields.io/badge/Marketplace-CloudExpat%20Cost%20Report-blue?logo=github)](https://github.com/marketplace/actions/cloudexpat-cost-report)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

Automatically post cloud cost and carbon footprint reports to your Pull Requests.

## Features

- **Cost Summary** - Cloud spending across all your connected accounts
- **Carbon Footprint** - Environmental impact of your cloud usage
- **Trend Analysis** - Week-over-week changes
- **Multi-Cloud** - AWS, Azure, and GCP support

## Usage

```yaml
name: CloudExpat Cost Report

on:
  pull_request:
  workflow_dispatch:

permissions:
  pull-requests: write

jobs:
  cost-report:
    runs-on: ubuntu-latest
    steps:
      - uses: CloudExpat/cost-report@v1
        with:
          api-key: ${{ secrets.CLOUDEXPAT_API_KEY }}
```

That's it! The action will post a cost report comment on every PR.

## Setup

### 1. Get Your API Key

1. Log in to [CloudExpat](https://app.cloudexpat.com)
2. Go to **Settings** > **API Keys**
3. Click **Create API Key**
4. Copy the key (starts with `ce_live_`)

### 2. Add the Secret

1. In your GitHub repository, go to **Settings** > **Secrets and variables** > **Actions**
2. Click **New repository secret**
3. Name: `CLOUDEXPAT_API_KEY`
4. Value: Paste your API key

### 3. Create the Workflow

Create `.github/workflows/cloudexpat.yml` with the usage example above.

## Example Output

```markdown
## CloudExpat Cost Report

**Report Period**: Dec 16 - Dec 23, 2025

### Cost Summary

| Account     | Provider | This Week  | Last Week  | Change  |
|-------------|----------|------------|------------|---------|
| Production  | AWS      | $2,450.00  | $2,200.00  | +11.4%  |
| Staging     | Azure    | $340.00    | $380.00    | -10.5%  |
| Analytics   | GCP      | $520.00    | $510.00    | +2.0%   |
| **Total**   |          | **$3,310** | **$3,090** | **+7.1%** |

### Carbon Emissions

| Account     | This Week    | Last Week    | Change  |
|-------------|--------------|--------------|---------|
| Production  | 245 kgCO2e   | 220 kgCO2e   | +11.4%  |
| Staging     | 34 kgCO2e    | 38 kgCO2e    | -10.5%  |
| Analytics   | 52 kgCO2e    | 51 kgCO2e    | +2.0%   |
| **Total**   | **331 kgCO2e** | **309 kgCO2e** | **+7.1%** |
```

## Inputs

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| `api-key` | Your CloudExpat API key | Yes | - |
| `api-url` | API URL (for testing) | No | `https://data.cloudexpat.com` |
| `post-comment` | Post as PR comment | No | `true` |

## Outputs

| Output | Description |
|--------|-------------|
| `report-file` | Path to the generated report file |
| `success` | Whether the report was fetched successfully |

## Configuration Options

### Run on Schedule

```yaml
on:
  schedule:
    - cron: '0 9 * * 1'  # Weekly on Monday 9am UTC
```

### Run on Push to Main

```yaml
on:
  push:
    branches: [main]
```

### Disable PR Comments

```yaml
- uses: CloudExpat/cost-report@v1
  with:
    api-key: ${{ secrets.CLOUDEXPAT_API_KEY }}
    post-comment: 'false'
```

## Troubleshooting

### "CloudExpat API key is required"

Add the `CLOUDEXPAT_API_KEY` secret to your repository settings.

### "Failed to fetch report. HTTP 401"

Your API key is invalid or expired. Generate a new one at [app.cloudexpat.com](https://app.cloudexpat.com/dashboard/settings/api-keys).

### "Failed to fetch report. HTTP 403"

No cloud accounts connected. Add at least one AWS, Azure, or GCP account in CloudExpat.

### No PR comment appears

Ensure your workflow has `pull-requests: write` permission.

## Security

- Store API keys only in GitHub Secrets
- The action requires minimal permissions (`pull-requests: write`)
- Revoke API keys anytime from the CloudExpat dashboard

## Links

- [CloudExpat Dashboard](https://app.cloudexpat.com)
- [Documentation](https://docs.cloudexpat.com)
- [Report Issues](https://github.com/CloudExpat/cost-report/issues)

## License

MIT License - see [LICENSE](LICENSE) for details.
