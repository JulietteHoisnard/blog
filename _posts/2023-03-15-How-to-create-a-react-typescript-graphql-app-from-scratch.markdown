---
layout: post
title: "How to create a React application from scratch"
subtitle: "Including Vite, React Router, Typescript, Tailwind, MSAL authentification, tests and production setup"
date: 2023-03-15 15:10:00 +0100
related_image: https://images.unsplash.com/photo-1507778031059-d74c30b52585?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1674&q=80
tags: [tech, coding]
---

1. **Create a repo in Github**
   Clone your repo to work from your computer and go inside this repo:

```shell
git clone git@github.com:my-project.gi
cd my-project
```

2. **Create a react app with typescript (OLD)** (files will be named in tsx and ts)

```shell
npx create-react-app my-project-frontend --template typescript
cd my-project-frontend
```

**OOOR**<br>

**Create a react application with Vite (RECOMMENDED)**
Why should you use Vite instead of Create-React-App? Two links to understand the current stand:
https://blog.logrocket.com/vite-3-vs-create-react-app-comparison-migration-guide/

https://luketheweb.dev/blog/what-is-vite-and-why-should-you-use-it-instead-of-create-react-app

```shell
npm init vite@latest vite-project --typescript react
```

3. **Install a react router**

```shell
npm install --save react-router-dom
```

Now add your router in your app.tsx:

```javascript
import React from "react";
import "./App.css";
import { Route, Routes, BrowserRouter } from "react-router-dom";
import Plans from "./components/Plans";
import Teams from "./components/Teams";
import NavBar from "./components/NavBar";

function App() {
  return (
    <div className="h-screen w-full">
      <NavBar />
      <BrowserRouter>
        <Routes>
          <Route path="/" element={<Plans />} />
          <Route path="teams" element={<Teams />} />
        </Routes>
      </BrowserRouter>
    </div>
  );
}

export default App;
```

Then you can run and see your app on the localhost in the browser:

```shell
npm start
```

4. **Add Tailwind with postcss:**

```shell
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init
```

Configure the postcss.config.cjs file:

```typescript
module.exports = {
  plugins: {
    tailwindcss: {},
    autoprefixer: {},
  },
};
```

Configure it in the tailwind.config.js which was just created:

```typescript
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: ["./src/**/*.{html,js}"],
  theme: {
    extend: {},
  },
  plugins: [],
};
```

My config is:

```typescript
const colors = require("tailwindcss/colors");

module.exports = {
  content: ["./src/**/*.{jsx,tsx,ts,js}"],
  theme: {
    screens: {
      sm: "640px",
      md: "768px",
      lg: "1024px",
      xl: "1280px",
      "2xl": "1536px",
    },
    // You can custom the colors
    colors: {
      transparent: "transparent",
      current: "currentColor",
      black: colors.black,
      white: colors.white,
      gray: colors.gray,
      // etc
      yellow: {
        50: "rgb(254 252 232)",
        100: "rgb(254 249 195)",
        // etc
      },
      dark: {
        300: "#XXXXXX",
        600: "#XXXXXX",
        800: "#XXXXXX",
      },
    },
    extend: {
      // you can extend the tailwind classes, or just add new ones like this:
      boxShadow: { yourname: "Xpx Xpx Xpx Xpx rgba(X, X, X, X)" },
    },
  },
  //need this plugin to customize checkboxes for example
  plugins: [require("@tailwindcss/forms")],
};
```

**5. Add authentication system**
If your organization/product is using azure/Microsoft to connect, check this page:
https://learn.microsoft.com/en-us/azure/active-directory/develop/tutorial-v2-react
Another useful page: https://blog.logrocket.com/using-msal-react-authentication/
Start by installing the msal-react library and its peer dependencies:

```shell
npm install @azure/msal-browser @azure/msal-react @azure/msal-common
```

The msal library makes use of the context API, so make sure to wrap the app in the MsalProvider.

```javascript
<MsalProvider instance={msalInstance}>
  <App />
</MsalProvider>
```

**6. Configure a .env page to run in local**

