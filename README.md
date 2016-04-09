# Managing Your Fork
## Syncing with Upstream
### Add Upstream Remote
`git remote add upstream git://github.com/bazzinotti/github-tutorial.git`
### Have Your Local Master Branch Track upstream/master
`git branch master -u upstream/master`
### Syncing Your Fork

First you must sync to your local machine. You ought do this before branching a new feature request.

```
git fetch
git status
```

Follow the advice printed from the status command. There may not be anything to update.

If you _did_ get updates, you should push these local updates to your remote fork now.

`git push origin` pushes the local update to your fork's remote master branch on (ie. Github).

## Pull Request
See this [recorded livestream](https://www.youtube.com/watch?v=wFck6txFeck&t=26m42s)

# Check Remote Tracking for All Branches
```
$ gitb -vv
  a      cabf6d8 [origin/a] [a] w capitalized
  b      8af3e75 [origin/b] [b] did a thing again
* master 8527a00 [upstream/master] derp
```

# Undoing a commit
`git reset HEAD~1` Where 1 is the number of commits to remove.

Alternatively, you can use a commit hash to reset to (a hash could be obtained from `git log`)

Normally, a reset to another commit will retain any added files or file modifications that were present. If you desire to remove these changes automatically, you add the `--hard` flag, ie `git reset --hard HEAD~`

# Rephrasing Commits

## Most Recent Commit
`git commit --amend`
## Several Commits
`git rebase -i HEAD~5` 

In this example, `HEAD~5` specifies the bottom-most commit (5 past commits), which combined with the HEAD will provide a range of commits from which to work with.

This does not mean you will be re-editing 5 commits, but actually your text editor will open with some text based on the range of commits. Replace 'pick' of each commit you want to reword with 'r' -- Save and close the file --and then you will reword only the commits you've specified.

You can alternatively use a commit hash to specify the bottom commit of the commit-range.