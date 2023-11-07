# How to Contribute

## Summary
* [Prepare Your Environment](#prepare-your-environment)
* [Live Development Server](#live-development-server)
* [Live Development API](#live-development-api)
- [Contributing](#contributing)
  * [Getting Started](#getting-started)
  * [Branch Names](#branch-names)
  * [Commit Messages](#commit-messages)
- [The Desktop App](#the-desktop-app)
  * [How to Start Desktop App](#how-to-start-desktop-app)
- [Important Note: Fishing Data and Allagan Reports](#important-note-fishing-data-and-allagan-reports)

### Prepare Your Environment

* Install [Node.js](http://nodejs.org/) (>= 16.14) and Yarn (`npm i -g yarn`)
* Install local dev dependencies: `yarn` while current directory is this repo

#### Windows 10 environment

To build Electron on Windows, node-gyp is required and depends on some external tools:

1. Install a Python 3 distribution (like miniconda) Python needs to be discoverable on your PATH.
1. Install Visual Studio Community Edition 2022 and the C++ Desktop development tools.

### Live Development Server

Simply run `yarn start` to start a live server with file watcher.

### Live Development API

Since 10.2, Teamcraft includes its own API for various optimizations, hosted at https://api.ffxivteamcraft.com.

If you want to work on this API, simply run `yarn api:start`, which will run a watcher compiler and serve the api at http://localhost:3333.

Then edit `environment.ts` and set `useLocalAPI: true` to make sure it'll use the local API instead of the production one.

Data exposed by the API is extracted by the `data-extraction` project located in `apps/data-extraction` (the one at root folder is for chinese and korean data extraction), more details in the `README.md` file located there.

## Contributing

### Getting Started

When getting started with open source, it's important to note that new features and bug fixes are developed on new branches, which for this project follow a specific naming convention,  instead of contributing straight to the main/master branch. Setting this up can be accomplished in a few short steps. 

When interested in contributing to FFXIV Teamcraft, start by forking the main repository via tha `Fork` button on the GitHub homepage. 

Then, clone the repository on your local machine via the HTTPS link that is displayed after clicking the green `Code` button on your local repository.

After the repository has been cloned, create a new branch via the Git command `git branch <branchname>` using the format described below. 

Finally, checkout your new branch using the command `git checkout <branchname>`.

### Branch Names

When contributing to main repository, you'll notice that branch names follow a given pattern,
this pattern is the following: `<branch-type>/<short-description>`.

Example: `feat/commission-history-tab` would be a branch that adds a commission history tab. 

More `<branch-type>` examples are listed in the Commit Messages section.

We're using gitflow for this, more information on [https://github.com/nvie/gitflow](https://github.com/nvie/gitflow)

### Commit Messages

The commit messages are checked by a pre-commit git hook, meaning that if they don't meet the requirements, 
your commit will not be created.
 
A commit message should follow this structure:
```
<type>(<optional context>): <subject>
<BLANK LINE>
<body>
<BLANK LINE>
<footer>
```

Only the first line is mandatory, the rest is optional.

Types are the ones used by [standard-version](https://github.com/conventional-changelog/standard-version):

- **feat** - New feature
- **fix** - Bug fix
- **docs** - Documentation-related
- **style** - Style-related
- **refactor** - Refactoring of a code piece/feature
- **perf** - Performance optimization
- **test** - Tests-related
- **build** - Build-related
- **ci** - Continuous Integration-related
- **chore** - Changes that are not needed to be displayed in the changelog
- **revert** - Commit reverts

The optional context parameter (the part between parenthesis) is used to provide context
easily inside the changelog, to avoid having to append "inside page blabla" at the end of the message.

Context values can be any of the major features:

- simulator
- profile
- search
- alarms
- gathering-location
- list-details
- crafting-log
- pricing
- desktop
- favorites
- gearsets
- inventory
- db
- lists
- list-overlay
- fishing-reporter
- teams
- workshop
- rotations
- log-tracker
- macro-translator
- core
- comments
- layouts
- list-picker
- rotation-picker
- etc...

Examples:

`fix(simulator): byregots blessing now working as intended`

```
fix: need latest rxjs

For our http calls, rxjs can make us save a lot of time, it had to be updated.
```

## The Desktop App

Teamcraft is available as a desktop app using electron, and you might want to use it locally to implement or debug features that are specific to it (overlays, packet capture, file watchers).

The source files for the desktop app are located in `apps/electron`, entry point being `main.ts`.

### How to Start Desktop App

For this you'll need two terminals opened, bash, cmd, ps, as you want.

 - In the first terminal, run `yarn build:watch` and wait for it to produce at least one set of output files
 - In the second terminal, run `yarn electron:start` to start electron using the built files.
 - If you're modifying the electron files or the angular files and you want to see the result in the app, simply close the app or kill the `electron:start` process and restart it.

## Important Note: Fishing Data and Allagan Reports

Fishing data and allagan reports won't work in a dev env, this is due to the fact that dev env uses a separate firebase instance, which isn't able to produce the same oauth token that's used in production to communicate with the graphql API. 

In order to use fishing data, you'll have to edit the `environment.ts` (or `environment.beta.ts` if you're using desktop app) file to replace the content of the `firebase` key by the content of the `firebase` key in the `environment.prod.ts` file.
