# Git Cheat Sheet

## Configuration

### Global

```console
git config --global user.name "Name Surname"
git config --global user.email "name.surname@example.com"
```

### For specific project

```console
git config user.name "Name Surname"
git config user.email "name.surname@example.com"
```

## Changing remote url

```console
git remote set-url origin https://github.com/USERNAME/REPOSITORY.git
```

Verify that the remote URL has changed.

```
git remote -v
```

## Changing the author of last commit to current settings

```console
git commit --amend --reset-author --no-edit
```

## Changing the author and name in existing commits

Change the name and/or email address in existing commits. It rewrite the entire history of your Git repository.

```console
git filter-branch --env-filter '
OLD_EMAIL="old@example.com"
NEW_NAME="New Name"
NEW_EMAIL="new@example.com"

if [ "$GIT_COMMITTER_EMAIL" = "$OLD_EMAIL" ]
then
    export GIT_COMMITTER_NAME="$NEW_NAME"
    export GIT_COMMITTER_EMAIL="$NEW_EMAIL"
fi
if [ "$GIT_AUTHOR_EMAIL" = "$OLD_EMAIL" ]
then
    export GIT_AUTHOR_NAME="$NEW_NAME"
    export GIT_AUTHOR_EMAIL="$NEW_EMAIL"
fi
' --tag-name-filter cat -- --branches --tags
```
## Removing sensitive data from git repository

```console
git filter-branch --force --index-filter \
  'git rm -r --cached --ignore-unmatch "$PATH_TO_SENSITIVE_DATA"' \
  --prune-empty --tag-name-filter cat -- --all
```

## Creating branch from given commit

Creating a branch

```console
git branch <branch-name> <sha1-of-commit>
```

Creating a switching to the branch

```console
git checkout -b <branch-name> <sha1-of-commit>
```

# Stash untracked files

```console
git add . # or specific file list
git stash --include-untracked # stash files
git stash pop # unstash files
```
