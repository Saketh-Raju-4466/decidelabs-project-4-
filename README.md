🎯 Project Objective

The primary objectives of this project were:

Understand the concept of Serverless Computing
Create an AWS Lambda Function
Use Python as the Lambda runtime
Pass data through an event payload
Perform basic processing inside the Lambda function
Return the result as JSON
Create and execute multiple test events
Understand Lambda's execution role
Use AWS IAM permissions
Verify Lambda execution using Amazon CloudWatch
Understand basic serverless architecture and execution

The project specifically demonstrates how application logic can run without manually provisioning or managing a traditional server.

☁️ What is Serverless Computing?

Serverless computing is a cloud-computing approach where developers can run application code without directly managing the underlying servers.

In a traditional application architecture, developers may need to manage:

Servers
Operating systems
Runtime environments
Infrastructure
Scaling
Server maintenance

With a serverless platform such as AWS Lambda, the cloud provider manages the underlying infrastructure while the developer focuses mainly on the application logic.

Traditional Architecture
Developer
    │
    ▼
Application
    │
    ▼
Server
    │
    ▼
Operating System
    │
    ▼
Infrastructure
Serverless Architecture
Developer
    │
    ▼
Lambda Function
    │
    ▼
AWS Managed Infrastructure

This allows developers to focus on writing and deploying code rather than maintaining servers.

⚡ What is AWS Lambda?

AWS Lambda is a serverless compute service provided by Amazon Web Services.

It allows code to execute in response to events without requiring the developer to maintain a traditional server.

For this project, AWS Lambda was used to:

Receive an event.
Read two numbers from the event.
Add the numbers.
Return the result.
Record execution information through CloudWatch.
🏗️ Project Architecture

The architecture of this project is intentionally simple so that the fundamental Lambda workflow can be understood clearly.

                 ┌─────────────────────┐
                 │     Test Event      │
                 │                     │
                 │  num1: 15           │
                 │  num2: 25           │
                 └──────────┬──────────┘
                            │
                            ▼
                 ┌─────────────────────┐
                 │     AWS Lambda      │
                 │                     │
                 │  Python Runtime     │
                 └──────────┬──────────┘
                            │
                            ▼
                 ┌─────────────────────┐
                 │   Lambda Handler    │
                 │                     │
                 │  num1 + num2        │
                 └──────────┬──────────┘
                            │
                            ▼
                 ┌─────────────────────┐
                 │    JSON Response    │
                 │                     │
                 │    Sum: 40          │
                 └─────────────────────┘
                            │
                            ▼
                 ┌─────────────────────┐
                 │   Amazon CloudWatch │
                 │                     │
                 │  Execution Logs     │
                 └─────────────────────┘
🛠️ Technologies Used
Technology	Purpose
AWS Lambda	Serverless function execution
Python	Programming language used for Lambda
AWS IAM	Managing Lambda execution permissions
Amazon CloudWatch	Monitoring and execution logs
JSON	Event input and function response
AWS Management Console	Creating, configuring and testing the Lambda function
📋 Project Requirements

The project required the implementation of a serverless function capable of:

Accepting two numbers.
Receiving those numbers through an event payload.
Performing an addition operation.
Returning the sum as JSON.
Testing the function with multiple inputs.
Verifying execution through CloudWatch.

The project also introduces the role of IAM execution permissions and CloudWatch in a Lambda workflow.

🚀 Implementation
Step 1 — Open AWS Lambda

The project was implemented using the AWS Management Console.

The AWS Lambda service was opened and a new Lambda function was created.

Step 2 — Create Lambda Function

A Lambda function was created with the following configuration:

Function Name:
decodelabs-project4-cost-calculator
Runtime
Python

The Python runtime was selected because the project required implementing the serverless logic using Python.

🐍 Step 3 — Implement the Lambda Function

The Lambda function contains a handler that receives the event payload and extracts the two numbers.

Lambda Source Code
def lambda_handler(event, context):
    num1 = event.get("num1")
    num2 = event.get("num2")

    total = num1 + num2

    return {
        "Sum": total
    }
🔍 Understanding the Code
Lambda Handler
def lambda_handler(event, context):

The lambda_handler function is the entry point for the Lambda execution.

AWS Lambda invokes this function whenever the function is executed.

The handler receives two parameters:

event

The event parameter contains the data sent to the Lambda function.

For this project, the event contains:

{
    "num1": 15,
    "num2": 25
}
context

The context parameter provides information about the Lambda execution environment.

It is included in the handler even though the basic addition logic does not require it.

📥 Step 4 — Reading the Input

The function retrieves the two numbers from the event:

num1 = event.get("num1")
num2 = event.get("num2")

The values are extracted using the corresponding JSON keys.

For example:

{
    "num1": 15,
    "num2": 25
}

Results in:

num1 = 15
num2 = 25
➕ Step 5 — Perform the Calculation

The two numbers are added:

total = num1 + num2

For example:

15 + 25 = 40
📤 Step 6 — Return the Result

The Lambda function returns the calculated value as JSON:

