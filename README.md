# BugReplay TestCafe Integration
The BugReplay TestCafe integration records screencasts of your automated TestCafe tests including timesynced JavaScript Console and Network logs

## Installation
Install the package

```sh
npm install testcafe-bugreplay --save-dev
```

or if you prefer to use [yarn](https://yarnpkg.com/)

```sh
yarn add testcafe-bugreplay --dev
```

## Configuration
### Getting an API key
You will need to sign up for an account at https://bugreplay.com. After that you will need to login and get an API key by clicking the Hamburger Menu, click My Settings, and then Show API Key. You'll use this in the configuration file.

![getting an API key](./docs/assets/bugreplay_api_key.gif)


### Adding the BugReplay Integration
In .testcaferc.json you'll need to tell Chrome to use the BugReplay Automation extension:

```json
// .testcaferc.json
{
  "browsers": {
    "path": "/path/to/google-chrome",
    "cmd": "--no-first-run --no-default-browser-check --user-data-dir=/tmp/testcafe-chrome-profile --load-extension=./node_modules/bugreplay-automation/extension/ --auto-select-desktop-capture-source='Chrome'"
  }
}
```

After setting up this configuration you can have BugReplay record a fixture of tests by importing bugReplay and wrapping your fixture around this function and supplying an API key. For instance:

```js
// test.js
import bugReplay from 'testcafe-bugreplay'

bugReplay(
  fixture `Getting Started`
    .page `http://devexpress.github.io/testcafe/example`,
  { apiKey: "YOUR API KEY GOES HERE"}
)
// ... your tests go here
```

All tests in this file would be recorded to BugReplay.

## Running the Test
### Running from Command Line
You can run the test directly by running the following in your terminal:
```sh
npx testcafe path/to/tests
```

### Setting up a script
Inside of `package.json` add the following to the `scripts` object:
```json
"scripts": {
  "test:testcafe": "testcafe path/to/tests"
}
```
You can name the script anything you'd like, it does not have to be `test:testcafe`.

Then in your command line run:
```sh
npm run test:testcafe
```

or

```sh
yarn test:testcafe
```

## Limitations
This currently only works for Chrome. We're looking to expand to other browsers in the future.
