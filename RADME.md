# Git Cheat Sheet

## Change the author and name in existing commits

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