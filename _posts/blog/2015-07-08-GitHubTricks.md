---
layout: post
title: GitHub Tricks
link: 
link-alt: 
date: 2015-07-08
category: blog
description: Useful commands for my everyday GitHub life
tags: [blog,how to,tutorial,github,git,tips and tricks]
article: yes

---

# Contents
{:.no_toc}

* This line will be replaced by the ToC, excluding the "Contents" header
{:toc}

# Branching

## Create a new branch

### Create a new branch from scratch and push it to the remote repo

Before creating a new branch pull the changes from upstream, since your master needs to be up to date. Create the branch on your local machine and switch in this branch :

{% highlight bash %}
git checkout -b [name_of_your_new_branch]
{% endhighlight %}

Push the branch on github :

{% highlight bash %}
git push origin [name_of_your_new_branch]
{% endhighlight %}

When you want to commit something in your branch, be sure to be in your branch. You can see all branches created by using `git branch`.

### Create a new local branch and make it track the remote branch that was already there

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

## Merge a branch into master

### Unsafely (but it works 90% of the times)
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

### Safely

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

But in this way you will lose the changelogs in the test branch. Solution is, use `rebase` instead of `merge` (IF we have solved the branches conflicts). Please refer to [http://git-scm.com/book/en/v2/Git-Branching-Rebasing](http://git-scm.com/book/en/v2/Git-Branching-Rebasing) for further info.

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

#### IMPORTANT

The only thing you need to avoid is: **never use `rebase` on `master` branch!** I.e. never do this:

{% highlight bash %}
git checkout master
git rebase -i test
{% endhighlight %}

## Delete a remote/local branch or tag

### Delete a branch
Assuming that yours is a branch called `bugfix`, you have to do the following:
 
 * locally: `git branch -D bugfix`
 * remotely: `git push origin :bugfix`

### Delete a tag

If you want to delete a local tag then you would do `git tag -d <tag name>` (as you did with the branch). But if you want to delete remote tag, then the syntax is a little different:
{% highlight bash %}
$ git push origin :refs/tags/<tag name>
{% endhighlight %}
This will delete the tag on the remote origin.

## Copy files between branches

To copy a file from one branch to another, e.g. from the `experiment` branch to the `master` branch,

{% highlight bash %}
git checkout master                 # get back to master
git checkout experiment -- file.txt # copy the version of the file from "experiment"
{% endhighlight %}

# Remote URLs

## List existing remote URL

In order to get the name of the remote URL, you need to do the following:

{% highlight bash %}
$ git remote -v
origin  https://github.com/USERNAME/REPOSITORY.git (fetch)
origin  https://github.com/USERNAME/REPOSITORY.git (push)
{% endhighlight %}

## Change remote URL from HTTPS to SSH

In order to go from `HTTPS` to `SSH`, you need to use the `remote set-url` command:

{% highlight bash %}
$ git remote set-url origin git@github.com:USERNAME/REPOSITORY.git
{% endhighlight %}

## Change remote URL 

The same command is used to point your repository to another remote:

{% highlight bash %}
$ git remote set-url origin git@github.com:USERNAME/OTHERREPOSITORY.git
{% endhighlight %}

## Configuring a remote for a fork

To sync changes you make in a fork with the original repository, you must configure a remote that points to the upstream repository in Git. To do so, you need to specify a new remote upstream repository that will be synced with the fork:

{% highlight bash %}
$ git remote add upstream https://github.com/ORIGINAL_OWNER/ORIGINAL_REPOSITORY.git
{% endhighlight %}

{% highlight bash %}
$ git remote -v
origin    git@github.com:USERNAME/REPOSITORY.git
origin    git@github.com:USERNAME/REPOSITORY.git
upstream  https://github.com/ORIGINAL_OWNER/ORIGINAL_REPOSITORY.git (fetch)
upstream  https://github.com/ORIGINAL_OWNER/ORIGINAL_REPOSITORY.git (push)
{% endhighlight %}

# Forks

## Syncing a fork

Syncing a fork of a repository aims at keeping it up-to-date with the upstream repository. 
Before you can sync your fork with an upstream repository, you must configure a remote that points to the upstream repository in Git.

Then, you need to fetch the branches and their respective commits from the upstream repository. Commits to master will be stored in a local branch, `upstream/master`:

{% highlight bash %}
$ git fetch upstream
remote: Counting objects: 75, done.
remote: Compressing objects: 100% (53/53), done.
remote: Total 62 (delta 27), reused 44 (delta 9)
Unpacking objects: 100% (62/62), done.
From https://github.com/ORIGINAL_OWNER/ORIGINAL_REPOSITORY
 * [new branch]      master     -> upstream/master
{% endhighlight %}

Check out your fork's local master branch:

{% highlight bash %}
$ git checkout master
Switched to branch 'master'
{% endhighlight %}

Merge the changes from upstream/master into your local master branch. This brings your fork's master branch into sync with the upstream repository, without losing your local changes.

{% highlight bash %}
$ git merge upstream/master
Updating a422352..5fdff0f
Fast-forward
 README                    |    9 -------
 README.md                 |    7 ++++++
 2 files changed, 7 insertions(+), 9 deletions(-)
 delete mode 100644 README
 create mode 100644 README.md
{% endhighlight %}

If your local branch didn't have any unique commits, Git will instead perform a "fast-forward":

{% highlight bash %}
$ git merge upstream/master
Updating 34e91da..16c56ad
Fast-forward
 README.md                 |    5 +++--
 1 file changed, 3 insertions(+), 2 deletions(-)
{% endhighlight %}

# Stashing your work

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

# Switch to a different commit back in time

## Temporarily switch
In order to temporarily go back to a previous commit, fool around, then come back to the master, all you have to do is check out the desired commit:

{% highlight bash %}
git checkout 0d1d7fc32
{% endhighlight %}

This will detach your HEAD, that is, leave you with no branch checked out.

## Branch out from that commit

In order to make commits from that commit, a new branch is needed:

{% highlight bash %}
git checkout -b old-state 0d1d7fc32
{% endhighlight %}

# Hard delete commits

To get rid of everything you've done since then, there are two possibilities. 

## Hard delete unpublished commits

If those commits have not been published yet, simply reset:

{% highlight bash %}
git reset --hard 0d1d7fc32
{% endhighlight %}

This will destroy any local modifications. *Don't do it if you have uncommitted work you want to keep.*

Alternatively, if there's work to keep:

{% highlight bash %}
git stash
git reset --hard 0d1d7fc32
git stash pop
{% endhighlight %}

This saves the modifications, then reapplies that patch after resetting. You could get merge conflicts, if you've modified things which were changed since the commit you reset to. If you mess up, you've already thrown away your local changes, but you can at least get back to where you were before by resetting again.

## Undo published commits with new commits

On the other hand, if you've published the work, you probably don't want to reset the branch, since that's effectively rewriting history. In that case, you could indeed revert the commits. With `git`, revert has a very specific meaning: create a commit with the reverse patch to cancel it out. This way you don't rewrite any history.

This will create three separate revert commits:

{% highlight bash %}
git revert a867b4af 25eee4ca 0766c053
{% endhighlight %}

It also takes ranges. This will revert the last two commits:

{% highlight bash %}
git revert HEAD~2..HEAD
{% endhighlight %}

Reverting a merge commit

{% highlight bash %}
git revert -m 1 <merge_commit_sha>
{% endhighlight %}

To get just one, you could use `rebase -i` to squash them afterwards. Or, you could do it manually (be sure to do this at top level of the repo) get your index and work tree into the desired state, without changing HEAD:

{% highlight bash %}
git checkout 0d1d7fc32 .
{% endhighlight %}

Then commit. Be sure and write a good message describing what you just did!

{% highlight bash %}
git commit
{% endhighlight %}

The [`git-revert` manpage](http://schacon.github.io/git/git-revert.html) actually covers a lot of this in its description. Another useful link is this [git-scm.com blog post](http://git-scm.com/blog/2010/03/02/undoing-merges.html) discussing `git-revert`.
If you decide you didn't want to revert after all, you can revert the revert (as described here) or reset back to before the revert (see the previous section).

# Tagging

Like most VCSs, Git has the ability to tag specific points in history as being important. Typically people use this functionality to mark release points (`v1.0`, and so on).
Listing the available tags in Git is straightforward. Just type `git tag`:

{% highlight bash %}
$ git tag
v0.1
v1.3
{% endhighlight %}

This command lists the tags in alphabetical order; the order in which they appear has no real importance.

## Creating annotated tags

Creating an annotated tag in Git is simple. The easiest way is to specify `-a` when you run the tag command:

{% highlight bash %}
$ git tag -a v1.4 -m 'my version 1.4'
$ git tag
v0.1
v1.3
v1.4
{% endhighlight %}

The `-m` specifies a tagging message, which is stored with the tag. If you don't specify a message for an annotated tag, Git launches your editor so you can type it in. You can see the tag data along with the commit that was tagged by using the `git show` command:

{% highlight bash %}
$ git show v1.4
tag v1.4
Tagger: Ben Straub &lt;ben@straub.cc&gt;
Date:   Sat May 3 20:19:12 2014 -0700

my version 1.4

commit ca82a6dff817ec66f44342007202690a93763949
Author: Scott Chacon &lt;schacon@gee-mail.com&gt;
Date:   Mon Mar 17 21:52:11 2008 -0700

    changed the version number
{% endhighlight %}

That shows the tagger information, the date the commit was tagged, and the annotation message before showing the commit information.

### Creating annotated tags for past commits

{% highlight bash %}
git tag -a v1.2 9fceb02 -m "Message here"
{% endhighlight %}

Where `9fceb02` is the beginning part of the commit id. You can then push them up using 

## Pushing tags

By default, the git push command doesn't transfer tags to remote servers. You will have to explicitly push tags to a shared server after you have created them. This process is just like sharing remote branches - you can run `git push origin [tagname]`:
{% highlight bash %}
git push origin v1.5
{% endhighlight %}

If you have a lot of tags that you want to push up at once, you can also use the --tags option to the git push command. This will transfer all of your tags to the remote server that are not already there.
{% highlight bash %}
git push --tags origin master
{% endhighlight %}

Now, when someone else clones or pulls from your repository, they will get all your tags as well. Here is [a good chapter on tagging](http://git-scm.com/book/en/v2/Git-Basics-Tagging).

# Merging and Rebasing

In Git, there are two main ways to integrate changes from one branch into another: the `merge` and the `rebase`.
Let us assume that we have this setup, in which `experiment` branch has diverged from `master`:

{% include image.html exturl="https://git-scm.com/book/en/v2/book/03-git-branching/images/basic-rebase-1.png" description="Simple divergent history" %}

The easiest way to integrate the branches is the `merge` command. It performs a three-way merge between the two latest branch snapshots (`C3` and `C4`) and the most recent common ancestor of the two (`C2`), creating a new snapshot (and commit).

{% include image.html exturl="https://git-scm.com/book/en/v2/book/03-git-branching/images/basic-rebase-2.png" description="Merging to integrate diverged work history" %}

However, you can also `rebase`: you can take the patch of the change that was introduced in `C4` and reapply it on top of `C3`. With the `rebase` command, **you can take all the changes that were committed on one branch and replay them on another one**.

In this example, you'd run the following:

{% highlight bash %}
$ git checkout experiment
$ git rebase master
First, rewinding head to replay your work on top of it...
Applying: added staged command
{% endhighlight %}

It works by going to the common ancestor of the two branches (the one you're on and the one you're rebasing onto), getting the diff introduced by each commit of the branch you're on, saving those diffs to temporary files, resetting the current branch to the same commit as the branch you are rebasing onto, and finally applying each change in turn.

{% include image.html exturl="https://git-scm.com/book/en/v2/book/03-git-branching/images/basic-rebase-3.png" description="Rebasing the change introduced in C4 onto C3." %}

At this point, you can go back to the master branch and do a fast-forward merge.

{% highlight bash %}
$ git checkout master
$ git merge experiment
{% endhighlight %}

{% include image.html exturl="https://git-scm.com/book/en/v2/book/03-git-branching/images/basic-rebase-4.png" description="Fast-forwarding the master branch." %}

Now, the snapshot pointed to by `C4'` is exactly the same as the one that was pointed to by `C5` in the merge example. There is no difference in the end product of the integration, but **rebasing makes for a cleaner history**. If you examine the log of a rebased branch, it looks like a linear history: it appears that all the work happened in series, even when it originally happened in parallel.

Often, you'll do this to make sure your commits apply cleanly on a remote branch – perhaps in a project to which you're trying to contribute but that you don't maintain. In this case, you'd do your work in a branch and then rebase your work onto origin/master when you were ready to submit your patches to the main project. That way, **the maintainer doesn't have to do any integration work – just a fast-forward or a clean apply**.

## How to play with different branches

Sometimes, it might just be not possible to either merge or rebase two branches. In this context, the commands listed below might come useful:

{% highlight bash %}
$ git diff --name-status master..experimental     # this lists the files that have diffs between the two branches
$ git difftool master experimental -- filename    # this opens a difftool viewer (in my case, Meld), to analyze the diff between a file in two different branches 
{% endhighlight %}

To pick a file from the `master` branch and move it into the `experimental` branch:

{% highlight bash %}
$ git checkout experimental
$ git checkout master -- modules/virtualContactGeneration/
{% endhighlight %}

# Ignore tracked files

In most projects/repositories, there are some files whose default version is important to track, but that change very often and whose change is machine dependent (e.g. configuration files) or is a consequence of automatic change while building the code. Usually, you don't want to un-track them, you just don't want them to appear as modified and you don't want them to be staged when you `git add`. The command is the following:

{% highlight bash %}
git update-index --assume-unchanged [<file> ...]
{% endhighlight %}

Git will fail (gracefully) in case it needs to modify this file in the index e.g. when merging in a commit; thus, in case the assumed-untracked file is changed upstream, you will need to handle the situation manually.

Importantly, in order to undo the previous command and start tracking again, use:

{% highlight bash %}
git update-index --no-assume-unchanged [<file> ...]
{% endhighlight %}

## What if I forgot what files were untracked?

You can use `git ls-files -v`. If the character printed is lower-case, the file is marked assume-unchanged.

To print just the files that are unchanged use:

{% highlight bash %}
git ls-files -v | grep '^[[:lower:]]'
{% endhighlight %}

To embrace your lazy programmer, turn this into a git alias. Edit your `.gitconfig` file to add this snippet:

{% highlight bash %}
[alias]
    ignored = !git ls-files -v | grep "^[[:lower:]]"
{% endhighlight %}

Now typing `git ignored` will give you output like this:

{% highlight bash %}
h path/to/ignored.file
h another/ignored.file
{% endhighlight %}

