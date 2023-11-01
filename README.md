# Semantic Release Github Action

![GitHub Workflow Status](https://img.shields.io/github/actions/workflow/status/90dy/gha-semantic-release/semantic-release.yml)
![GitHub release (latest SemVer)](https://img.shields.io/github/v/release/90dy/gha-semantic-release)

This GitHub Action allows you to run [semantic-release](https://semantic-release.gitbook.io/semantic-release/) with the same options as the command-line interface (CLI) in your GitHub Actions workflow. Semantic Release automates the versioning and release process of your software projects.

## Usage

To use this GitHub Action, add the following YAML code to your workflow file (e.g., `.github/workflows/semantic-release.yml`):

```yaml
name: Semantic Release

on:
  push:
    branches:
      - main

permissions:
  contents: write

jobs:
  release:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout Code
        uses: actions/checkout@v4

      - name: Semantic Release
        uses: 90dy/gha-semantic-release@v1
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
        with:
          extends: '' # List of modules or file paths containing shareable configurations
          branches: main # List of branches on which releases should happen
          repository-url: '' # The git repository URL
          tag-format: '' # Git tag format for identifying releases
          plugins: | # List of plugins to use
            @semantic-release/commit-analyzer
            @semantic-release/release-notes-generator
            @semantic-release/changelog
            @semantic-release/github
            @semantic-release/git
          dry-run: 'false' # Enable or disable dry-run mode
          ci: 'true' # Enable or disable Continuous Integration environment verifications
          debug: 'false' # Enable or disable debugging

```

You can configure the inputs based on your project's requirements:

- `extends`: List of modules or file paths containing a [shareable configuration](https://semantic-release.gitbook.io/semantic-release/usage/shareable-configurations).

- `branches`: The branches on which releases should happen. By default, it includes common branch patterns.

- `repository-url`: The git repository URL.

- `tag-format`: The Git tag format used to identify releases.

- `plugins`: Define the list of plugins to use.

- `dry-run`: Enable or disable dry-run mode.

- `ci`: Enable or disable Continuous Integration environment verifications.

- `debug`: Enable or disable debugging.

## License

This GitHub Action is licensed under The Unlicense License. See the [LICENSE](LICENSE) file for details.
