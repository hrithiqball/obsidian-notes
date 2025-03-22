```bash
git fetch
```

> pulls from remote repository to local machine without merging

```bash
git pull
```

> merge latest changes into local repository. this will overwrite the local repository changes

```bash
git add
```

> use `.` after add to add all files in current directory. or write specific files for stashing changes. the stashed changes can be used to store temporarily and commonly used for committing changes

```bash
git commit -m "use: git conventional here"
```

> commit the changes as one node to current branch. use the [[Git Conventional]](git conventional notes) to commit message

```bash
git push
```

> push committed changes to remote repository. this can either be tags, branch or even deleting branch on remote. `git push -uf origin main` will push to main branch on remote. `git push --tags` will push the tags into remote. `git push origin -d branch-name` will push the command to delete the branch in remote.

### Branch

```bash
git branch
```

> this command will list the branch available in local and what is the current branch being used in the current repository. adding new branch is the same command + name desired. for example, `git branch new-branch`. and to delete a branch locally, use `-d` flag to remove the branch for example `git branch -d new-branch`.

The best practice is when an issue is created during planning, create new branch from the issue. For an example, an issue about a button not working. The issue would be

1. button page login not working
   The branch that could be created from this is `1-button-page-not-working`. Once the branch is created on remote repository, git fetch the repository and checkout to the repository. Use this cli to checkout to new branch and pull immediately

```bash
git checkout -b 1-button-page-not-working
```

Check your current with the branch command to ensure we are currently working in an intended branch. Once the branch is confirmed, start developing only the part where it involves the specific button. Once it is fixed and documentation is written in issuer, stash all changes and commit with a meaningful message `fix(button): login page button not working`.

Push the changes to remote repository of the branch you are currently working. `git push origin 1-button-page-not-working`. Now in remote repository there are master or main branch and 1-button-page-not-working. Create a merge request or pull request and input why the merge is needed. If the changes is not enough requirement, go to local and fix what is needed first then commit and push again.

Finally, when the merge request is approved and reviewed, merge the issue branch into main/master branch.

---

- Make sure 1 big issue is 1 branch
- Make sure 1 small issue is 1 committed message
