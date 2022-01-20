# How to perform empty commit

Empty commit is sometimes necessary to trigger something based on commit or to just test permissions.

```
git commit --allow-empty -m "Commit with empty content" && git push
```