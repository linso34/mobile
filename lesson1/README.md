# Lesson 1 - AWS Amplify and AWS Mobile Hub Introduction

AWS provides 2 services to simplify the development of Mobile applications and especially to create the backend environment in the cloud, AWS Mobile Hub and AWS Amplify.
You the workshop you can use either one of them.

## 1. AWS Mobile Hub

AWS Mobile Hub provides an integrated console that helps you build, test, and monitor your mobile apps. Use the console to choose the features you want to include in your app. Mobile Hub then provisions and configures the necessary AWS services on your behalf and creates a working sample app for you.

AWS Mobile Hub helps to create the below "features" and the related services in AWS Cloud:

* user-signin - Amazon Cognito
* user-files - Amazon S3 for file storage
* cloud-api - API Gateway and AWS Lambda
* database - Amazon DynamoDB
* analytics - Amazon Pinpoint
* hosting - Amazon S3 and Amazon Cloudfront for static website
* appsync - AWS AppSync
* Conversational Bots - Amazon Lex

This can be done either on the AWS Console or by using the AWS Mobile CLI.

### Installing & configuring a new mobile hub project.

- Installing the AWS Mobile CLI

`npm i -g awsmobile-cli`
- Configuring the CLI

`awsmobile configure`

If you need to get an accessKeyId & secretAccessKey:

* Visit the IAM Console.
* Click Users in left hand menu.
* Click Add User.
* Give the user a name & choose programatic access as the access type & click next.
* Click Create Group.
* Give the group a name & choose Administrator Access as the access type & click Create Group.
* Click Next & click Create User.
* Copy the accessKeyId & secretAccessKey to the terminal to configure the CLI.

- Creating a new Project

`awsmobile init`

After running the above command you will have a few options:

```Choose default for source directory
Choose default for project's distribution directory
Choose default for build command
Choose default for project's start command
Give the project a name of AmplifyReact
```

Now that the project is successfully created, we can view it in the AWS Console by running the following command:

`awsmobile console`

## 2. AWS Amplify

AWS Amplify is a JavaScript library for frontend and mobile developers building cloud-enabled applications.
AWS Amplify provides a declarative and easy-to-use interface across different categories of cloud operations. AWS Amplify goes well with any JavaScript based frontend workflow, and React Native for mobile developers.

AWS Amplify helps to create the AWS resources for the below category:

* analytics - To collect analytics data for you app
* API - For HTTP requests to REST and GraphQL endpoints
* Authentication - To provide Authentication APIs
* function - To provide backend integration with AWS Lambda, AWS API-Gateway, Amazon DynamoDB
* hosting - To provide an hosting solution for static files on Amazon S3 + Amazon CloudFront      
* notifications - To integrate push notifications
* storage - To provide a simple mechanism for managing user content for your app in public, protected or private storage buckets.
* Interactions - To enable AI-powered chatbots


### Integrate with AWS Amplify

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
