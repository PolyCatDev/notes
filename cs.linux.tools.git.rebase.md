
Git rebase is used to rewrite commits above a specific base commit.


## Rebase default mode

The default mode takes all the new commits on your current branch, puts them aside, pulls in all commits from specified branch and then reapplies your commits one by one.

```sh
git rebase <branch-name>
```

> This will pull in all commits from specified branch and reapply your commits one by one.

### Handling merge conflicts

1. If a merge conflict is encountered the rebase will stop.
2. Manually go and resolve the conflicts.
3. Add changed files staging using `git add <file-path>`.
4. Run `git rebase --continue` to continue the rebase.
5. If a new merge conflict happens, repeat steps 1 thru 4.


## Rebase interactive mode

Interactive mode edits all commits above a specific commit using your configured text editor.

```sh
git rebase -i <commit-hash>
```

> This will open a buffer with all commits above the commit hash provided in your configured text editor.

> In this buffer, you can do all the actions documented lower in the buffer and also rearrange the order of commits by changing the order of the commits at the top.

