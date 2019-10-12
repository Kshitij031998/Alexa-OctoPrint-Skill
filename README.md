# Amazon Alexa + OctoPi
A simple [AWS Lambda](http://aws.amazon.com/lambda) function that uses the [Alexa SDK](https://developer.amazon.com/alexa-skills-kit) to control [Octoprint](http://octoprint.org/) & [OctoPi](https://octopi.octoprint.org/).

## Concepts
Connect an Alexa Voice Service with Octoprint Running on a Raspberry Pi

## Setup
To run this skill you need to do a few setup things. The first is to deploy the code in Lambda, and the second is to configure the Alexa Skill to use Lambda.
On your OctoPi machine, you will need to install the Octoprint-Alexa-Plugin

### AWS Lambda Setup
1. Go to the AWS Console and click on the Lambda link. Note: Ensure you are in us-east or you won't be able to use Alexa with Lambda.
2. Click on the Create a Lambda Function or Get Started Now button.
3. Skip the blueprint
4. Name the Lambda Function "Alexa-OctoPi".
5. Select the runtime as Node.js
5. Go to the src directory, select the index.js file, enter the forwarded address from your OctoPi machine (i.e. 100.92.100.54) for the variable OCTO_PATH.
6. Back at the src directory, select all files and then create a zip file, make sure the zip file does not contain the src directory itself, otherwise Lambda function will not work.
6. Select Code entry type as "Upload a .ZIP file" and then upload the .zip file to the Lambda
7. Keep the Handler as index.handler (this refers to the main js file in the zip).
8. Create a basic execution role and click create.
9. Leave the Advanced settings as the defaults.
10. Click "Next" and review the settings then click "Create Function"
11. Click the "Event Sources" tab and select "Add event source"
12. Set the Event Source type as Alexa Skills kit and Enable it now. Click Submit.
13. Copy the ARN from the top right to be used later in the Alexa Skill Setup

### Alexa Skill Setup
1. Go to the [Alexa Console](https://developer.amazon.com/edw/home.html) and click Add a New Skill.
2. Set "OctoPi" as the skill name and "Octo Print" as the invocation name, this is what is used to activate your skill. For example, you would say: "Alexa, ask Octo Print for the printer status"
3. Select the Lambda ARN for the skill Endpoint and paste the ARN copied from above. Click Next.
4. Copy the Intent Schema from the included IntentSchema.json.
5. Copy the Sample Utterances from the included SampleUtterances.txt. Click Next.
6. [optional] go back to the skill Information tab and copy the appId. Paste the appId into the index.js file for the variable APP_ID,
   then update the lambda source zip file with this change and upload it to lambda again, this step makes sure the lambda function only serves a request from an authorized source. (Again, highly recommend this)
7. You are now able to start testing your sample skill! You should be able to go to the [Echo webpage](http://echo.amazon.com/#skills) and see your skill enabled.
8. In order to test it, try to say some of the Sample Utterances from the Examples section below.
9. Your skill is now saved and once you are finished testing you can continue to publish your skill.

### Octoprint Plugin Setup
1. Open Octoprint and Navigate to Settings
2. Open Plugins and type '' as the source
3. Install the plugin and reboot your Octoprint device
4. Open Octoprint and Navigate to Settings
5. Open Alexa Voice Service under Plugins
6. Continue with Authentication on Alexa

## Examples
    User: "Alexa, ask Octo Print for the printer status."
    Alexa: "Printer is not operational."
    
## Resources
