# Alexa Skill Apps - Notes

### Basic Definitions

Skills - built in capabilities for Alexa to give new customer experiences
	Example: skills in the app like hacker news, kayak

Invocation Name - how Alexa will identify what the user would like to do. Usually the name of your app, but more importantly how you will call upon it. Example - Weather app

Intent - what the user specifically wants to do. Example "Alexa, ask weather app for tomorrow's weather" - The intent is tomorrow's weather

Slots - variable set by the user. For example - alarm - When to set the alarm (4am) --> 4am is the variable. When to set is the intent, but the variable is the slot

Utterances - set sample utterances to improve accuracy of Alexa. Example - Set the alarm for 6am, alarm for 6am, 6am alarm --> specify as much as you can how something could be said

Command  - what the user essentially says to Alexa. Example - Alexa set AlarmMe to set alarm for 4am --> AlarmMe is invocation, set alarm is intent, 4am is slot

Intent Schema - what intents and slot look like in JSON format
	{
		"intents": {
			"intent": "Set alarm",
			"slots" : {
				"time": "4"
				"type": "am"
					}
				}
	}

### Setting it up

Need AWS account and AWS developer account.

Amazon Developer Services

Go to Lambda --> You see the functions --> You create a function and can create from scratch or use a preconfigured blueprint

Create a lambda function from scratch:

Name: Hello_world_1

Node.js 6.10

Choose an existing role

Lambda_basic_execution

When done creating function --> notice the ARN at the top right. Provides an inline editor

AWSCloud 9 --> you can add in your files

Add Alexa Skills Kit --> configure triggers -->

Enable and get skill id --> go to developer account and go under Alexa --> we can create 2 types of services --> add new service under alexa skills kit --> Custom Interaction Model, Name: hello_world_1 and invocation Name will be hello world - save - go back to skills and view skill Id - copy skill id and that is the way we are connecting to the lambdwea function. Click add and save - then go back to developer console.

We are going to go through the interaction model, configuration, test, publishing information, privacy & compliance and skills beta testing.

### Import Hello World Lambda Function

Key things to look at package.json and index.js

Variable Alexa = require('alexa-sdk')

```JavaScript
var Alexa = require('alexa-sdk');

exports.handler = function(event, context, callback) {
    var alexa = Alexa.handler(event, context);

    alexa.registerHandlers(handlers);
    alexa.execute();
};

var handlers = {
    'LaunchRequest': function() { //when Alexa is first envoked
        this.emit('LaunchIntent');
    },

    'LaunchIntent': function() {
        this.emit(':ask', "How are you today?");
    },

    'HelloIntent': function() { //intent schema and utterances
        this.emit(':tell', "I'm great. You have successfully created your first skill with Amazon Alexa.");
    }
};
```

### Intent Schema and Utterances

In the developer portal hit next to go to Interaction Model.

In the intent schema:
```JavaScript
	{
	  "intents": [{
	    "intent": "HelloIntent" 
	  }]
	}
```
	
Then in Utterances (things that can wake up the skill):

HelloIntent hello
HelloIntent open Hello World
HelloIntent how are you
HelloIntent hello world

Hit save, then hit next once the model has been built

Now we connect the endpoint. AWS resource Lambda name -- in the AWS services --> jump up to the ARN name and copy and paste. This connects it for us.  No to geographical endpoints. Then hit save

### Testing

Can test using text or voice in the developer's portal. Ensure device is connected to same account and can already use it.