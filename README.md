# VSCode Package Watcher

[![Visual Studio Marketplace Version](https://img.shields.io/visual-studio-marketplace/v/noinfode.noinfo-package-watcher)](https://marketplace.visualstudio.com/items?itemName=noinfode.noinfo-package-watcher)
[![Visual Studio Marketplace Installs](https://img.shields.io/visual-studio-marketplace/i/noinfode.noinfo-package-watcher)](https://marketplace.visualstudio.com/items?itemName=noinfode.noinfo-package-watcher)

Watch package lock files and suggest to re-run pnpm, npm or yarn.

Forked from [pinterest.package-watcher](https://marketplace.visualstudio.com/items?itemName=pinterest.package-watcher) to add `pnpm` support. Also removed telemetry.

<img src="https://raw.githubusercontent.com/christianvuerings/vscode-package-watcher/master/images/package-watcher-animated.gif" width="595" alt="Package Watcher animated gif to show functionality of the VSCode extension" />

## Features

- `pnpm`, `npm` and `yarn` support
- Monorepo support
- 2 Modes: `auto` & `request` [mode](#extension-settings)
- Restart ESLint server when package install is successful

## Install

Install options:

- [Download from the marketplace](https://marketplace.visualstudio.com/items?itemName=noinfode.noinfo-package-watcher)
- Install from the command line: `code --install-extension noinfode.noinfo-package-watcher`
- Search for `Package Watcher` in the VS Code extensions panel

## Requirements

- Use either `pnpm`, `npm` or `yarn` in your project
- A `node_modules` directory

## Extension Settings

| Setting                     | Type (default)                           | Description                                                                                                                                                                                               |
| :-------------------------- | :--------------------------------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `noinfoPackageWatcher.mode` | `enum: 'auto', 'request'` (**`'auto'`**) | `auto` runs the extension in the background and automatically runs yarn/npm install.<br />`request`notifies you when a change in a package lock file is detected and asks you to install new depedencies. |

## Extension Commands

| Setting                                  | Description             |
| :--------------------------------------- | :---------------------- |
| `noinfoPackageWatcher.showOutputChannel` | Show the output channel |

## Release Notes

See [Changelog](./CHANGELOG.md)

## Publish

Publish a new version:

1. Update `CHANGELOG.md` and add a new version
2. Publish with `vsce`

```
npm i -g vsce
vsce publish patch
```

## FAQ

### How does the extension work?

- Activate if there are 1 or multiple `package.json` file(s) within the workspace.
- Watch for changes to `pnpm-lock.yaml`, `yarn.lock` or `package-lock.json` files.
- When there are changes, ensure a sibling `node_modules` directory already exists. If not, don't do anything.
- When a `node_modules` directory exist either:
  - Ping the user to run the install command: `request` mode
  - Automatically run the install command: `auto` mode

### How does the monorepo support work?

We only run the install command in directories which have a `node_modules` directory. If that doesn't exist, we will not run the package install command.

### The extension doesn't seem to work, what can I do to debug?

Validate the following:

1. `package.json` exists in the VSCode workspace.
2. `pnpm-lock.yaml`, `yarn.lock` or `package-lock.json` file exists in the VSCode workspace.
3. `node_modules` directory lives next to the `package.json` directory.

Then restart your editor and copy/paste the output in the `noinfo Package Watcher` output log. You can see this log by clicking on `noinfo Package Watcher` in the status bar.
