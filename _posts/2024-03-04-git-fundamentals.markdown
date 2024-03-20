---
layout: post
title: "Git essentials"
subtitle: "Back to fundamentals"
date: 2024-03-12 18:10:00 +0100
related_image: https://images.unsplash.com/photo-1477949331575-2763034b5fb5?q=80&w=2070&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D
tags: [coding, tech]
---

I am using a lot the Source Control UI of Visual Code Studio and feel stupid not to know all the secrets of git, plus it seems to be more handy to use the command line with complex cases, so here is my take on the git commands and tricks that are essentials for you to know!

1. **Git commit**
   When you only write

```shell
git commit
```

without the -m

```shell
git commit -m
```

you are in VIM, in escape mode. You then need to start insert mode to write. The simplest way is to type i, and a message will appear on the bottom (-- INSERT --). You are in insert mode and you can now type in your message.

After that, you must exit insert mode, and you do that by pressing Esc once. The -- INSERT -- message on the bottom should vanish. You are now in escape mode again, and you must save and quit.

That is done by using the : key to enter command mode and typing the command wq or x, leaving you with either :wq or :x typed at the bottom.

w stands for write and q for quit, so wq is write and quit. x is an alias for wq.

So you write :wq and you just press Enter and you're done, out of VIM.

To change the editor to something different run the following command (eg. for vim):

```shell
git config --global core.editor "vim"
```

To have a comment done in Visual Studio Code you can run:

```shell
git config core.editor "code --wait"
```

2. **Undoing things**

I found the Git documentation pretty confusing about undoing things, so here is my attempt to make it clearer:

Case A: You just committed and forgot a file or you want to change the commit message.

```shell
git commit --amend
```

If you staged nothing in between (between your commit and the git commit --amend), you will lend on the "change commit message" part.
If you staged another file, fileB, then it will replace the initial commit with the fileB added inside the commit. You will see only 1 commit in the git graph.

Case B: You have some staged stuff and you want to send it back to the "modified" / "changes" state
For all the files in staged:

```shell
git reset .
```

or for a particular file:

```shell
git reset file_name
```

Case C: git restore, git checkout and git switch

Case D: If you want to remove the last commits of a branch and set it back to the state of a previous commit:

```shell
 git reset --hard sha1
```

3. **Working with remotes**

If you git clone a repo from Github for example, you will
If you’ve cloned a repository (by running git clone), and then run

```shell
 git remote
```

you should at least see origin — that is the default name Git gives to the server you cloned from.
If you run

```shell
 git remote -v
```

you can see the URLs that Git has stored for the shortname to be used when reading and writing to that remote.

You can add a remote:

```shell
git remote add <shortname> <url>
```

For example you add this git remote add pb https://github.com/paulboone/ticgit, now you can run git fetch pb, it accessible locally for your machine.

Why do we need several remotes? For example:

- if the project is hosted on GitHub and GitLab.
- If we deploy in prod via git, we save on GitHub and we push on prod.
- If we want to clone a repo in local on my computer, in another folder.

If you want to see more information about a particular remote, you can use the <span style="color:red">git remote show <remote></span> command.

You can rename <span style="color:red">git remote rename pb paul</span> or remove a remote <span style="color:red">git remote remove paul</span>. Now if you run git remote, there is only origin left.

4. **Tagging**

List tags:

```shell
 git tag
 OR
 git tag -l
 OR
 git tag -l "v1.8.5*"
```

Creating tags:

```shell
 git tag
 OR
 git tag -l
 OR
 git tag -l "v1.8.5*"
```

5. **Aliasing**
   Most used aliases:

```shell
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.st status
```
