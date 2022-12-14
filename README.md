# Heroku Review Application

Create a Heroku review app when a PR is raised by someone with write or admin access

## Usage

```yaml
# in .github/workflows/review-app.yml
name: Heroku Review App
on:
  pull_request:
    types: [opened, reopened, synchronize, labeled, closed]
  pull_request_target:
    types: [opened, reopened, synchronize, labeled, closed]

jobs:
  heroku-review-application:
    if: ${{ github.event.label.name == 'Review App' }} || contains(github.event.pull_request.labels.*.name, 'Review App') # Add This if you want to run the job based on a label - Review App
    name: Heroku Review App
    runs-on: ubuntu-latest
    steps:
      - name: Heroku Review Application
        uses: rodrigoea/pr-heroku-review-app@master
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          heroku_api_token: ${{ secrets.HEROKU_API_TOKEN }}
          heroku_pipeline_id: ${{ secrets.HEROKU_PIPELINE_ID }}
```

## Available Configuration

### Inputs

- **github_token** - Github API access token
- **heroku_api_token** - Heroku API Token; generate this under your personal settings in Heroku
- **heroku_pipeline_id** - Pipeline ID configured to use review apps. You can get this from the URL in your browser.
