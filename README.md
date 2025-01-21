# Publish Dotnet Nuget to JFrog Artifactory

This GitHub Action publishes .NET packages to JFrog Artifactory.

## Inputs

- `file_publish_path`: Relative path to the packages (default: `**/*.nupkg`, required)
- `target`: Target path in Artifactory (required)
- `skip_duplicate`: Skip duplicate packages (default: `true`, optional)

## Secrets

- `artifactory_url`: Artifactory URL (required)
- `api_key`: Artifactory API key (required)

## Example Usage

```yaml
name: Publish .NET Package

on: [push]

jobs:
  publish:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Publish to Artifactory
        uses: gekowdaniels/jfrog-nuget-push@v1
        with:
          file_publish_path: '**/*.nupkg'
          target: 'owner/your-repo/1.0.0'
        secrets:
          artifactory_url: ${{ secrets.ARTIFACTORY_URL }}
          api_key: ${{ secrets.ARTIFACTORY_API_KEY }}
