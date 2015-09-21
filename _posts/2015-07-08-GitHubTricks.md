---
layout: post
title: GitHub Tricks
link: 
link-alt: 
date: 2015-07-08
category: blog
description: Useful commands for my everyday GitHub life
article: yes

---

# Contents
{:.no_toc}

* This line will be replaced by the ToC, excluding the "Contents" header
{:toc}

# Create a new branch

## Create a new branch from scratch and push it to the remote repo

Before creating a new branch pull the changes from upstream, since your master needs to be up to date. Create the branch on your local machine and switch in this branch :

{% highlight bash %}
git checkout -b [name_of_your_new_branch]
{% endhighlight %}

Push the branch on github :

{% highlight bash %}
git push origin [name_of_your_new_branch]
{% endhighlight %}

When you want to commit something in your branch, be sure to be in your branch. You can see all branches created by using `git branch`.

## Create a new local branch and make it track the remote branch that was already there

`git branch -a` will list all of the remote branches that are available to pull from the repo, e.g.:

{% highlight bash %}
[alecive@malakim]$ git branch -a
* master
  remotes/origin/HEAD -> origin/master
  remotes/origin/features/redball-shanghai
  remotes/origin/gh-pages
  remotes/origin/master
{% endhighlight %}

To create a new repo and make it track one of the listed branches, simply type:

{% highlight bash %}
[alecive@malakim]$ git checkout -b features/redball-shanghai origin/features/redball-shanghai
{% endhighlight %}

A `git pull` should not be necessary.

# Merge a branch into master

## Unsafely (but it works 90% of the times)
This is one very practice question, but all before answers are not practical.

{% highlight bash %}
git checkout master
git pull origin master
git merge test
git push origin master
{% endhighlight %}

Two issues arise:

 1. Not safe because we don't know if there are any conflicts between test branch and master branch
 2. it would "squeeze" all test commits into one merge commit on master: on master branch, we can't see the all the changelogs of test branch

## Safely

{% highlight bash %}
git checkout test
git pull 
git checkout master
git pull
git merge --no-ff --no-commit test
{% endhighlight %}

The latest command tests the merge merge before committing, and avoids a fast-forward commit by `--no-ff`; if conflicts appear, we can run `git status` to check details about the conflicts and try to solve them.
Once we solve the conflicts, or there are no conflicts at all, we can commit and push them:

{% highlight bash %}
git commit -m 'merge test branch'
git push
{% endhighlight %}

But in this way you will lose the changelogs in the test branch. Solution is, use `mebase` instead of `merge` (IF we have solved the branches conflicts). Please refer to http://git-scm.com/book/en/v2/Git-Branching-Rebasing for further info.

{% highlight bash %}
git checkout master
git pull
git checkout test
git pull
git rebase -i master
git checkout master
git merge test
{% endhighlight %}

The major benefit of rebasing is that you get a much cleaner project history.

### IMPORTANT

The only thing you need to avoid is: **never use `rebase` on `master` branch!** I.e. never do this:

{% highlight bash %}
git checkout master
git rebase -i test
{% endhighlight %}

# Delete a branch both locally and remotely

Assuming that yours is a branch called `bugfix`, you have to do the following:
 
 * locally: `git branch -D bugfix`
 * remotely: `git push origin :bugfix`

# Change remote URL

1) List your existing remotes in order to get the name of the remote you want to change.

{% highlight bash %}
git remote -v
# origin  git@github.com:USERNAME/REPOSITORY.git (fetch)
# origin  git@github.com:USERNAME/REPOSITORY.git (push)
{% endhighlight %}

2) Change your remote's URL from SSH to HTTPS with the remote set-url command.

{% highlight bash %}
git remote set-url origin git@github.com:USERNAME/OTHERREPOSITORY.git
{% endhighlight %}

3) Verify that the remote URL has changed.

{% highlight bash %}
$ git remote -v
# Verify new remote URL
# origin  git@github.com:USERNAME/OTHERREPOSITORY.git (fetch)
# origin  git@github.com:USERNAME/OTHERREPOSITORY.git (push)
{% endhighlight %}

# `git stash` - Stashing your work

`git stash` does the following:

 1. Saves your working directory and index to a safe place.
 2. Restores your working directory and index to the most recent commit.

You can then work on other branches, make commits, etc. and when you're ready to get back to where you were, you type git stash pop and you're back, working at full speed.

## Example: Working Normally

Before you start git stashing, make sure any new files added to the working directory have been added to the index: git stash will not stash (save) files in the working directory unless the files are being tracked (some version of the file has been added to the index).

Let's create a repository, add a file, and make the first commit:

{% highlight bash %}
$ git init
Initialized empty Git repository ...
$ echo This is the README file. > README
$ git add README
$ git commit -m'Initial commit'
[master (root-commit) 35ede5c] Initial commit
 1 files changed, 1 insertions(+), 0 deletions(-)
 create mode 100644 README
{% endhighlight %}

Next we'll make some changes to the working directory:

 * i) add a line to `README`
 * ii) dd a new file, `file2`

{% highlight bash %}
$ echo ADD TO THE WORKING DIRECTORY VERSION OF README >> README
$ echo file2 is here > file2
$ ls
file2  README
{% endhighlight %}

### We Get Interrupted

Now we find out about the bug we need to fix in another branch. Our goal is to stash (save) the changes that we had made to the working directory, go to the other branch and then eventually return to right before we heard about that bug.

We first need to add the new file, `file2`, to the index, so git will track the file and know to save the file during the git stash:

{% highlight bash %}
$ git add file2
{% endhighlight %}

We don't need to add `README` to the index since that file path was already in the index: Git will notice that the working directory version is newer than the index and will stash it. Now we're ready for the stashing:

{% highlight bash %}
$ git stash
Saved working directory and index state WIP on master: 8d8b865 Initial commit
HEAD is now at 8d8b865 Initial commit
$ ls
README
$ cat README
This is the README file.
{% endhighlight %}

By doing so, the changes we had made to the working directory, are squirreled away somewhere to somewhere safe. Further, the working directory is set back to its state before the modifications were made. In particular: `file2` was removed, and the `README` no longer has the second line.

### Work On Another Branch or Two

Now we can do anything we want, such as git checkout other-branch, make modifications, fix bugs, and commit the fix to that branch. When we're ready to continue where we left off, we simply type `git stash pop` and our "stashed" working directory is back where it was when we had typed `git stash`:

{% highlight bash %}
$ git stash pop
# On branch master
# Changes to be committed:
#   (use "git reset HEAD ..." to unstage)
#
#   new file:   file2
#
# Changed but not updated:
#   (use "git add ..." to update what will be committed)
#   (use "git checkout -- ..." to discard changes in working directory)
#
#   modified:   README
#
Dropped refs/stash@{0} (9c72eaeebdb712ad527f06f88a5cbec1098957f1)
$ ls
file2  README
$ cat README
This is the README file.
ADD TO THE WORKING DIRECTORY VERSION OF README
{% endhighlight %}