return {
    "Sum": total
}

The resulting response is:

{
    "Sum": 40
}
🧪 Step 7 — Create Test Event

AWS Lambda provides a built-in testing feature that allows the function to be invoked using custom event data.

The first test event used in this project was:

{
    "num1": 15,
    "num2": 25
}

Expected result:

{
    "Sum": 40
}
🧪 Step 8 — Execute the First Test

The Lambda function was executed using the test event.

Input
{
    "num1": 15,
    "num2": 25
}
Output
{
    "Sum": 40
}

This confirmed that the Lambda function successfully processed the event payload and performed the required calculation.

🧪 Step 9 — Execute Additional Tests

To ensure that the function was not working only for one specific input, additional test cases were created.

Test Case 1
{
    "num1": 15,
    "num2": 25
}

Expected output:

{
    "Sum": 40
}
Test Case 2
{
    "num1": 100,
    "num2": 250
}

Expected output:

{
    "Sum": 350
}

Testing multiple inputs demonstrates that the Lambda function performs the addition dynamically based on the event payload.

🔐 IAM Execution Role

AWS Lambda requires permissions to interact with other AWS services when necessary.

Lambda functions operate using an execution role provided through AWS Identity and Access Management (IAM).

The execution role defines what AWS resources and services the Lambda function is allowed to access.

For this project, the Lambda execution role is important for allowing the function to perform its execution and write relevant logs.

The project introduces IAM execution roles as part of the Lambda configuration.

📊 Amazon CloudWatch

Amazon CloudWatch was used to verify and inspect the Lambda execution.

CloudWatch provides logs and monitoring information related to Lambda executions.

The execution logs can be used to confirm that the function was successfully invoked.

Typical Lambda execution information can include:

START RequestId
...
END RequestId
REPORT RequestId
Duration
Billed Duration
Memory Size
Max Memory Used

This provides useful information about how the Lambda function executed.

🔎 CloudWatch Verification

After executing the Lambda function, the corresponding execution information was checked through CloudWatch.

This provides an additional verification layer beyond simply checking the returned JSON response.

The workflow was:

Invoke Lambda
      │
      ▼
Lambda executes
      │
      ▼
Execution completed
      │
      ▼
CloudWatch receives logs
      │
      ▼
Review execution information

CloudWatch verification is an important part of the project because it demonstrates how serverless functions can be monitored after deployment.

📁 Repository Structure

The repository is organized as follows:

DecodeLabs-Project-4-Serverless-Logic/
│
├── README.md
│
├── src/
│   └── lambda_function.py
│
├── test-events/
│   ├── test-event-1.json
│   └── test-event-2.json
│
└── screenshots/
    │
    ├── 01-lambda-function-created.png
    ├── 02-lambda-code.png
    ├── 03-test-event.png
    ├── 04-successful-test.png
    ├── 05-second-test.png
    ├── 06-execution-role.png
    ├── 07-cloudwatch-logs.png
    └── 08-project-completed.png
📸 Screenshots

Screenshots documenting the project implementation are available inside the screenshots directory.

1. Lambda Function Created

Shows the successfully created AWS Lambda function and its configuration.

screenshots/01-lambda-function-created.png
2. Lambda Python Code

Shows the Python serverless logic implemented inside the Lambda function.

screenshots/02-lambda-code.png
3. Test Event

Shows the JSON event used to test the Lambda function.

screenshots/03-test-event.png

Example:

{
    "num1": 15,
    "num2": 25
}
4. Successful Test Result

Shows the successful execution result.

screenshots/04-successful-test.png

Expected output:

{
    "Sum": 40
}
5. Second Test

Shows the Lambda function successfully processing another input.

screenshots/05-second-test.png

Example:

{
    "num1": 100,
    "num2": 250
}

Expected:

{
    "Sum": 350
}
6. IAM Execution Role

Shows the Lambda function's execution role and associated permissions.

screenshots/06-execution-role.png
7. CloudWatch Logs

Shows the Lambda execution logs and runtime information.

screenshots/07-cloudwatch-logs.png
8. Project Completion

Final screenshot showing the completed Lambda project.

screenshots/08-project-completed.png
🧪 Test Cases
Test Case	num1	num2	Expected Output
Test 1	15	25	40
Test 2	100	250	350
Test 1

Input:

{
    "num1": 15,
    "num2": 25
}

Output:

{
    "Sum": 40
}
Test 2

Input:

{
    "num1": 100,
    "num2": 250
}

Output:

{
    "Sum": 350
}
💻 Source Code

The complete Lambda source code is available at:

src/lambda_function.py
Complete Implementation
def lambda_handler(event, context):
    num1 = event.get("num1")
    num2 = event.get("num2")

    total = num1 + num2

    return {
        "Sum": total
    }
🧠 Key Concepts Learned

Through this project, I worked with and understood the following concepts:

1. Serverless Computing

Understanding how applications can execute without directly managing traditional servers.

2. AWS Lambda

Understanding how Lambda functions can run application logic on demand.

3. Event-Driven Execution

