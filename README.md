# Serverless-Application

🚀 I completed Project of AWS Cloud On, A Server less Real-time Chat Application with Global
Distribution is a chat app that allows users from all over the world to send and receive messages
instantly, without you having to manage any servers.

👨💻In the Project we basically hosted Chat application on Serverless; you don't manage any servers.
AWS handles the infrastructure, so you only focus on your code. • Real-time: Messages are sent and
received instantly, without delays. • Global Distribution: The chat app can be accessed from anywhere in
the world, with low latency.

✨Get ready to enhance your AWS skills and boost your confidence in cloud technology☁

Prerequisites -
Before we start, make sure you have:-
An AWS account
• Basic understanding of AWS Lambda, Dynamo DB, and API Gateway
• AWS CLI and Node.JS installed (optional, if you're using Cloud Formation)

Step 1 - Step 1: Create Lambda Functions and a Dynamo DB Table:
In this step, we will create the necessary backend components for your serverless chat application.
These components include Lambda functions to manage client connections and a DynamoDB table to
store each client's unique ID.
Download and Unzip the CloudFormation Template
https://docs.aws.amazon.com/apigateway/latest/developerguide/samples/ws-chat-app-starter.zip
1. Download the Template: Obtain the CloudFormation template file that will set up your DynamoDB
table and Lambda functions. This file is usually provided in .yaml and .json format.
2. Unzip the Template: if the template is in a compressed format (e.g.zip), unzip it to access the .yaml or
.json file. Deploy the CloudFormation Stack
1. Open AWS Management Console: Go to the AWS Management Console.
2. Navigate to CloudFormation: In the AWS Management Console, search for and select
"CloudFormation".
3. Create a New Stack: Click on "Create stack" and then choose "With new resources (standard)".
4. Upload the Template File: In the "Specify template" section, choose "Upload a template file, Select
the .yaml or .json file you unzipped earlier.”
5. Configure the Stack: Give your stack a name, such as serverless-chat and then choose next
6. For Configure stack options no changes, choose next.
7. For Capabilities, acknowledge that AWS CloudFormation can create IAM resources in your account.
Choose submit , AWS CloudFormation provisions the resources specified in the template. It can take a
few minutes to finish provisioning your resources.
[Fig 1: Successful Creation of AWS CloudFormation stack]
8. When the status of your AWS CloudFormation stack is CREATE_COMPLETE, you're ready to move on
to the next step.

Step 2 - Create a Web Socket API:
You'll create a Web Socket API to handle client connections and route requests to the Lambda functions
that you created in Step 1.
Create a New Web Socket API
1. Choose "Create API“On the API Gateway homepage, select "Create API".
2. Select WebSocket API: under "Choose an API type", select "WebSocket API". Click "Build" to start
building your WebSocket API.
3. Enter API Details: API Name: Enter serverless-chatapp-ap as the name of your API. Route Selection
Expression: Enter request.body.action.
4. Define Routes: For Predefined routes, choose Add $connect, Add $disconnect, and Add $default.
The $connect and $disconnect routes are special routes that API Gateway invokes automatically when
a client connects to or disconnects from an API. API Gateway invokes the $default route when no other
routes match a request.
5. Integrate Routes with Lambda Functions:
Once you have created the WebSocket API and defined your routes, the next steps involve integrating
these routes with the appropriate Lambda functions that were created earlier. This will allow your API
to handle client connections, disconnections, and message transmissions.
Attach Integrations
1. For Each Route, Choose Integration Type as Lambda:
2. In the API Gateway console, you’ll see the routes you defined earlier ($connect, $disconnect, send
message, and $default), Attach Lambda Functions to Routes...
6. Review all steps and deploy the WebSocket API
[Fig 2: Successful Creation of API’S]

Step 3 - Test your API:
3.1 - Next, you'll test your API to make sure that it works correctly. Use the wscat command to connect
to the API, to connect to your API – open CMD Prompt – type Below Command – wscat –c {Paste API
URL}
Wscat -c wss://abcdef123.execute-api.us-west-2.amazonaws.com/production
3.2 - .Open a new command prompt terminal and run the wscat command again with the following
parameters.
Wscat -c wss://abcdef123.execute-api.us-west-2.amazonaws.com/production
To send message as a result, API Gateway invokes the send message route when you send the following
message: • {"action": "send message", "message": "hello, everyone!"}
The Lambda function associated with the invoked route collects the client IDs from DynamoDB. Then,
the function calls the API Gateway Management API and sends the message to those clients. All
connected clients receive the following message: • < hello, everyone!

Step 4: Clean up -
To prevent unnecessary Costs, Delete the resources that you created as part of this tutorial.
