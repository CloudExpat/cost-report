# CloudExpat GitHub Action Test

This repository is used to test the CloudExpat GitHub Action workflow.

## What it does

When a Pull Request is created, the GitHub Action:
1. Fetches cloud cost and carbon data from CloudExpat API
2. Posts a summary as a PR comment
3. Adds the report to the GitHub Actions job summary

## Setup

The `CLOUDEXPAT_API_KEY` secret must be configured in repository settings.