Understanding how Lambda receives an event payload and processes the provided data.

4. JSON Event Payloads

Understanding how structured JSON data can be passed into a Lambda function.

5. Lambda Handler

Understanding the role of the Lambda handler as the entry point for function execution.

6. IAM Execution Roles

Understanding how Lambda uses IAM roles to obtain required AWS permissions.

7. CloudWatch

Understanding how Lambda execution can be monitored and verified through CloudWatch logs.

8. Function Testing

Understanding how multiple test events can be used to verify serverless application logic.

🌐 Why Serverless?

Serverless architecture provides several advantages.

No Traditional Server Management

Developers do not need to manually manage the underlying server infrastructure for the Lambda function.

Event-Based Execution

Functions can execute when triggered by events.

Automatic Infrastructure Management

The cloud provider manages the underlying compute infrastructure.

Scalability

Serverless platforms are designed to handle changing workloads without requiring developers to manually manage traditional server infrastructure.

Focus on Application Logic

Developers can concentrate more on application functionality rather than server administration.

💰 Cost Efficiency

One of the important concepts associated with serverless computing is that resources are used when functions execute rather than requiring a continuously running traditional server.

For small workloads and event-driven applications, this can make serverless architectures particularly useful.

Note: This project was focused on understanding the serverless concept and AWS Lambda workflow rather than performing a detailed AWS cost analysis.

🔄 Complete Execution Flow

The complete implementation can be summarized as:

┌─────────────────────────┐
│      AWS Console        │
└────────────┬────────────┘
             │
             ▼
┌─────────────────────────┐
│     Create Lambda       │
│        Function         │
└────────────┬────────────┘
             │
             ▼
┌─────────────────────────┐
│   Select Python        │
│       Runtime           │
└────────────┬────────────┘
             │
             ▼
┌─────────────────────────┐
│  Implement Lambda       │
│        Handler          │
└────────────┬────────────┘
             │
             ▼
┌─────────────────────────┐
│     Create Test Event   │
│                         │
│  num1 + num2            │
└────────────┬────────────┘
             │
             ▼
┌─────────────────────────┐
│     Invoke Function     │
└────────────┬────────────┘
             │
             ▼
┌─────────────────────────┐
│     JSON Response       │
│                         │
│       Sum: 40           │
└────────────┬────────────┘
             │
             ▼
┌─────────────────────────┐
│     CloudWatch Logs     │
└─────────────────────────┘
🔐 AWS Services Used
AWS Lambda

Used to create and execute the serverless Python function.

AWS IAM

Used for the Lambda execution role and permissions.

Amazon CloudWatch

Used to inspect and verify Lambda execution logs.

🧩 Challenges & Learning

During the project, one of the important learning points was understanding the difference between writing application code and managing infrastructure.

In a traditional deployment model, deploying an application may involve configuring servers and runtime environments.

With AWS Lambda, the focus shifts toward:

Function
   ↓
Event
   ↓
Execution
   ↓
Response
   ↓
Monitoring

This helped strengthen my understanding of cloud-based application execution and serverless architecture.

📈 Possible Improvements

Although this project focuses on a simple addition function, the same architecture can be extended into more practical applications.

Possible improvements include:

Add subtraction functionality.
Add multiplication and division.
Validate input values.
Handle missing parameters.
Handle invalid data types.
Add error handling.
Create an API Gateway endpoint.
Connect Lambda to a frontend application.
Store results in a database.
Add structured logging.
Add monitoring and alerts.
Create a complete serverless REST API.

A possible future architecture could be:

Frontend
    │
    ▼
API Gateway
    │
    ▼
AWS Lambda
    │
    ├──────► Database
    │
    └──────► CloudWatch
📚 Project Outcome

By completing this project, I gained practical exposure to the basic workflow of building and testing a serverless application using AWS Lambda.

The project demonstrated:

AWS Lambda
     +
Python
     +
JSON Events
     +
IAM
     +
CloudWatch
     =
Serverless Application Workflow

The Lambda function successfully accepts two numbers through an event payload, performs the required addition, and returns the result as JSON.

✅ Project Completion Checklist
 Created AWS Lambda function
 Selected Python runtime
 Implemented Lambda handler
 Accepted input through event payload
 Implemented addition logic
 Returned result as JSON
 Created Lambda test event
 Tested function with multiple inputs
 Verified successful execution
 Reviewed IAM execution role
 Verified execution using CloudWatch
 Captured project screenshots
 Organized project files
 Prepared project documentation
📊 Skills Demonstrated
Cloud & AWS
AWS Lambda
AWS IAM
Amazon CloudWatch
Serverless Architecture
Event-Driven Computing
Programming
Python
Functions
Parameters
JSON
Basic arithmetic operations
Development
Testing
Debugging

👨‍💻 Author
Saketh Raju

B.Tech — Computer Science & Engineering (AI & ML)

Interested in:

Software Development
Artificial Intelligence & Machine Learning
Cloud Computing
Generative AI
Backend Development
Data Structures & Algorithms
Execution monitoring
Technical documentation
GitHub repository organization
