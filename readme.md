# bun-monorepo-shared-packages-repro

Reproduction set up to demonstrate how a developer can declare a dependency in a monorepo package, then use it in another monorepo package without also declaring the dependency there.

- [package-b](packages/package-b/) takes a dependency on [`itty-router`](https://www.npmjs.com/package/itty-router)
- [package-a](packages/package-a/) has no dependencies, but a script that imports `itty-router` and logs an instance of the router

with [pnpm](https://pnpm.io) npm packages will not be resolved if they are not declared as a dependency in the monorepo package

this is a mechanism to prevent the use of "phantom dependencies"

> So let's consider why phantom dependencies are a problem. Imagine you depend on the parse-git package. parse-git depends on lodash, so since lodash is hoisted to the outermost node_modules, you can use lodash in your code without explicitly including it in your package.json. The problem arises the day the authors of parse-git decide that they no longer need lodash and remove the dependency ✂️ Now your code is going crash with a module not found error 💣 Even worse, if lodash is updated to a version with breaking changes, then your app may not crash, but suddenly start to misbehave in a difficult to debug manner.
> https://www.coana.tech/post/a-quick-introduction-to-phantom-dependencies

this is also helpful when onboarding new developers to a project, as they will not need to decipher what dependency is installing the phantom dependency used in the project's code
