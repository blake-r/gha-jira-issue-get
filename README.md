# Jira Server Issue Get

Downloads Jira issue in the JSON format.


## Example

```
on:
  - pull_request:
      types:
        - opened
        - reopened
        - synchronize

jobs:
  gha-test:
    runs-on: ubuntu-latest
    name: 'GitHub Action Test'
    steps:
      - uses: actions/checkout@v3
      - id: issue
        uses: blake-r/gha-jira-issue-get@latest
        with:
          jira_url: ${{ secrets.TEST_JIRA_URL }}
          jira_pat: ${{ secrets.TEST_JIRA_PAT }}
          issue_key: gbl-1
      - shell: bash
        run: test "$(jq -r '.fields.status.name' '%{{ steps.issue.filename }}')" = "Done"
```
