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
- Add Cognito in your backend using Amplify CLI
` amplify auth add`
- Then push hthe configuration to build the resources and build it in AWS
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
1. Using Authenticator Component


2. Use your own Components + Amplify API calls



