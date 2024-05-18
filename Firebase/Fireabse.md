# Firebase
## Intro
Link: https://www.youtube.com/watch?v=DYfP-UIKxH0
Link: https://firebase.google.com/docs/web/setup?authuser=0&hl=en
- Backend runs on Google Cloud Servers
- Your code responds (is triggered in response) to events coming from Firebase Products
  These events include:
    - Writes to the **Firestore DB**.
    - File Uploads to the **Cloud Storage Bucket**.
    - New accounts in **Firebase Authentication**.
    - Incoming web **HTTPS requests**.
  <br>
- **Install**:
  - `Node.js` is required.
  - Firebase CLI:
  ```sh
  npm install -g firebase-tools
  ```
  - Firebase login: to log in with Gmail in browser.
  ```sh
  firebase login
  ```
  - Initialization of the project: to get the initial files.
  ```sh
  firebase init
  ```
    - Navigate with **arrow keys** to select the type of application you want.
    - **Space** to select.
    - **Enter** to accept selection and go next.
  <br>
- **Use**
  - The link given by the CLI Firebase will be the link for the endpoints.  
  - TypeScript needs to be compiled to JavaScript.
  <br>
- **Deploy**
  - Use the command to deploy:
  ```sh
  firebase deploy
  ```
  - The output of the log will be in the Firebase UI in your Firebase Project.
  - The link given by the deployment command is the link to the main application.
  <br>
- **Firebase Services** You can add in a single **Web Project** all the Firebase Services (Auth, Functions, Firestore, Cloud Storage...) by adding the script given when initializing the application on the Firebase Website.
<br>
- **Emulators** To run the firebase project locally use the command `firebase emulators:start`. It will start emulators for all services. 
  - **THIS MUST BE DONE INSIDE THE FUNCTIONS FOLDER TO WORK**: run `npm run build` to build the changes in the typescript.
  - For any products you are not emulating, your apps and code will interact with the live resource (database instance, storage bucket, function, etc.).
  - To configure emulators for Storage: `connectStorageEmulator(storage, "127.0.0.1", 9199);`
  - To configure emulators for Functions: `connectFunctionsEmulator(functions, "127.0.0.0", 5000);`
  - **IMPORTANT**: From experience connecting the emulators is really unhandy and hard to deploy if implemented.
<br>
- DO NOT COMMIT TO REPOSITORY THE **node_modules** OR **lib** FOLDER
### Logging and stack traces
To see the stack trace of a Firebase Function use the following command:
```sh
firebase functions:log --only  __function__name__
```
Replace `__function__name__` with the name of the generated Firebase Function. You should see this during deployment.

### Complete logs
- To see the complete logs you should use `Google Cloud Logs` to see every request to your deployed application.

## Post- and predeployment
- You can run scripts, Node commands etc., before and after a Firebase Service is deployed. You just need to add `"postdeploy":"_command_"`,`"predeploy":"_command_"` to the `firebase.json` config file for each service. You can run multiple commands by creating an array.

## Exposing firebase keys
Source: https://stackoverflow.com/questions/37482366/is-it-safe-to-expose-firebase-apikey-to-the-public

It is safe to expose the following keys to the client:
```JavaScript
const firebaseConfig = {
  apiKey: "",
  authDomain: "",
  projectId: "",
  storageBucket: "",
  messagingSenderId: "",
  appId: "",
  measurementId: ""
};
```
These keys are needed to properly communicate between Client and Firebase Backend.
As good practice include them in `.env.local` inside hosting and commit that file to `.git` (**it is safe**).


## Firebase and NextJS

### How to install and set-up Next.js in firebase, a list of commands
- First you need to enable experimental features.
```sh
firebase experiments:enable webframeworks
```
- To initialize the hosting. Select `NextJs` with `App Route`.
```sh
firebase init hosting
```
- To enable emulators:
```sh
firebase init emulators
```
- To run emulators, so you can test your app locally:
```sh
firebase emulators:start
```
Emulators run fast build, which means each update to the code is reflected in real time to your locally hosted website.

- To run the hosting together with all the firebase services.
```sh
firebase deploy
```

### Improper `.firebase` caching messing up with emulators
- `.firebase` folder represents the cache build after `firebase deploy`. The hosting emulator will reuse this without rebuilding the `NextJs` source code.
  - To properly use emulators with Next.js you need to delete `.firebase` after deployment. One solution is done add a post deployment script to the hosting configuration in `firebase.json`. Add `"postdeploy":` followed by the script:
  
```sh
powershell.exe -Command "Remove-Item -Path .firebase -Force -Recurse"
```

### Changing regions
- To change region for your Firebase Functions: `setGlobalOptions({region: "europe-west1"});`
- To change region for your frontend (hosting): Go `firebase.json` -> `"hosting"` -> add `"frameworksBackend": {"region": "europe-west1"}` or any other region available. (`"europe-west1"` is recommended out of latency and security reasons).
- To invoke your **Client-side** functions with your specific region: 
```javascript
export const functions = getFunctions(app,"europe-west1");
```
These functions will be tied to the correct region and calling them will reach `europe-west1` in our case.