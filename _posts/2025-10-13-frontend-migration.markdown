---
layout: post
title: "Migrating from AngularJS to React"
subtitle: "Insights and lessons learned"
date: 2025-10-13 12:22:00 +0100
related_image: /blog/assets/images/migration-image.jpg
tags: [coding, tech]
---

Every legacy migration faces a choice: a big-bang rewrite or a gradual transition. When at Netlight we helped a major German accounting company migrate from AngularJS to React, we discovered that one of the biggest challenge alongside the old codebase upgrade was the organizational challenge. This is the story of how we navigated that complexity.

# Why do a migration

Generally speaking, a company needs to do a migration when they see the needs to move to a more modern system, whether it is a cloud migration or a frontend migration. Indeed, in the case of a cloud migration, it can be a pivotal step for businesses striving to stay competitive and innovative in today’s fast-evolving digital landscape. The advantages often includes better scalability, cost efficiency, improved performances, enhanced security, but also disaster recovery and faster time to market.
For a frontend application, the reasons to do a migration are also numerous:
In the case of my client, the migration was absolutely needed: AngularJS officially reached its end of life in December 2021. This means no more updates, bug fixes, or security patches are being released by Google. Continuing to use AngularJS carries inherent risks, including security vulnerabilities and technical debt, making migration essential.

React, maintained by Facebook, is one of the most widely used frontend libraries with robust community support and constant updates. Its fast-growing ecosystem ensures access to modern tools, libraries, and best practices, helping developers stay ahead of the curve.

A company becomes more attractive by upgrading to React, because of its broad adoption and rich talent pool. In the example of my client, the market to hire AngularJS engineers is less interesting than the market of React developers. The community is bigger, and finding experts and seniors is easier. New graduates are also more attracted to React, which is a technology that is gaining momentum, unlike AngularJS.

![Google Trend comparison: React VS AngularJS](/blog/assets/images/google_trends_react_vs_angular.png)

React is designed to be highly efficient using its virtual DOM, which optimizes how changes are applied to the UI. This results in faster rendering and enhanced performance, even for dynamic, complex applications.
Unlike AngularJS, which comes with a tightly coupled framework, React is a library that provides flexibility. You can choose other libraries for routing, state management (like Redux or Zustand), and build tools, giving you freedom to design development workflows tailored to your needs.

By migrating from AngularJS to React, organizations can modernize their codebase, adopt a more efficient development approach, and create high-performing, future-proof applications that better meet user and business needs.

# Which strategies to adopt

A migration can be a challenge for a tech company. How do you temporarily put the right effort into actually duplicating your existing product, and at the same time continue to produce value?
That was the big challenge of my client, a major player in accounting services for freelancers in Germany. Another challenge they could face was how to enable their teams to transition from great AngularJS developers to great React.js developers.

They came to the conclusion to use externals to support them overcome these challenges. Externals (consultants from my company as well as freelancers) will support them to kick start the migration without disturbing the current business, as well as coaching and enabling good practices into the new framework. The teams had different approaches: in my team one person from the team was rotating every sprint to get their hands into the migration, to grasp knowledge of the new patterns and to have a continuity when we hand over the migration work to them. Several team started at the same time to have 1 or 2 external developers supporting the migration of their team's scope.

# A zoom on the frontend migration

The client decided to migrate only the frontend part first, and to keep the same backend. The company decided to adopt a shared components library along the frontend migration. This means that the features and components needed a redesign first, done and validated by the designers, then a developer could create the corresponding item in the component library, then only the developers could integrate the component in the new codebase. For the component library, we used Storybook in combination with Supernova. Storybook is the tool that we used to develop, document and test UI components in isolation. Supernova was used to monitor the health of our design system components. It helps to track the health and maturity of the design systems content and display it easily in the documentation.

The company had several feature teams in charge of separated / independent features of the product. The idea was to migrate page by page, copying the previous version. But in real life what happens was that different teams had different use cases:

- For one team, the features already existed but were far from using the latest frontend patterns, were 100% written in AngularJS, and were not integrating the new design.

- For another team, a feature would already exist and would be already developed in React, but in the old AngularJS codebase: this made it possible to “copy” and reuse the logic. The components will need to be updated anyway to comply with coding rules in the new product.

In order to complete the migration, each team had to define its own strategy to achieve the same standard. The steps were therefore different for each team, and each team contributed differently to the component library. Some teams contributed enormously to this component library, while others, which started later, simply had to draw on the already well-developed library.

# Lessons learned

As I just mentioned, some parts of the old codebase were already written in React. So we thought it would be easy to migrate. However, that wasn’t quite the case. What happened was that:

