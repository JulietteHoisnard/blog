---
layout: post
title: "Why should you use Next.js?"
subtitle: "The tool to build your next application"
date: 2024-03-26 18:10:00 +0100
related_image: https://miro.medium.com/v2/resize:fit:646/1*gMiUPuRGC36nxZHe2zthOg.png
tags: [coding, tech]
---

If you are new to frontend development, Next.js is the most hyped framework, based on React, that you should use to build your next application. It was introduced in 2016 by Vercel, as an open-source framework, with the goal of enhancing performance, scalability and SEO-friendliness of React based applications.

Let's see in a few points what are these key ideas that Next.js brings on top of React:

1. It optimizes fonts and images rendering.
   Why do you need font optimization?
   Based on the principle of Core Web Vitals created at Google, which defines 3 core measurements (LCP, INP, and CLS),
   Why do you need images rendering optimization?
   Next.js comes with an Image component, as an extension of the html `<img>` tag, but which integrates automatic image optimization, such as:

- Preventing layout shift automatically when images are loading.
- Resizing images to avoid shipping large images to devices with a smaller viewport.
- Lazy loading images by default (images load as they enter the viewport).
- Serving images in modern formats, like WebP and AVIF, when the browser supports it.

2. It integrates a routing system with pages and layouts reusable across pages. It uses partial rendering thanks to this routing system, which means that on navigation, only the page components update while the layout won't re-render.

3.
