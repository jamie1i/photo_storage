# ROLLINGTRANS-API

This project provides API functions.

## How to get started

This project was initialized with [Firebase CLI](https://firebase.google.com/docs/cli/) and deployed to [Firebase Cloud Functions](https://firebase.google.com/docs/functions/get-started).

## Setting up

1. [Node.js](https://nodejs.org/) and [npm](https://www.npmjs.org/) are required.

2. Install the Firebase CLI via npm:

```bash
npm install -g firebase-tools
```

3. Clone or download this repo and open the `rollingtrans-api` directory.

4. Login with:

```bash
firebase login
```

5. Install Cloud Functions dependencies locally by running:

```bash
cd functions; npm install; cd ..
```

## Test and Deploy

### on local

Read the reference [Run Functions Locally](https://firebase.google.com/docs/functions/local-emulator).

- The old method

```bash
firebase serve --only functions
```

- The latest tool: Local Emulator Suite

1. **_Node.js version 16_** and **_[Java](https://openjdk.java.net/install/) JDK version 11 or higher_** are required.

2. Set up the Emulator Suite. (Select emulators you need, like firestore and functions.)

```bash
firebase init emulators
```

3. Start the emulators

If you need to start with an empty local firestore, run:

```bash
firebase emulators:start
```

or you'd like to export data on shutdown and start with the saved data in the firestore, then run:

```bash
firebase emulators:start --import=./dir --export-on-exit
```

could save it in `package.json` and start it in a faster way if you prefer

### **Appendix**

**Reminder:**

If you need to run backup api, make sure that the firestore emulator is off.
You could simply run:

```bash
firebase emulators:start --only functions
```

**Troubleshooting:**

- _Error: Could not start "Specific" Emulator, port taken._

There are 3 ways you could try:

1. Turn off AirPlay Receiver on Mac.

2. Find the Process ID (PID) and then kill the process.

```bash
sudo lsof -i :[PORT]
```

```bash
sudo kill -9 [PID]
```

3. Change port in `firebase.json`

- _If you experience Java heap space related errors, you may increase the maximum Java heap size to 4GB._

Read the reference [Specifying Java options](https://firebase.google.com/docs/emulator-suite/install_and_configure#specifying_java_options).

```bash
export JAVA_TOOL_OPTIONS="-Xmx4g"
firebase emulators:start
```

### on development environment

```bash
firebase use dev; firebase deploy --only functions
curl 'https://developer.rollingtrans.com/api/v1/validateDotNumber?dotNumber=44110';echo
curl -H "Content-Type: application/json" -d '{"email": "foo@bar.com","password": "123456","dotNumber":"44110", "freeTrial":true, "vehicleLimits": 10, "accountLimits": 20}' 'https://developer.rollingtrans.com/api/v1/createUser';echo
curl -H "Content-Type: application/json" -d '{"email": "foo@bar.com","password": "123456","dotNumber":"44110", "freeTrial":true, "vehicleLimits": 10, "accountLimits": 20, "legalName": "Test name", "phyStreet": "Test street", "phyCity": "Test city", "phyState": "Test state", "phyZip": "11111-1111", "phyCountry": "Test country", "firstName": "Foo", "lastName": "Bar"}' 'https://developer.rollingtrans.com/api/v1/createUser';echo
```

## Test Backup Api by Postman

1. Set your HTTP request to GET.

2. Input link in the request URL field.

3. Switch to the Params tab and write parameters needed for the request.

![Testing with postman](https://github.com/jamie1i/Setting-up-a-Work-Environment-for-Angular/blob/main/img/%E6%88%AA%E5%9C%96%202022-10-25%20%E4%B8%8B%E5%8D%8812.27.31.png?raw=true)

4. Switch to the Headers tab and add an `Authenticated Email`.

Please note that the requested email is case-sensitive and must be spelled precisely. The api can only be used with authenticated emails.

![Authenticated Email](https://github.com/jamie1i/Setting-up-a-Work-Environment-for-Angular/blob/main/img/%E6%88%AA%E5%9C%96%202022-10-25%20%E4%B8%8B%E5%8D%8812.44.04.png?raw=true)

5. Click Send.
