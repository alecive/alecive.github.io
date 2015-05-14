---
layout: post
title: GitHub Tricks
link: https://github.com/alecive/periPersonalSpace
link-alt: Sublime Website
date: 2015-05-07
category: blog
description: 
article: yes

---

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
git remote -v
# Verify new remote URL
# origin  git@github.com:USERNAME/OTHERREPOSITORY.git (fetch)
# origin  git@github.com:USERNAME/OTHERREPOSITORY.git (push)
{% endhighlight %}
