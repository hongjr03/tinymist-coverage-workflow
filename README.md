# Tinymist Coverage Workflow

A reusable GitHub Actions workflow for generating and tracking code coverage for Typst documents using Tinymist.

## Features

- ✅ Automatically generate coverage reports for Typst documents
- ✅ Track coverage changes over time
- ✅ Add coverage badges to README files
- ✅ Highly configurable to suit different project needs
- ✅ Works with any Typst project using Tinymist

## Usage

### Basic Setup

To use this workflow in your repository, create a workflow file (e.g., `.github/workflows/coverage.yml`) with the following content:

```yaml
name: Coverage Analysis

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]
  workflow_dispatch:

jobs:
  coverage:
    runs-on: ubuntu-latest
    steps:
      # First checkout the code
      - name: Checkout code
        uses: actions/checkout@v4
        
      # Then run Tinymist Coverage workflow
      - uses: hongjr03/tinymist-coverage-workflow@v0.1.4
        with:
          target_files: 'README.typ'  # Your main Typst file
```

### Advanced Configuration

You can customize the workflow with the following inputs:

| Input | Description | Default |
|-------|-------------|---------|
| `tinymist_version` | Version of Tinymist to use | `latest` |
| `create_symlinks` | Whether to create symlinks for local Typst package development | `true` |
| `target_files` | Files to analyze (comma separated) | `README.typ` |
| `report_path` | Path to store coverage reports | `coverage/output` |
| `auto_commit` | Whether to auto-commit report updates | `true` |
| `readme_paths` | README files to update with badge (comma separated) | `README.md,README_zh.md` |

Example with all options:

```yaml
jobs:
  coverage:
    runs-on: ubuntu-latest
    steps:
      # First checkout the code
      - name: Checkout code
        uses: actions/checkout@v4
        
      # Then run Tinymist Coverage workflow
      - uses: hongjr03/tinymist-coverage-workflow@v0.1.4
        with:
          tinymist_version: 'latest'
          create_symlinks: false
          target_files: 'main.typ,docs/guide.typ'
          report_path: 'docs/coverage'
          auto_commit: false
          readme_paths: 'README.md'
```

## Coverage Badge

Once the workflow runs successfully, it will add or update a coverage badge in your specified README files:

[![Coverage](https://img.shields.io/badge/coverage-85.5%25-green)](coverage/output/coverage_report.md)

## Requirements

- GitHub repository with Typst files
- Tinymist-compatible project

## How It Works

1. The workflow installs Tinymist and other required dependencies
2. It creates symlinks for local Typst packages if enabled (for package development)
3. It runs coverage analysis on your specified files
4. A detailed coverage report is generated
5. README files are updated with coverage badges
6. Changes are committed back to the repository (if auto_commit is enabled)
7. Reports are uploaded as workflow artifacts

## License

MIT

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.
