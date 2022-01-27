# How to change last commit message

If the commit it is not pushed to remote yet, use the following `amend` command.

```
git commit --amend -m "New commit message."
```

But if the commit was already pushed to remote, it is needed to force the `push` because the old commit SHA will not exist anymore, it will be overwritten

```
git commit --amend -m "New commit message."
git push --force <remoteName> <branchName>
```
