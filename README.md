# Monorepo

## pnpm

- `npm install -g pnpm@latest-10` - installation via `npm`
- `brew install pnpm` - installation via `brew`
- `winget install -e --id pnpm.pnpm` - installation via `winget`
- [Other possibilities](https://pnpm.io/installation#prerequisites)

## pnpm workspace

In the project scope create `pnpm-workspace.yaml` file with content:

```yaml
packages:
  - packages/*
  - app1
  - app2
# - other packages
```

More information about [workspaces](https://pnpm.io/workspaces)

## Generate package.json for workspace

To generate new `package.json` for every package,app and etc run `pnpm init` at folder. That will create default `package.json` file.

## Installing/Adding packages globally or for workspace

Selectors may be specified via the `--filter` or (`-F`) flag. [More info about filtering](https://pnpm.io/filtering)

- `pnpm install` - is used to install all dependencies for a project.
- `pnpm install {{packageName}} -F {{workspace}}` - is used to install package for a workspace.
- `pnpm add {{packageName}}` in the root - this will add package in the root `package.json`;
- `pnpm add {{packageName}} -F {{workspace}}` in the root - this will add new package in specified workspace `package.json`; You can make multi filter if package required to be installed in the multiple workspaces `pnpm add {{packageName}} -F {{workspace1}} -F {{workspace2}}`
- `pnpm add {{packageName}}` in the workspace package - this will add new package in specific workspace `package.json`;

## Adding workspace package to another

You can add a workspace package to another by running command `pnpm add {{workspacePackageName}} -F {{workspace}} -workspace`. Multi filters can be used here too.

**NOTE from pnpm documentation:**

> pnpm cannot guarantee that scripts will be run in topological order if there are cycles between workspace dependencies. If pnpm detects cyclic dependencies during installation, it will produce a warning. If pnpm is able to find out which dependencies are causing the cycles, it will display them too.

## Running scrips

For example `pnpm run -parallel -F \"./packages/**\" -F \"./app1/**\" {{scriptTag}}` - it will run all defined `scriptTag` scripts from selected workspaces `packages.json`. `scriptTag` can be `build`, `test` and etc.