```shell
  VITE_STAGE=local
  VITE_API_GATEWAY_URL="http://localhost:8001/gql"
  VITE_REDIRECT_URI="http://localhost:3000"
  VITE_API_GATEWAY_REST="http://localhost:8001/rest"
  VITE_USE_MSAL=true
  VITE_API_GATEWAY_MOCK_DATA=false
```

**7. Add tests**

The Vite template doesn't include any test runner, we have to choose one. We decide to use Vitest as it is well develop to work easily with a Vite application. We will not use Jest, though Jest is currently the best up-to-date, with a large community, test runner for a React app (+ it is a native Vite test runner).

```shell
npm install -D vitest
```

Write the script for the tests in the package.json. The command vitest run "vitest watch" in dev, and "vitest run" in the CI. Specify the environment or it will not run correctly:

```json
"scripts": {
    // ...
    "test": "vitest watch --environment jsdom"
  },
```

Add the config to use jsdom in the Vite configuration file:

```typescript
import { defineConfig } from "vite";
import react from "@vitejs/plugin-react";

// https://vitejs.dev/config/
export default defineConfig({
  plugins: [react()],
  test: {
    environment: "jsdom",
  },
});
```

Also, you need to have @testing-library/react installed to run your tests. Example:

```typescript
import { expect, test, describe } from "vitest";
import React from "react";
import { render, screen } from "@testing-library/react";
import Avatar from "../components/Avatar";
import { AuthenticationContext } from "../contexts";
import { cleanup } from "@testing-library/react";

describe("when the avatar is displayed", () => {
  test("basic test works", () => {
    expect(Math.sqrt(4)).toBe(2);
  });
  test("should display the default unsplash picture if auth default provided", () => {
    const auth = {
      accessToken: "MockAPI",
      userId: "123",
      email: "evita.muzic@tourdefrance.com",
      jobTitle: "admin",
      avatar:
        "https://images.unsplash.com/photo-1607746882042-944635dfe10e?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1170&q=80",
    };
    const setAuth = null;
    render(
      <AuthenticationContext.Provider value={{ auth, setAuth }}>
        <Avatar />
      </AuthenticationContext.Provider>
    );
    const img = document.querySelector("img") as HTMLImageElement;
    expect(img).toBeTruthy();
    const svg = document.querySelector("svg") as SVGSVGElement;
    expect(svg).toBeFalsy();
    expect(img.src).toContain("unsplash");
    cleanup();
  });
```

**8. Add Apollo Client and GraphQL**

First install dependencies:

```shell
npm install @apollo/client graphql
```

Then initialize your client:

```typescript
const client = new ApolloClient({
  uri: "https://flyby-router-demo.herokuapp.com/",
  cache: new InMemoryCache(),
});
```

uri specifies the URL of our GraphQL server.
cache is an instance of InMemoryCache, which Apollo Client uses to cache query results after fetching them.

Then wrap your App in the context provider ApolloProvider:

```typescript
root.render(
  <ApolloProvider client={client}>
    <App />
  </ApolloProvider>
);
```

I advise you to use [GraphQL Code Generator](https://the-guild.dev/graphql/codegen):

```shell
npm install -D @graphql-codegen/cli
```

This tool generates code from your schema, especially typed queries and typed types that you can perfectly use in a Typescript application.
In your package.json, add a script to start the code generation:

```json
"graphql:generate": "graphql-codegen"
```

Then you config the codegen.yml file:

```yml
overwrite: true
schema: "./schemaTest.graphql"
documents: "src/**/!(*.d).{js,jsx,ts,tsx}"
generates:
  src/generated/graphql.tsx:
    plugins:
      - typescript
      - typescript-operations
      - typescript-react-apollo
    config:
      withHooks: true
      withComponent: false
      withMutationFn: false
```

Add useful predefined scalars to your schema:

```shell
npm install graphql-scalars
```

**9. Handle a local state with Recoil**

```shell
npm i recoil
```

Wrap your app inside RecoilRoot:

```typescript
import React from "react";
import {
  RecoilRoot,
  atom,
  selector,
  useRecoilState,
  useRecoilValue,
} from "recoil";

function App() {
  return (
    <RecoilRoot>
      <CharacterCounter />
    </RecoilRoot>
  );
}
```

**X. 404 page**

```shell

```
