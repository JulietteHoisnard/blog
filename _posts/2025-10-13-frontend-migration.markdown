---
layout: post
title: "Migrating from Angular.js to React"
subtitle: "Insights and lessons learned"
date: 2025-10-13 12:22:00 +0100
related_image: /blog/assets/images/migration_image.png
tags: [coding, tech]
---

As part of an assignment with a client, where I helped initiate a migration from Angular.js to React, I decided to write this article to share my insights and lessons learned about managing a frontend migration effectively, and also about understanding what are common rules between a frontend migration and any other type of migration.

# Why to do a migration

Generally speaking, a company needs to do a migration when they see the needs to move to a more modern system, whether it is a cloud migration or a frontend migration. Indeed, in the case of a cloud migration, it can be a pivotal step for businesses striving to stay competitive and innovative in today’s fast-evolving digital landscape. The advantages often includes better scalability, cost efficiency, improved performances, enhanced security, but also disaster recovery and faster time to market.
For a frontend application, the reasons to do a migration are also numerous:
In the case of my client, the migration was absolutely needed: Angular.js officially reached its end of life in December 2021. This means no more updates, bug fixes, or security patches are being released by Google. Continuing to use Angular.js carries inherent risks, including security vulnerabilities and technical debt, making migration essential. 
React, maintained by Facebook, is one of the most widely used frontend libraries with robust community support and constant updates. Its fast-growing ecosystem ensures access to modern tools, libraries, and best practices, helping developers stay ahead of the curve.
A company becomes more attractive by upgrading to React, because of its broad adoption and rich talent pool. In the example of my client, the market to hire Angular.js engineers is less interesting than the market of React developers. The community is bigger, and finding experts and seniors is easier. New graduates are also more attracted to React, which is a technology that is gaining momentum, unlike Angular.js.

![Google Trend comparison: React VS Angular.js](/blog/assets/images/google_trends_react_vs_angular.png)

React is designed to be highly efficient using its virtual DOM, which optimizes how changes are applied to the UI. This results in faster rendering and enhanced performance, even for dynamic, complex applications.
Unlike Angular.js, which comes with a tightly coupled framework, React is a library that provides flexibility. You can choose other libraries for routing, state management (like Redux or Zustand), and build tools, giving you freedom to design development workflows tailored to your needs.

By migrating from Angular.js to React, organizations can modernize their codebase, adopt a more efficient development approach, and create high-performing, future-proof applications that better meet user and business needs.

# Which strategies to adopt

A migration can be a challenge for a tech company/product. How do you temporarily put the right effort into actually duplicating your existing product, and at the same time continue to produce value?
That was the big challenge of my client, a major player in accounting services for freelancers in Germany. Another challenge they could face was how to enable their teams to transition from great Angular.js developers to great React.js developers.
They came to the conclusion to use externals to support them overcome these challenges. Externals (consultants from my company as well as freelancers) will support them to kick start the migration without disturbing the current business, as well as coaching and enabling good practices into the new framework. The teams had different approaches: in my team one person from the team was rotating every sprint to get their hands into the migration, to grasp knowledge of the new patterns and to avoid being lost when we hand over the migration work to them. Several team started at the same time to have 1 or 2 external developers supporting the migration of their team's scope.

# A zoom on the frontend migration

The client decided to migrate only the frontend part first, and to keep the same backend. The company decided to adopt a shared components library along the frontend migration. This means that the features and components needed a redesign first, done and validated by the designers need, then a developer could create the corresponding item in the component library, then only the developers could integrate the component in the new codebase. For the component library, we used Storybook in combination with Supernova. Supernova is used to monitor the health of your design system components. It helps you track the health and maturity of your design systems content and display it easily in your documentation.

The company had several feature teams in charge of separated / independant features of the product. The idea was to migrate page by page, copying the previous version. But in real life what happens was that different teams had different use cases:
- For one team, the features already existed but were far from using the latest frontend patterns, were 100% written in Angular.js, and were not integrating the new design.
- For another team, a feature would already exist and would be already developed in React, but in the old Angular.js codebase: this made it possible to "copy" and reuse the logic. The components will need to be updated anyway to comply with coding rules in the new product.

# Lessons learned

As I just mentioned, some parts of the old codebase were already written in React. So we thought it would be easy to migrate. However, that wasn't quite the case. What happened was that:
- the quality level was higher on the new codebase: we started to use SonarQube, with a higher test coverage requested, additional rules like limited nested functions depth etc.
- We introduced type management with Zod instead of with Typescript,
- Features were already existing and fully coded in React. So it was easy to pick a huge block of code and migrate it. Although, merging a big chunk while the main migration part is still in development is a bad idea, because the developer had to 

There is also a need to re-add everything related to marketing and tracking. The marketing team needs to be able to continue using the same tools to see what users are doing.

# General challenges raised while doing a migration

You can see a lot of similarities between a frontend migration and any other type of migration. By discussing with a Cloud Migration expert from Netlight, he highlighted 3 common patterns between any migrations:

The first one is the organisational challenge. The change management skills are very important in order to do a migration. Migrations introduce new tools, workflows, and technologies, which means teams must adapt their ways of working. For example, in the case of a frontend migration like Angular.js to React, developers not only need to learn a new framework but also shift to understand new concepts like React’s component-based architecture or declarative programming. This transformation often disrupts established routines, and can lead to initial resistance or a dip in productivity. To obtain an effective change, the management layers needs to be involved with clear communication about the reasons for the migration, Part of my job at the client was also to coach, review pull requests, so that team members can switch effectively from Angular to React.

Another common thing is to analyse what is the smallest chunk you can migrate without breaking the app. This is why we could see above that my client split the tasks into 2 distinct types of teams: the central migration team, taking care of building the bridges and adapters to facilitate the communication between the new and the old systems, and the feature teams, migrating their independant features and pages.

The third one is to decide to do an incremental migration. You always have to fight the fact that you cannot let your product die, meaning stopping completely from adding features or maintaining. But if you continue to produce too much inputs in the old version, you will never win the race! And this applies to any kind of migration. The secret is to be able to split your services. So if you are able to start deploying in prod a part of your new migrated version, and little by little, replace every service by the new one, then you are on the right way to succeed in migrating tour product. This is called gradual migration.

# Conclusion

Migrating from Angular.js to React (or any system) goes beyond technical tasks: it’s about balancing business priorities, team dynamics, and modern technology needs. My client’s journey shows universal challenges like incremental progress, change management, and breaking work into manageable pieces. While migrations can be complex, they also present powerful opportunities to modernize, improve workflows, and future-proof systems. With the right strategies and collaboration, any migration can become a catalyst for growth and innovation.


More topics:

Central team to manage the migration.
What role exactly played this team? What kind of activities should be centralized? How do you share knowledge from this team to other teams? At which point is the team too much challenged and lacking of capacity to be able to review everything?

Was it a good strategy to start the migration in every team instead of trying to migrate only one team at a time, with a bigger power force?

How is AI enabling you to do the migration faster?


