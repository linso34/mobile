# Mobile Workshop

The objective is to start to get familiar with AWS Mobile services, including AWS Amplify and building a simple chatbot mobile application.

## Building a simple "Hello World!" react native app with Authentication
  ### Prerequisites
  
- [XCode](https://developer.apple.com/xcode/)/[Android Studio](https://developer.android.com/studio/)
- Installing an IDE, such as [Visual Cloud Studio](https://code.visualstudio.com/download)
- [Node.js](https://nodejs.org/en/download/) and [npm](https://www.npmjs.com/get-npm)
    ```
    npm install -g react-native-cli
    npm install -g create-react-native-app
    ```
- [AWS Mobile CLI](https://github.com/aws/awsmobile-cli)
   ` npm install -g awsmobile-cli `
- (Optional) [Watchman](https://facebook.github.io/watchman/)
    On macOS, it is recommended to install it using [Homebrew](https://brew.sh/)
    ` brew install watchman`
- Install and configure AWS Amplify CLI - Follow the step by step guide
    ```
    npm install -g @aws-amplify/cli
    amplify configure
    ```
  
### Create the application

- Create a new React Native App (CRNA) using create-react-native-app
` create-react-native-app <appName> `
- cd into your new app dir.
` cd <appName> `
- Eject your react native app (in our examples call it "myapp")
` npm run eject `

```
? How would you like to eject from create-react-native-app? React Native: I'd like a regular React Native project.

We have a couple of questions to ask you about how you'd like to name your app:
? What should your app appear as on a user's home screen? 
? What should your Android Studio and Xcode projects be called? 
```

### Integration with AWS Amplify

- Install the dependencies
` npm install`
- Install aws-amplify and aws-amplify-react-native
```
npm install aws-amplify --save
npm install aws-amplify-react-native --save
```
- Set up your backend
You can quickly create your backend from scratch with Automatic Setup, using `amplify init`
```
? Choose your default editor: << choose-your-preferred editor >>
? Choose the type of app that you're building javascript
Please tell us about your project
? What javascript framework are you using react-native
? Source Directory Path:  src
? Distribution Directory Path: dist
? Build Command:  npm run-script build
? Start Command: npm run-script start
? Do you want to use an AWS profile? Yes
? Please choose the profile you want to use default
```
- Then push the configuration to build the resources
` amplify push`
When pushing the configuration, a configuration file for your app is put in your configured source directory called aws-exports.js
- Update your App.js to import Amplify and the configuration
```
import Amplify from 'aws-amplify';
import aws_exports from './src/aws-exports';
Amplify.configure(aws_exports)
```
- Run your application
` npm run android # npm run ios`

### Adding Authentication
1. Add the authentication component to your AWS environment, Cognito, using AWS Amplify

- Add Cognito in your backend using Amplify CLI
` amplify auth add`
- Then push the configuration to build the resources and build it in AWS
` amplify push`

2. Using Authenticator Component

For React and React Native apps, the simplest way to add authentication flows into your app is to use withAuthenticator High Order Component. 

withAuthenticator automatically detects the authentication state and updates the UI. If the user is signed in, the underlying component (typically your app’s main component) is displayed otherwise signing/signup controls is displayed.

- Configure your application
```
import { withAuthenticator } from 'aws-amplify-react-native';
...
export default withAuthenticator(App); # export default withAuthenticator(class App extends React.Component {
```
The withAuthenticator component adds Sign Up, Sign In with MFA and Sign Out capabilites to your app out of box.
Now, your app has complete flows for user sign-in and registration. Since you have wrapped your App with withAuthenticator, only signed in users can access your app. The routing for login pages and giving access to your App Component will be managed automatically.

3. Use your own Components + Amplify API calls

You can build your own UI Components and the API calls using Amplify. You would need to include:

- `import { Auth } from 'aws-amplify';`
Using the AWS Amplify Auth API Calls:

- SignIn
```
import { Auth } from 'aws-amplify';

Auth.signIn(username, password)
    .then(user => console.log(user))
    .catch(err => console.log(err));

// If MFA is enabled, sign-in should be confirmed with the congirmation code
// `user` : Return object from Auth.signIn()
// `code` : Confirmation code  
// `mfaType` : MFA Type e.g. SMS, TOTP.
Auth.confirmSignIn(user, code, mfaType)
    .then(data => console.log(data))
    .catch(err => console.log(err));
```

- SignUp
```
import { Auth } from 'aws-amplify';

Auth.signUp({
    username,
    password,
    attributes: {
        email,          // optional
        phone_number,   // optional - E.164 number convention
        // other custom attributes 
    },
    validationData: []  //optional
    })
    .then(data => console.log(data))
    .catch(err => console.log(err));

// After retrieveing the confirmation code from the user
Auth.confirmSignUp(username, code, {
    // Optional. Force user confirmation irrespective of existing alias. By default set to True.
    forceAliasCreation: true    
}).then(data => console.log(data))
  .catch(err => console.log(err));
  ```
- For complete list of API calls, refer to [Reac Native Documentation}(https://aws-amplify.github.io/amplify-js/media/authentication_guide)




