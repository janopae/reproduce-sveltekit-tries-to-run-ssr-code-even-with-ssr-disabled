This repository should help you reproducing https://github.com/sveltejs/kit/issues/12580.

## How to reproduce

1. clone, `npm install`
2. `npm run dev`
3. Request the development server (e. g. in a browser)
4. See the error message:

```
[vite] Error when evaluating SSR module /src/routes/+layout.ts:
|- ReferenceError: localStorage is not defined
    at /var/www/my-app/src/routes/+layout.ts:4:1
    at instantiateModule (file:///var/www/my-app/node_modules/vite/dist/node/chunks/dep-Cy9twKMn.js:52858:11)
```

## The problem

Svelte runs the `+layout.ts` file on server-side, even though SSR is explicitly disabled.

This can't be avoided, as SSR is disbaled as late as in the `+layout.ts` file itself.

We either need a way to disable SSR from the begin with, or another way to add layout code that won't be run on server side.
