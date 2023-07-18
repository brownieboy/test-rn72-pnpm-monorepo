# Test of PNPM Monorepo for React Native

This is to test how a PNPM Monorepo works with React Native.  And it doesn't at the moment

## Install Instructions

Assumes that you have PNPM installed globally.  If you don't, then `npm i pnpm -g` is the quickest way to do that.

After clone this repo, `cd into` it and run 

```bash
pnpm i
cd apps/app1
pnpm ios
```

It will fail with error:

```bash
 BUNDLE  ./index.js

error: Error: Unable to resolve module react-native from /Users/michaelbrown/Development/test-rn72-pnpm-monorepo/apps/app1/index.js: react-native could not be found within the project or in these directories:
  node_modules
  ../../node_modules
  3 |  */
  4 |
> 5 | import {AppRegistry} from 'react-native';
    |                            ^
  6 | import App from './App';
  7 | import {name as appName} from './app.json';
```

`yarn android` will fail with this error:

```bash
FAILURE: Build failed with an exception.

* Where:
Settings file '/Users/michaelbrown/Development/test-rn72-pnpm-monorepo/apps/app1/android/settings.gradle' line: 2

* What went wrong:
A problem occurred evaluating settings 'app1'.
> Could not read script '/Users/michaelbrown/Development/test-rn72-pnpm-monorepo/apps/app1/node_modules/@react-native-community/cli-platform-android/native_modules.gradle' as it does not exist.
```

These are, I think, manifestations of the same issue.   React Native is not following PNPM's symlinks, even with the experimental symlink support enabled.

react-native *is* in the apps/app1/node_modules folder, although it's a symlink.