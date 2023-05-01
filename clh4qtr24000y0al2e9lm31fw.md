---
title: "Migrate Your Create-React-App to Vite Easily!"
seoTitle: "Migrate Your Create-React-App to Vite"
seoDescription: "Migrate Your Create-React-App to Vite Easily with these simple steps"
datePublished: Mon May 01 2023 11:14:28 GMT+0000 (Coordinated Universal Time)
cuid: clh4qtr24000y0al2e9lm31fw
slug: migrate-your-create-react-app-to-vite-easily
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1682927535669/b33abd90-7c3a-45ca-87e8-67fac1eb1c1d.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1682939404803/77c1d31a-72bb-49c5-b947-26ede51a17a0.png
tags: frontend, reactjs, typescript, frontend-development, vite

---

Recently I have migrated some of my existing React projects to Vite, and the results are shocking. The development process has been drastically faster for quick build time.

In this article, I will discuss why to switch to Vite and how quickly you can achieve this.

## Why Vite?

%[https://media.giphy.com/media/kX7OWl40hcz6RSYyjN/giphy.gif] 

Though, no such drawbacks to using Create React App, you can achieve a significantly faster development cycle using Vite. Here are some of the reasons for that:

* Vite uses ESmodules in the browser to load your code instantly, no matter how large that is.
    
* Vite uses Hot Module Replacement (HMR) for a faster feedback loop during development.
    
* While using production build, Vite uses Rollup. **Rollup has better tree shaking** than Webpack, which can eliminate unused code more effectively and reduce the bundle size.
    

## Well, Seems Interesting...! But How to Migrate?

### 1\. First, Install two dependencies:

```bash
npm install --save-dev vite @vitejs/plugin-react vite-plugin-svgr
```

And then remove react-scripts from your project:

```bash
npm uninstall react-scripts
```

![Replace react-scripts with vite on package.json](https://cdn.hashnode.com/res/hashnode/image/upload/v1682939207084/53b8ada2-293e-4219-ae44-97f714b21c78.png align="center")

> **Now Move your** `index.html` **file which was in your public folder to the root of your project**

### 2\. Replace Existing Scripts in `package.json`

```json
"scripts": {
    "start": "vite",
    "build": "vite build",
    "preview": "vite preview"
}
```

### 3\. Now, In your `index.html` remove all the %PUBLIC\_URL%.

![Remove %PUBLIC_URL% from links in index.html](https://cdn.hashnode.com/res/hashnode/image/upload/v1682931309676/3ba31572-8001-4545-95dd-0193dcfda33e.png align="center")

```xml
// Before
<link rel="icon" href="%PUBLIC_URL%/favicon.ico" />
// After removing %PUBLIC_URL%
<link rel="icon" href="/favicon.ico" />
```

### 4\. Now add an entry point to your `index.html` file:

```xml
<!-- entry point 👇 -->
<script type="module" src="/src/index.tsx"></script>
```

### 5\. Now, add a `vite.config.ts` or vite.config.js to the root of your project

> you will need `vite-plugin-svgr` if you're using svg in your projects. Otherwise vite will throw an error.

```typescript
import { defineConfig } from 'vite';
import react from '@vitejs/plugin-react';
import svgrPlugin from 'vite-plugin-svgr';

export default defineConfig({
  plugins: [react(), svgrPlugin( { icon: true } )],
});
```

### 6\. Create a `vite.env.d.ts` to your src directory

If you use TypeScript then add:

```typescript
/// <reference types="vite/client" />
```

Now to use SVG, also add this to `vite.env.d.ts`

```typescript
/// <referencetypes="vite-plugin-svgr/client" />
```

### 7\. Handling Environment Variables

Now in your project, you may have variables that start with `REACT_APP_` but on Vite, those are needed to be replaced with `VITE_`:

![Replace REACT_NAME_ with VITE_ in all your environment variables](https://cdn.hashnode.com/res/hashnode/image/upload/v1682935151431/c1235e33-34f3-4a84-8c2a-890ca67c951b.png align="center")

But doing this may be time-consuming, To overcome that you need to install `vite-plugin-env-compatible`

```bash
npm i vite-plugin-env-compatible
```

**now in your** `vite.config.ts` **file:**

```typescript
import { defineConfig } from 'vite';
import react from '@vitejs/plugin-react';
import svgrPlugin from 'vite-plugin-svgr';
import envCompatible from 'vite-plugin-env-compatible';

export default defineConfig({
  envPrefix: 'REACT_APP_',

  plugins: [react(), envCompatible(),svgrPlugin( { icon: true } )],
});
```

Now you don't need to change variable prefixes. But in react we import those variables as `process.env.VARIABLE_NAME` but in Vite, you need to replace those as `import.meta.env.VARIABLE_NAME`

![replace process.env with import.meta.env](https://cdn.hashnode.com/res/hashnode/image/upload/v1682937204419/b42ab47d-a66d-4671-b1d7-8f67cbce3dc6.png align="center")

### 8\. Edit TSconfig.json

Things you need to update in `tsconfig.json` are `types`. For example:

```typescript
{
  "compilerOptions": {
    ...
    "types": ["vite/client", "vite-plugin-svgr/client"],
    ...
  },
  ...
}
```

### 9\. TypeScript Path Aliases

For the path aliases to work in your project you need to install `vite-tsconfig-paths` :

```bash
npm i vite-tsconfig-paths
```

Then on your `vite.config.ts` :

```typescript
import { defineConfig } from 'vite';
import react from '@vitejs/plugin-react';
import svgrPlugin from 'vite-plugin-svgr';
import envCompatible from 'vite-plugin-env-compatible';
import tsconfigPaths from 'vite-tsconfig-paths';

export default defineConfig({
  envPrefix: 'REACT_APP_',

  plugins: [react(), envCompatible(), tsconfigPaths(), svgrPlugin( { icon: true } )],
});
```

## Additional Steps:

### 1\. Change Build Output folder:

By default, Vite generates a `dist/` folder for generated build files. However, you can change that folder name

on your `vite.config.ts` file:

```typescript
import { defineConfig } from 'vite';
import react from '@vitejs/plugin-react';
import svgrPlugin from 'vite-plugin-svgr';
import envCompatible from 'vite-plugin-env-compatible';
import tsconfigPaths from 'vite-tsconfig-paths';

export default defineConfig({
  envPrefix: 'REACT_APP_',

  plugins: [react(), envCompatible(), tsconfigPaths(), svgrPlugin( { icon: true } )],
  // add this 👇
  build: {
      outDir: "build",
  },
});
```

### 2\. Change the server port

on your `vite.config.ts` file:

```typescript
import { defineConfig } from 'vite';
import react from '@vitejs/plugin-react';
import svgrPlugin from 'vite-plugin-svgr';
import envCompatible from 'vite-plugin-env-compatible';
import tsconfigPaths from 'vite-tsconfig-paths';

export default defineConfig({
  envPrefix: 'REACT_APP_',

  plugins: [react(), envCompatible(), tsconfigPaths(), svgrPlugin( { icon: true } )],
  build: {
      outDir: "build",
  },
  // add this 👇
  server: {
      port: 4000,
      open: true, // this will open directly to your browser
  },
});
```

### And... You're Done!!

%[https://media.giphy.com/media/SPimgKxdLZHHs5eosn/giphy.gif] 

## Final Thoughts

Migrating from Create-React-App was pretty simple. After implementing this the development experience has been great and fast! If you find this article helpful consider dropping a like and comment down to share your thoughts!