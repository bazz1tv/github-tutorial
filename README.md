# Managing Your Fork

Follow these instructions after you've forked this repository by pressing the "fork" button near the top-right of this browser page, and cloned your forked repo to your local PC (eg by using `git clone` with the cloning URL specified on your forked project page). Run the commands below from *somewhere* inside your local repo directory.

Note: When you clone a git repo, it is automatically associated with where you downloaded it from. This is through an actual git device called a "remote". Remotes are primarily used as simple labels for a complex GIT repo URL. The automatic remote you get when you clone a repo is called "origin". In this case, it will refer to your Github fork remote repo.

## Syncing Upstream

You will need to routinely make sure your local repo (and remote fork) are consistent with the progress being made on the main project. Here is how you can do that.

### Add Upstream Remote

You only need to do this once.

Let's add a remote to your local repo. It refers to the project's original remote repository (not your remote fork). We'll label it "upstream"

`git remote add upstream git://github.com/bazzinotti/github-tutorial.git`

_Note_: We could nitpick how I obtained the repo URL, or the protocol used (git://) -- but I am too tired at this point.
 
### Have Your Local Master Branch Track upstream/master

Since you are discouraged from making any changes to your fork's master branch - we will make your local master branch be directly tracked from the original repo's master branch (instead of your fork's)

`git branch master -u upstream/master`

### Syncing Your Fork

You won't need to do this immediately after cloning your repo. But generally, if more than a day has passed, or you know you need to update, you will want to sync up your master branch with "master repo" before you start a new branch.

#### Checkout the Master Branch
A typical behavior you should follow is to make sure you're in your master branch by typing `git branch` -- there will be an asterisk next to the active branch. If the master is not the active branch, then `git checkout master`. 

_Note_: If your local repo has uncommitted changes at this point in time, you will need to either finish committing them, or you may temporarily `git stash` them before checking out the master branch. You can later `git stash apply` to bring them back.

#### Fetch/Status/Pull
Now we are ready to sync to your local machine. You ought do this every time before creating a new branch (which will be based on the master). Do the following commands while inside your **master** branch.

```
git fetch
git status
```

Follow the advice printed from the status command (it varies). There may not be anything to update. You will probably be told to `git pull` if there are updates.

#### Push to Remote
`git push origin` pushes the local update to your fork's remote master branch (ie. on Github). 


## Creating a New Branch

This is what you'll do when you want to fix bug(s) or add a feature to the project. ALWAYS create a branch FROM the master (while the master is the active branch). See [Syncing your Fork](#Syncing Your Fork) for details on checking out the master branch.

`git checkout -b branchname` will create the new branch and make it the active branch.

You can now do work, add files, commit them as normal.

When you're ready to push your progress to your fork remote repo for the first time, you must also create the remote branch with some extra arguments to the push. `git push -u origin branchname`

All subsequent pushes can just use `git push` 

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

# Advanced Remarks

It's probably a good idea to have your fork master branch mirroring the original repo master branch, but it seems completely unnecessary. In fact, your local master branch alone is all that's required. But removing the remote master branch is a nuisance and requires another remote branch having been made, and is therefore discouraged for beginner users. That and, if anything _were_ to happen to the "master repo," at least you would have a copy in the fork if you maintained the remote master branch.