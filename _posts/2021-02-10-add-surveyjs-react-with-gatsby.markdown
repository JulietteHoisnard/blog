---
layout: post
title: "How to add SurveyJS React to Gatsby"
subtitle: ""
date: 2021-02-10 15:26:56 +0100
related_image: https://www.meme-arsenal.com/memes/732d1b1716f4f493280b1ab23b19612d.jpg
tags: [coding]
---

1. I assume you already created a Gatsby app by following the [Quick Start documentation](https://www.gatsbyjs.com/docs/quick-start/)

1. Create your survey here: https://surveyjs.io/Survey/Builder/

1. Click on 'Embed Survey' and copy only the surveyJSON. Example:

   ```node
   const surveyJSON = {
     pages: [
       {
         name: "page1",
         elements: [
           {
             type: "text",
             name: "question1",
             title: "Firstname",
             isRequired: true,
           },
         ],
         title: "Survey",
         description: "Please give me your data.",
       },
     ],
   };
   ```

1. Install survey-react in your Gatsby project.

   ```shell
   npm install survey-react
   ```

1. Create a component Form.js in pages > components with the following content:

```react
import * as React from "react";
import * as Survey from "survey-react";
import "survey-react/survey.css";

export const Form = () => {
  // Paste your surveyJSON here

  const surveyJSON = { ... }

  //Define a callback methods on survey complete
  const onComplete = (survey) => {
    //Write survey results into database
    console.log("Survey results: " + JSON.stringify(survey.data));
  };

  return <Survey.Survey json={json} onComplete={onComplete} />;
};
```

1. Call the component in your index.js
   Start the local development server with
   ```shell
   npm run develop
   ```