- the quality level was higher on the new codebase: we started to use SonarQube, with a higher test coverage requested, additional rules like limited nested functions depth etc.

- We introduced type management with Zod on top of using Typescript. With Zod, you prioritize runtime safety and validation over the purely static type checking provided by TypeScript. This added layers of complexity and validation.

- Some features were already implemented in React, making it seem straightforward to migrate large blocks of code. However, the new codebase was still evolving, with its rules and tools being established during the migration process. As a result, by the time an entire page was migrated, the rules had often changed, requiring all interim modifications to be reapplied to the migrated codebase. This experience highlighted the importance of keeping PRs under 400 lines to ensure smoother reviews and more effective integration into the evolving codebase.

- It was also necessary to reintroduce everything related to marketing and tracking. The marketing team still needed access to their tools to monitor user behavior. However, this requirement wasn’t initially accounted for and had to be addressed later, on top of migrating existing features. This included implementing elements like cookie acceptance to ensure tools such as Hotjar and other marketing platforms continued functioning seamlessly in the migrated version.

- I got a feedback from a former internal senior colleague a few months later. He could express that the goal was to create a “golden path”, like a centralized, best-practice-driven approach to the migration roadmap. In the beginning, they served as gatekeepers to ensure the path would neither be shortened nor deviated by using different tools or patterns. Coordinating efforts among three to four teams proved challenging, and looking back, he suggested a more incremental approach: starting small, achieving initial success within only one team, and after that, spreading the knowledge and good practices to other teams.

# Did you say AI?

Of course, AI can have a great potential to support the migration and we creatively incorporated it with a PoC to identify how much GenAI was able to leverage the existing frontend.

What did we learn on the way?

Existing migration examples, screens and an existing component library were a necessary foundation to generate qualitative long-term results. We could notice that GenAI performed well for documentation like generating Storybook stories, or API documentation. It was good at adding new features in the migration especially when generating structure for components​ or extracting reusable code. Doing repetitive tasks like generating unit tests and mocks were also completed well.

At the same time, there was room for improvement concerning design, when handling complexity like solving complex bugs involving different files​ or solving advance accessibility issues​.

The results with the PoC were promising with a productivity gain of development estimated between 2.5x and 5x and 60 to 80% of manual efforts that could be saved on the overall migration.

AI-generated code must be, of course, reviewed and refined by experienced developers. Clear code review policies, paired with secure coding standards and project-specific guidelines help catch inconsistencies, reduce duplication, and prevent tech debt. You should always treat AI as an assistant and not as an authority to preserve the code quality and your team accountability!

# General challenges raised while doing a migration

There are many parallels between a frontend migration and other types of migrations. In a conversation with a Cloud Migration expert from Netlight, we covered three identified common patterns that apply universally to migrations:

The first one is the organizational challenge. The change management skills are very important in order to do a migration. Migrations introduce new tools, workflows, and technologies, which means teams must adapt their ways of working. For example, in the case of a frontend migration like AngularJS to React, developers not only need to learn a new framework but also shift to understand new concepts like React’s component-based architecture or declarative programming. This transformation often disrupts established routines, and can lead to initial resistance or a dip in productivity. To obtain an effective change, the management layers needs to be involved with clear communication about the reasons for the migration, Part of my job at the client was also to coach, review pull requests, so that team members can switch effectively from Angular to React. Also, if you do a migration and do not change the way of communication in your company, it will end in the same way as before, as illustrated by the Conway’s Law.

![Conway's Law - Image: Jono Hey, Sketchplanations](/blog/assets/images/conways_law.jpg)

Another common thing is to analyze what is the smallest chunk you can migrate without breaking the app. This is why we could see above that my client split the tasks into 2 distinct types of teams: the central migration team, taking care of building the bridges and adapters to facilitate the communication between the new and the old systems, and the feature teams, migrating their independent features and pages.

The third one is to decide to do an incremental migration. You always have to fight the fact that you cannot let your product die, meaning stopping completely from adding features or maintaining. But if you continue to produce too much inputs in the old version, you will never win the race! And this applies to any kind of migration. The secret is to be able to split your services. So if you are able to start deploying in prod a part of your new migrated version, and little by little, replace every service by the new one, then you are on the right way to succeed in migrating tour product. This is called gradual migration.

# Conclusion

Migrating from AngularJS to React goes beyond technical tasks: it’s about balancing business priorities, team dynamics, and modern technology needs. My client’s journey shows universal challenges like incremental progress, change management, and breaking work into manageable pieces. While migrations can be complex, they also present powerful opportunities to modernize, improve workflows, and future-proof systems. With the right strategies and collaboration, any migration can become a catalyst for growth and innovation!


