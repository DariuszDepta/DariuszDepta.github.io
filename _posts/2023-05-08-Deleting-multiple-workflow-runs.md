# Deleting multiple workflow runs in GitHub

## Step 1

Install GitHub CLI:
```shell
$ sudo dnf install gh
```
## Step 2

Login to GitHub account:
```shell
$ gh auth login
```

## Step 3

Save the bash code to file, make it executable, replace placeholders with proper values and run.  
```shell
#!/usr/bin/env bash

# number of most recent workflows to be preserved (not deleted)
SKIP=_place_the_number_of_workflow_runs_to_be_skipped_

# name of the github account 
GITHUB_OWNER=_place_your_GitHub_user_account_here_

# name of the repository
GITHUB_REPOSITORY=_place_GitHub_repository_name_here_

function delete_workflow_run() {
  gh api --method DELETE \
         -H "Accept: application/vnd.github+json" \
         -H "X-GitHub-Api-Version: 2022-11-28" \
         /repos/$GITHUB_OWNER/$GITHUB_REPOSITORY/actions/runs/$1
}

gh api -H "Accept: application/vnd.github+json" \
       -H "X-GitHub-Api-Version: 2022-11-28" \
       /repos/$GITHUB_OWNER/$GITHUB_REPOSITORY/actions/runs?per_page=100 \
| jq -r '.workflow_runs[] | [.updated_at, .id] | @tsv' \
| sort -r -k 1 \
| tail -n "+$((SKIP + 1))" \
| awk '{print $2}' \
| while read -r RUN_ID ; do
    delete_workflow_run "$RUN_ID";
  done
```