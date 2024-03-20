---
layout: post
title: "Git branching"
subtitle: "Back to fundamentals"
date: 2024-03-20 18:10:00 +0100
related_image: https://images.unsplash.com/photo-1618401471353-b98afee0b2eb?q=80&w=2088&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D
tags: [coding, tech]
---

This is the second article about git fundamentals. It is largely inspired by the book ProGit, available for free on the [git documentation page](https://git-scm.com/book/en/v2).

Here we are focusing on branching!

1. **Merging**

Case A:
To merge a branch B into your current branch C using rebase in Git, you would follow these steps:
Make sure you are in the right branch (branch C):

```shell
 git checkout C
```

Rebase:

```shell
 git rebase B
```

Resolve any conflicts:

```shell
git rebase --continue
```

After resolving conflicts (if any) and completing the rebase, you can push the changes to the remote repository if necessary:

```shell
git push origin C --force
```

Be cautious when using --force as it will overwrite the history of the remote branch C.
Be aware that using rebase can rewrite the commit history, so it's important to communicate with your team if you're working on a shared branch.
