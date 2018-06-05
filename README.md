# meu.starter.blank.ionic-v3
[![Conventional Commits](https://img.shields.io/badge/Conventional%20Commits-1.0.0-yellow.svg)](https://conventionalcommits.org)
[![Travis CI badge](https://travis-ci.org/meumobi/meu-starter.blank.ionic-v3.svg?branch=master)](https://travis-ci.org/)

[![Greenkeeper badge](https://badges.greenkeeper.io/meumobi/meu-starter.ionic-v3.svg)](https://greenkeeper.io/)

## Introduction

A starter template for PWA and Native Ionic v3 projects, providing worflow & build management best pratices out-of-box:

- [x] [Aliases and environment variables support](#aliases-and-environment-variables-support)
- [x] [Documentation generation using Compodoc](#documentation-generation-using-compodoc)
- [x] [Unit testing and end-to-end (e2e)](#unit-testing-and-end-to-end-e2e)
- [x] [Continuous integration with Travis CI](#continuous-integration-with-travis-ci)
- [x] [Automated dependency updates](#automated-dependency-updates)
- [x] [Standardized commit messages and automatic changelog generator](#standardized-commit-messages-and-automatic-changelog-generator)

## Coding best practices

- [] Shared module
  - [meumobi: Creating a shared module for Ionic App](http://meumobi.github.io/ionic/2017/08/23/creating-shared-module-ionic.html)
- [] Simple Logging Service
  - [A simple logging service for Angular 4](https://robferguson.org/blog/2017/09/09/a-simple-logging-service-for-angular-4/)
  - [Angular's github: Add $log like functionality to Angular 2](https://github.com/angular/angular/issues/5458)
- [] Lazy loading / Deep-linking
  - [Ionic blog: Ionic and Lazy Loading Pt 1](https://blog.ionicframework.com/ionic-and-lazy-loading-pt-1/)
  - [Ionic blog: Ionic and Lazy Loading Pt 2](https://blog.ionicframework.com/ionic-and-lazy-loading-pt-2/)

# Getting started

```sh
$ git clone https://github.com/meumobi/meu-starter.blank.ionic-v3.git [YOUR PROJECT NAME]
$ cd [YOUR PROJECT NAME]
[YOUR PROJECT NAME]$ rm CHANGELOG.md
[YOUR PROJECT NAME]$ git init
[YOUR PROJECT NAME]$ git add .
[YOUR PROJECT NAME]$ git commit -m "first commit"
[YOUR PROJECT NAME]$ git remote add origin ttps://github.com/[YOUR ACCOUNT]/[YOUR PROJECT NAME].git
[YOUR PROJECT NAME]$ git push -u origin master
[YOUR PROJECT NAME]$ npm run release -- --first-release
[YOUR PROJECT NAME]$ npm ci
[YOUR PROJECT NAME]$ ionic serve
```

- Signup/Signin on [Travis CI](https://travis-ci.org/) and enable your new repository for Continuous Integration.
- Signup/Signin on [Greenkeeper](https://greenkeeper.io/) and enable Greenkeeper access for your new repository from your account page on section 'repo not listed?'


# Worflow & Build Management
## Aliases and environment variables support
- [Managing Aliases and environment variables in Ionic v3... preparing Ionic v4](http://meumobi.github.io/ionic/2018/05/10/managing-aliases-environment-variables-ionc.html)

## Documentation generation using Compodoc
- [Compodoc: Getting Started](https://compodoc.github.io/website/guides/installation.html)

### Local installation
```
npm install --save-dev @compodoc/compodoc
```

### Build and serve docs
Define script tasks for it in your package.json :
```
"scripts": {
  "docs:build": "./node_modules/.bin/compodoc -d ./docs/ -p ./tsconfig.json",
  "docs:serve": "./node_modules/.bin/compodoc -s -d ./docs"
}
```

and run it like a normal npm script, to generate documentation :

```
$ npm run docs:build
```

To serve the generated documentation:

```
$ npm run docs:serve
```

Open your browser and navigate to: `http://localhost:8080`

You can exclude files from the generated documentation by using 'exclude' in tsconfig.json:

```
  "exclude": [
    "./node_modules",
    "./temp/**/*.ts",
    "./src/environments/*.ts",
    "./src/services/**/*.ts",
    "**/*.spec.ts"
  ]
```
## Unit testing and end-to-end (e2e)
- [Leif Wells's blog: Configure Existing Ionic Projects for Testing](https://leifwells.github.io/2017/08/27/testing-in-ionic-configure-existing-projects-for-testing/)
- [Unit Testing an Ionic2 project](https://lathonez.com/2018/ionic-2-unit-testing/)

The important modules are `karma`, `jasmine` and `protractor`:
- [karma](https://karma-runner.github.io/2.0/index.html) is our testing environment for unit testing. 
- [jasmine](https://jasmine.github.io/) is the unit testing framework. 
- [protractor](https://www.protractortest.org/#/) is our testing environment for our end-to-end tests. 

The rest of the modules are utilities that allow this configuration to work.

### Unit tests: Jasmine

```
$ npm run test
```

### End-to-end tests: Protractor

End-to-end tests explore the application as users experience it.
In e2e testing, one process runs the real application and a second process runs protractor tests that simulate user
behavior and assert that the application respond in the browser as expected.

```
$ npm run e2e
```

### Test coverage: Istanbul

```
$ npm run test-coverage
```

In the `./coverage` folder open index.html.

```
$ cd coverage/
$ python -m SimpleHTTPServer 8000
```
![test-coverage](https://www.evernote.com/l/APVZPlnTsIpHiI8tQcEN5r8pPLKHhjeZmwUB/image.png)

- [Automated testing with Headless Chrome](https://developers.google.com/web/updates/2017/06/headless-karma-mocha-chai)

## Continuous integration with Travis CI

- **Continuous Build**: a tool that checks periodically if the repository changed since the last build, and build/test if it did.
- **Continuous Integration**: a tool that takes Pull Requests and validate them against the latest head prior to making them visible.

If using feature branches, you should have the CI running automatically on those, and if the builds fail, don't merge them into master.

Using Travis, with each push we want to:

- run unit tests: `npm run lint`
- lint code: `npm run test:headless`
- generate build: `npm run build`
- run e2e (end to end) tests: `xvfb-run npm run e2e`

[Travis CI](travis-ci.org) connects to GitHub repositories out of the box. Navigate to (travis-ci.org) and sign in with your GitHub account. Navigate to your profile and you should see a list of your public repos from GitHub. Enable CI on targeted repo.

It was that simple, the last step for CI is to add a Travis CI configuration file to our project to tell Travis CI how to prepare environment for our app, on which branches to run CI build and which scripts to run on build.

To [speed up CI build we use npm ci and package-lock.json](https://medium.com/@tomastrajan/how-to-speed-up-continuous-integration-build-with-new-npm-ci-and-package-lock-json-7647f91751a).

### Headless Chrome

As the [official documentation](https://developers.google.com/web/updates/2017/04/headless-chrome) says…

> [Headless Chrome](https://chromium.googlesource.com/chromium/src/+/lkgr/headless/README.md) is shipping in Chrome 59. It’s a way to run the Chrome browser in a headless environment. Essentially, running Chrome without chrome! It brings **all modern web platform features** provided by Chromium and the Blink rendering engine to the command line.

### Caching with npm
[Caching with npm](https://docs.travis-ci.com/user/languages/javascript-with-nodejs/#Caching-with-npm)

```yaml
cache:
  directories:
    - "node_modules"
```

`npm install` will still run on every build and will update/install any new packages added to your package.json file.

Thanks to [julie-ng/angular-starter: Setup Travis CI](https://github.com/julie-ng/angular-starter/pull/1)
- use the Travis provided [Chrome addon](https://docs.travis-ci.com/user/chrome)
- use the Travis provided [xvfb wrapper](https://docs.travis-ci.com/user/gui-and-headless-browsers/#Using-the-xvfb-run-wrapper) around Chrome for E2E

### Furthermore

- [Testing Angular 2+ Apps with Jasmine and Karma](https://www.youtube.com/watch?v=yG4FH60fhUE)
- [Unit Testing with Angular](https://www.youtube.com/watch?v=Yod3tBt0beM)
- [Ionic project: Continuous Integration with Travis for gh-pages](https://medium.com/@hamidihamza/ionic-project-continuous-integration-with-travis-for-gh-pages-3275edaac6a0)
- [continuous integration | angular cli + firebase + travis ci](https://houssein.me/continuous-integration-angular-firebase-travisci)
- [Continuous Integration for Angular Projects with TravisCI](https://moduscreate.com/blog/continuous-integration-angular-projects-travisci/)
- [Continuous Deployment for Ionic 2 to Firebase Hosting](https://guillaumeroy.xyz/2017/02/23/continous-deployment-ionic2-firebase-hosting/)
- [E2E (End-to-End) Testing in Ionic 2: An Introduction](https://www.joshmorony.com/e2e-end-to-end-testing-in-ionic-2-an-introduction/)

## Automated dependency updates

We've selected [Greenkeeper](https://greenkeeper.io/), against [Dependabot](https://dependabot.com/), because it's free for github public project, **inclusive for organization**.
The [installation](https://greenkeeper.io/docs.html#installation) is pretty straight-forward, only need to signup on [Greenkeeper](https://greenkeeper.io/), give autorization to connect to your github repository and follow instructions.

- [Continuous everything with Angular, Travis CI, Firebase and Greenkeeper](https://medium.com/@jamzi/continuous-everything-with-angular-travis-ci-firebase-and-greenkeeper-6656543bd826)

## Standardized commit messages and automatic changelog generator
[standard-version](https://github.com/conventional-changelog/standard-version) automatically generates and updates `CHANGELOG.md` file with all the commits following [Conventional Commits specification](https://conventionalcommits.org/) and correctly determines new version of our project.

The commit contains the following structural elements, to communicate intent to the consumers of your library:

- **fix**: a commit of the `type fix` patches a bug in your codebase (this correlates with [PATCH](https://semver.org/#summary) in semantic versioning).
- **feat**: a commit of the `type feat` introduces a new feature to the codebase (this correlates with [MINOR](https://semver.org/#summary) in semantic versioning).
- **BREAKING CHANGE**: a commit that has the text `BREAKING CHANGE`: at the beginning of its optional body or footer section introduces a breaking API change (correlating with [MAJOR](https://semver.org/#summary) in semantic versioning). A breaking change can be part of commits of any type. e.g., a fix:, feat: & chore: types would all be valid, in addition to any other type.
- Others: commit types other than fix: and feat: are allowed, for example commitlint-config-conventional (based on the the [Angular convention](https://github.com/angular/angular/blob/22b96b9/CONTRIBUTING.md#-commit-message-guidelines)) recommends chore:, docs:, style:, refactor:, perf:, test:, and others. We also recommend improvement for commits that improve a current implementation without adding a new feature or fixing a bug. Notice these types are not mandated by the conventional commits specification, and have no implicit effect in semantic versioning (unless they include a BREAKING CHANGE, which is NOT recommended). 

# Inspiration

- [RomainFallet/ionic-workflow-guide](https://github.com/RomainFallet/ionic-workflow-guide)
- [Robinyo/big-top](https://github.com/Robinyo/big-top)