+++
title = "Syncing a fork in Github"
description = "Syncing a fork in Github"
tags = [
    "development",
    "git",
    "Github"
]
date = "2016-05-20"
categories = [
    "Development",
]

image = "empty.jpg" # optional
toc = true # optional, When set to TRUE this parameter, table of contents appears in only this article.
+++

Nowadays it’s essential to manage forks in [Github](https://github.com/) if you want to be a better programmer. Github is known worldwide and we must know at least how to use it.
A key concept in github is the word ‘fork’. When you create a fork based in an (open-source) interesting project from other people or organization, you are doing a copy of that, linked by github to his parent. Since this moment, the two projects will evolve independently.
The main reason to fork a project is to make new features or bug removals in your copy and then perform a ‘pull request’ to their father. Briefly, a pull request is a way to push changes in another project letting the owner in the other project to accept or discard these changes.
Of course it present a problem over time. If the father project is still developing new features and changes your fork must be updated in order to adquire these new changes and to avoid merge conflicts.
I will explain to you how to stay aligned with the original project in a few very simple steps.

By default, if you are using git you should know that you have the alias origin, which means your repository’s url, if more people are working in your project/fork probably you are using _git pull origin/master_ or just _git pull_ to get the new changes in your remote repository in your local machine. Now you will also need another one, I will name it _upstream_ following the main convention, but you can name it as you prefer.

Before all, you can check the list of your remote repositories already configured with

```bash
git remote -v
```
You should be seeing something like

```bash
origin  https://github.com/YOUR_USERNAME/YOUR_FORK.git (fetch)
origin  https://github.com/YOUR_USERNAME/YOUR_FORK.git (push)
```

which is your fork. To add another remote repository you should type this command

```bash
git remote add upstream https://github.com/ORIGINAL_OWNER/ORIGINAL_REPOSITORY.git
```
If the original repository were mine, I would type https://github.com/samuelmartingc/corbel-platform.github.io.git
Ok, now we can check again the list of our repositories with git remote -v and see that we have the new one too.

The next step is to check the new changes in the father repository, we can do it with the following command

```bash
git fetch upstream
```
Then go back to our branch master in which I am working

```bash
git checkout master
```
And finally perform the merge between both branches

```bash
git merge upstream/master
```
If you have no conflicts this will be an automatic step, otherwise you should fix the conflicts before finish.
At last but not least, you must remember to push the new changes in your branch to your remote repository with a simple _git push_.

I hope that you have enjoyed this post or, at least, you have found it useful.
Have a good day 🙂

Samuel Martin
