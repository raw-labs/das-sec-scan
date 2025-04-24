# DAS Security Scanner Action

A GitHub Action that scans Docker images for vulnerabilities with special handling for Raw Labs dependencies. This action combines Trivy scanning with dependency analysis to provide comprehensive security reports.

## Features

- Scans Docker images using Trivy
- Analyzes SBT dependency trees
- Special handling for Raw Labs transitive dependencies
- Generates detailed security reports in both Markdown and SARIF formats
- Creates or updates GitHub issues with scan results
- Automatic labeling based on vulnerability severity

## Usage

```yaml
name: Security Scan
on:
  schedule:
    - cron: '0 0 * * *'  # Run daily at midnight UTC
  workflow_dispatch:  # Allow manual trigger

jobs:
  security-scan:
    runs-on: self-hosted
    steps:
      - uses: actions/checkout@v4
        with:
          fetch-depth: 0  # Required when image-tag/image-name not provided (for auto-detecting latest release)

      - uses: raw-labs/das-sec-scan@main
        with:
          github-token: ${{ github.token }}  # Required: used for API access
```

## Inputs

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| `github-token` | GitHub token for API access | No | `${{ github.token }}` |
| `report-dir` | Directory to store reports | No | `security-reports` |
| `severity` | Severity levels to scan for (comma-separated) | No | `CRITICAL,HIGH` |
| `image-tag` | Image tag to use for scanning | No | Latest release tag |
| `image-name` | Full image name to scan | No | Auto-constructed from repo name |

## Outputs

| Output | Description |
|--------|-------------|
| `found-vulnerabilities` | Whether any vulnerabilities were found (true/false) |
| `vulnerability-count` | Total number of vulnerabilities found |
| `report-path` | Path to the generated report file |
| `issue-number` | Issue number if a report was created or updated |

## Report Format

The action generates a detailed Markdown report that includes:

- Total vulnerability count
- System dependencies vulnerabilities
- Library dependencies vulnerabilities, categorized by:
  - Raw Labs dependencies (with dependency chain information)
  - Third-party dependencies

The report will be available in the workflow summary with a direct link to the GitHub issue if vulnerabilities are found.

## Labels

The action automatically creates and manages the following labels:

- `security`: For all security-related issues
- `automated`: For automatically generated content
- `version:<tag>`: For tracking issues related to specific versions
- `severity:critical`: For critical vulnerabilities
- `severity:high`: For high severity vulnerabilities
- `severity:medium`: For medium severity vulnerabilities
- `severity:low`: For low severity vulnerabilities

## Requirements

- Repository must have releases with semantic versioning (or provide explicit `image-tag`)
- Docker images must follow the naming convention: `ghcr.io/<org>/<repo>/<repo>-server:<version>` (unless `image-name` is provided)
- SBT project with `dependencyBrowseTreeHTML` task available
- Java 21 (installed automatically)
- Git checkout with full history (`fetch-depth: 0`) required only when auto-detecting latest release (when neither `image-tag` nor `image-name` provided)

## License

Apache-2.0 license - see LICENSE file for details
