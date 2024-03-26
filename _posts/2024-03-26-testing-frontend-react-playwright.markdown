---
layout: post
title: "Testing with Playwright"
subtitle: "The art of testing"
date: 2024-03-26 18:10:00 +0100
related_image: https://miro.medium.com/v2/resize:fit:646/1*gMiUPuRGC36nxZHe2zthOg.png
tags: [coding, tech]
---

1. How to set up Playwright in your React application?

```shell
Run npm init playwright@latest
```

Run the install command and select the following to get started:

Choose between TypeScript or JavaScript (default is TypeScript)
Name of your Tests folder (default is tests or e2e if you already have a tests folder in your project)
Add a GitHub Actions workflow to easily run tests on CI
Install Playwright browsers (default is true)

You can run the tests (installed by default):

```shell
npx playwright test
```

You can run it also in the UI: (AMAZING FEATURE)

```shell
npx playwright test --ui
```

If you have snapshots to be updated:

```shell
npx playwright test --update-snapshots or -u
```

2. Good practices

Use snapshots and or screenshots!! It will save you a crazy amount of time.

Use screen recording: for this you need to install the extension in Visual Code Studio. It will save you a crazy amount of time.

Use the data-testid="string" attribute to reach the items you want to test easily and faster. Indeed, it improves the test reliability, it is easier to locate the element in the UI and there is a separation of concerns between the tests attributes and the running application. It helps to document the purpose of each element.

Try to test as much as possible things which are independant from your database content. Then the tests are reliable and strong.

3. Screenshot testing VS snapshot testing.

What is the difference between screenshot and snapshot testing?
Screenshot: Create a screenshot of the UI and save it. Screenshot testing is a type of snapshot testing.
Snapshot: Snapshot can be that you save just the text for example, and check the difference. It can be also that you generate JSON data structure of the UI to compare. It can be a screenshot.

4. Cannot easily set the tests in the CI/CD pipeline?

You can use tools to do Pre-Commit Hooks to make sure that we run the tests anytime someone pushes on the frontend folder. For example you can use [Husky](https://typicode.github.io/husky/), which will help you to format, lint and test before you commit or push (you do the setup of your choice).
