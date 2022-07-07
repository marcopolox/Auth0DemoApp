# [OKTA/AUTH0 CIAM Demo App](https://okta.com)



https://user-images.githubusercontent.com/4019770/176539385-99bc82d6-8616-4589-bb23-36fcbd0863ce.mp4

## Terminal Commands

1. Download and Install NodeJs from [NodeJs Official Page](https://nodejs.org/en/download/).
2. Navigate to the root / directory and run npm install to install the dependencies.

## Documentation
There are two files you need to worry about (rename them to .env and LOCAL-VARS.js respectively, before starting the app):
1. .env file in the root of the directory (note: CLIENT_SECRET and SECRET are the same values)
2. LOCAL-VARS.js in the assets->js folder 


You will need to do a bit of a legwork within the Auth0 platform itself, mainly the following (probably in this order):
1. Create a Database connection (leave the default name Username-Password-Authentication)
2. Create a Social connection to Google and/or Facebook
3. Create an Enterprise connection to Azure (or some other iDP). You will need to build an authorization url and put it in the LOCAL-VARS.js file. Here is a sample Authorize url: 
https://login.microsoftonline.com/myaccount.onmicrosoft.com/oauth2/v2.0/authorize?login_hint=&response_type=code&client_id=your_ms_client_id&redirect_uri=https%3A%2F%2Fyour-auth0-tenant-url%2Flogin%2Fcallback&nonce=bg1QiFDkq5mq9IiyKb4v&scope=openid%20profile%20email%20https%3A%2F%2Fgraph.microsoft.com%2FUser.Read%20https%3A%2F%2Fgraph.microsoft.com%2FDirectory.Read.All&state=rGCvyR67FdK1uW2aWOYqTA3W9SIAu_nf
4. Create two organizations, name them organization-a and organization-b
5. Enable and configure SMS passwordless
6. Register a web application which will give you client_id and client_secret that you need. Under "Advanced Settings" in the Application enable all grant types. Under "Connections" enable the "Username-Password-Authentication" database, Google, Enterprise and SMS passwordless. Also, make sure you specify the correct allowed callback URLs when creating the app in Auth0 (for logout, web origins and CORS simply use http://localhost:9999):
http://localhost:9999/callback, http://localhost:9999/authn/embedded, http://localhost:9999/test, http://localhost:9999/authn/embedded-lock, http://localhost:9999/authn/embedded-auth0js, http://localhost:9999/orgs, http://localhost:9999/privacy
7. Create an API, using the following identifier: http://local.api; Create two permissions: view:balance and transfer:funds; Authorize the API for your web aplication you created previously and check both permissions


After you have created all the pieces within the Auth0 management UI, collect all the IDs, etc and update your .env and LOCAL-VARS.js files accordingly.

For Mobile section, you will need to do following:
1. Download and modify the Android sample app locally: https://github.com/auth0-samples/auth0-android-sample
2. Build the local app for distribution (.apk)
3. Test it locally to make sure it works then deploy to https://appetize.io/upload
4. Grab the appetize.io link for your deployed app and put it in the LOCAL-VARS.js file

Now run
```bash
$ npm start
```
Open your browser and go to http://localhost:9999

NOTE: You can save and deploy actions from within the demo app, however you will still need to go to the Auth0 Admin UI and put the Action into the flow (mainly Login flow). Also, (might be obvious, but) when saving Action if the action with the same name already exists you will get an error in the app.

Et Voila! You're welcome.
