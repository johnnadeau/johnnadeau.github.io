---
layout: post
title: "Some Quick Git Tips I Wish I Knew Years Ago..."
date: 2017-04-21 09:43
published: true
tags: git vim code tips
comments: true
---

I was looking through some old material and I found some git tips I presented at the the [Haverhill
Hackers Meetup][hhmu] during one of the "lighting talks" meetups. I originally put them in a
[gist][gist], but feel it would be helpful to others to post here. Enjoy!

## Alias `git` and common commands
- at a minimum, alias `g="git"`, it's a tool you use all the time save those keystrokes!
- go further, alias common commands: `ga="git add"`, `gst="git status"`, `gc="git commit"`, etc
- if you use `zsh`, the `oh-my-zsh`configuration framework has _tons_ of aliases for git(and other
- things) if you don't want to take a whole framework, you can checkout the aliases it sets here
    [https://github.com/robbyrussell/oh-my-zsh/wiki/Cheatsheet#git](https://github.com/robbyrussell/oh-my-zsh/wiki/Cheatsheet#git)

## Use `git stash` or _WIP_ commit messages when changing branches
- `git stash` is a quick way to just put some changes to the side when you need to change the focus
    of your work
- if you're already on your own branch, nothing is stoping you from creating a commit with these
    changes and noting its _WIP_
- if you go with the _WIP_ commit message remember to `reset` or `amend` that commit so your
    commmit message can mean something

## Setup your `.gitconfig` to use a personal email address(even at work)
- [https://help.github.com/articles/setting-your-email-in-git/](https://help.github.com/articles/setting-your-email-in-git/)
    (applies to bitbucket as well)
- Why?
- open source commits will no longer show up for your (GitHub/BitBucket/etc) account if you don't
    have access to that email
- if you leave that job, future developers have a path to contact you if the need arise
- if that bothers you, at least set it globally to your personal email and then change the local
    config per project to be your work email

## Use a global `.gitignore`
- put common OS related files that get generated in here
- put common language/framework/tool related files that get generated
- do this in addition to local a ignore file because you have the added protection of not
    commiting garbage that other developers may have missed if they setup the ignore file

## Try out `git` plugins for your IDE or text editor of choice
- most _should_ have a plugin for git commands or at a minimum to show that a line has changed in
    the git history
- I use vim + vim-fugitive -
- [https://github.com/tpope/vim-fugitive](https://github.com/tpope/vim-fugitive)
- I mostly use it for `git diff` and `git blame` with quick shortcuts to access them

## Bonus
- store your `.gitconfig` and `.gitignore` in source control(hopefully with your other _dotfiles_)
- check out `git rebase` if you like that style of working with commit history
- create custom commands by adding them to your git config like this nifty command to remove a
    branch locally and remotely: `nuke-branch = !sh -c 'git branch -D $1 && git push origin :$1' -`


[hhmu]: http://www.meetup.com/haverhillhackers/
[gist]: https://gist.github.com/johnnadeau/e49eb2769d55a99912de352e8c69587c
