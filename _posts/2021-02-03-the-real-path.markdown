---
layout: post
title: "The right path"
subtitle: "How to find the right path for your image?"
date: 2021-02-03 15:26:56 +0100
related_image: https://images.unsplash.com/photo-1602924097911-a78ca1af38c6?ixid=MXwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=1318&q=80
tags: [coding]
---

- In the case where several files are referring to the same link, you have to provide an absolute path with `/` at the beginning for the reference at the root. See below:\
  \
   `src="/blog/assets/images/logo.png"`

- In the case where you want to use a path from a single file, you can use a relative path, with `../` targetting the parent folder:\
  \
   `src="../assets/images/logo.png"`

- In the case the targetted file is in the same folder, you can use:\
  \
   `src="./images/logo.png"`

Other types of paths to handle:

- In Ruby we can use **partials**. It can be scss or erb files. You can call a partial like this:\
  \
   `<%= render "menu" %>`\
   \
   and then the file named `_menu.html.erb` will be rendered (it should be available in the view folder).
  You can also call partial from inside another folder:\
   \
   `<%= render "shared/menu" %>`\
   \
   This will render the file here: `app/views/shared/_menu.html.erb`
