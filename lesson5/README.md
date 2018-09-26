# Lesson 5 - Adding Interactions capabilities using AWS Amplify

## 1. Architecture that will be achieved

<p align="center">
  <img src="../images/MobileWorkshop_Lex.jpg" />
</p>

## 2. Steps required to add Chatbot

1. Introduction to Amazon Lex

2. [Create your Amazon Lex Chatbot])(https://github.com/adamrb/amazon-ai-building-better-bots)

3. Integrate the chatbot with your mobile application

AWS Amplify Interactions category enables AI-powered chatbots in your web or mobile apps. You can use Interactions to configure your backend chatbot provider and to integrate a chatbot UI into your app with just a single line of code.

- The integration is currently manual and requires few steps 

* Add the Amplify configuration directly in the code.

```
import Amplify from 'aws-amplify';

Amplify.configure({
  Auth: {
    identityPoolId: 'us-east-1:xxx-xxx-xxx-xxx-xxx',
    region: 'us-east-1'
  },
  Interactions: {
    bots: {
      "BookTrip": {
        "name": "BookTrip",
        "alias": "$LATEST",
        "region": "us-east-1",
      },
    }
  }
});
```

* Update your code using the Amplify React Native ChatBot component

```
import {ChatBot, withAuthenticator} from 'aws-amplify-react-native';

class App extends React.Component {
 state = {
    botName: 'BookTrip',
    welcomeMessage: 'Welcome, what would you like to do today?',
 }
...
render() {
    const { botName, showChatBot, welcomeMessage } = this.state;
    return (
      
      <View style={styles.container}>
        <Text>Open up App.js to start working on your app!</Text>
        
        <Button title="Open" onPress={this.uploadPhoto} />
        <SafeAreaView style={styles.container}>
          <ChatBot
            botName={botName}
            welcomeMessage={welcomeMessage}
            onComplete={this.handleComplete}
            clearOnComplete={false}
            styles={StyleSheet.create({
                itemMe: {
                color: 'red'
                }
            })}
          />
        </SafeAreaView>
        
      </View>
```

* Add the handleComplete function

```
handleComplete(err, confirmation) {
    if (err) {
      console.log('Error', err);
    Alert.alert('Error', 'Bot conversation failed', [{ text: 'OK' }]);
    return;
    }

    Alert.alert('Done', JSON.stringify(confirmation, null, 2), [{ text: 'OK' }]);

    this.setState({
    botName: 'BookTrip',
    });

    return 'Trip booked. Thank you! what would you like to do next?';
}
```
* Add the IAM permissions to execute the Chatbot

- Retrieve the role names

```
aws cognito-identity list-identity-pools --max-result 10 --region us-east-1 //list all the cognito identity pools

>
{
    "IdentityPools": [
        {
            "IdentityPoolId": "us-east-1:asdfsdf", 
            "IdentityPoolName": "Name1"
        }, 
        {
            "IdentityPoolId": "us-east-1:sdsdlk-sdf-dsf", 
            "IdentityPoolName": "Name2"
        }, 
        {
            "IdentityPoolId": "us-east-1:identity-pool-id", 
            "IdentityPoolName": "cognitoxxxxx"
        }
    ]
}

aws cognito-identity get-identity-pool-roles --identity-pool-id us-east-1:identity-pool-id --region us-east-1
> 
{
    "IdentityPoolId": "us-east-1:identity-pool-id", 
    "Roles": {
        "unauthenticated": "arn:aws:iam::1111111:role/mypp02-1111111111-unauthRole", 
        "authenticated": "arn:aws:iam::1111111:role/mypp02-1111111111-authRole"
    }
}
```

- We would need to add Lex permissions on the authenticated IAM role
- Go to the AWS Console > IAM > Roles
- Search for mypp02-1111111111-authRole //The name of the role created by amplify
- Update the role with LexRunBot policy and Attach it




 
