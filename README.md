# fsevents-issue

## Dependencies

macOS Catalina version `10.15.7`

Node.js version `14.15.5`

npm version `7.5.4`

## Steps to reproduce issue

### Step 1: install npm packages

```console
npm install
```

### Step 2: run `react-scripts start` (which watches folders for changes) and wait for `Compiled successfully!`

```console
$ npm start
Compiled successfully!

You can now view my-app in the browser.

  Local:            http://localhost:3000
  On Your Network:  http://10.0.1.179:3000

Note that the development build is not optimized.
To create a production build, use npm run build.
```

### Step 3: edit `/Users/sunknudsen/Desktop/my-app/node_modules/react-cool-img/dist/index.esm.js`

```
printf "\nconsole.log(\"foo\")" >> node_modules/react-cool-img/dist/index.esm.js
```

Running command should trigger watch event (which outputs `Compiling...` to console) consistently.

On my system, running command either doesn’t trigger watch event or triggers one every two runs (expected behavior: watch event should be triggered on all runs).

If run consistency triggers watch event, stop `react-scripts` using `ctrl-c` and start over at [step 2](#step-2-run-react-scripts-start-which-watches-folders-for-changes-and-wait-for-compiled-successfully).

Using above steps, I am able to consistently reproduce the issue.