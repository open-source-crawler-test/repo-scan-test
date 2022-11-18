# repo-scan-test

Repository Secrets:
- 


## Basic Usage

```
name: Repository Scan 
on: 
 push:

jobs:
  test-action:
    runs-on: ubuntu-latest
    steps:
      - name: ✅ Run action.yml to verify all steps pass
        uses: open-source-crawler-test/repo-scan-test@main
        with:
          repository: ${{ github.repository }}
          typo-scan-exclude-match: '[''typos/**'', ''public/**'']'
```


## Advanced Usage

Scan an external repository, and archive the report in a repository you own.

> Make sure you add `PERSONAL_ACCESS_TOKEN: <GITHUB_ACCESS_TOKEN>` to Repository Secrets. This should have WRITE access to the archive repository, so it can upload the folders

```
name: Repository Scan w/ Report Archive
on: 
 push:

## -- CHANGE THIS --
env:
  # Scan THIS repository
  repository: ${{ github.repository }}
  # Scan EXTERNAL repository
  external-repo: facebook/react

jobs:
  test-action:
    runs-on: ubuntu-latest
    steps:
      - name: ✅ Run action.yml to verify all steps pass
        uses: open-source-crawler-test/repo-scan-test@main
        with:
          repository: ${{ env.repository }}
          typo-scan-exclude-match: '[''typos/**'', ''public/**'']'
          REPORT_ARCHIVE_OWNER: open-source-crawler-test
          REPORT_ARCHIVE_REPO: repo-scan-archive-test
          ARCHIVE_REPO_BRANCH_TARGET: main
          ARCHIVE_COMMIT_EMAIL: commit-bot@gmail.com
          ARCHIVE_REPO_ACCESS_TOKEN: ${{ secrets.PERSONAL_ACCESS_TOKEN }}
```