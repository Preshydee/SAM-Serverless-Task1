
```markdown
# SAM ToDo List App

I created this Serverless Application Model (SAM)-based ToDo List App using AWS Lambda, API Gateway, and DynamoDB. The application is designed to showcase a fully functional serverless architecture with CRUD operations for managing to-do items.

## Prerequisites

To set up this project, ensure the following are installed and configured:

1. **AWS CLI** - [Installation Guide](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html)
2. **AWS SAM CLI** - [Installation Guide](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/install-sam-cli.html)
3. **Node.js** - Version `22.x` or higher ([Download](https://nodejs.org/))
4. **IAM Permissions**:
   - I ensured that all Lambda functions adhere to the principle of least privilege by using scoped-down IAM roles and policies. You will need permissions to create Lambda functions, API Gateway endpoints, and DynamoDB tables.
5. **AWS Account**:
   - An active AWS account is required to deploy the application.
6. **Text Editor or IDE**:
   - I recommend using a code editor like Visual Studio Code for modifying the application code.

---

## Project Structure

Below is the structure of the project I created:

```plaintext
.
├── template.yaml       # SAM Template defining resources
├── handler.js          # Lambda functions' code
├── package.json        # Dependencies for Node.js
└── README.md           # Documentation
```

---

## Setup Instructions

### Step 1: Clone the Repository
Clone the repository I created to your local system:
```bash
git clone <repository-url>
cd <repository-folder>
```

### Step 2: Install Dependencies
Install the required Node.js dependencies:
```bash
npm install
```

### Step 3: Validate the SAM Template
Validate the SAM template to ensure it is correctly configured:
```bash
sam validate
```

### Step 4: Build the Application
Use the SAM CLI to build the application:
```bash
sam build
```

### Step 5: Deploy the Application
Deploy the application to AWS. Make sure you have the required permissions and provide a unique S3 bucket for the deployment artifacts:
```bash
sam deploy --guided
```
During deployment:
- Specify a stack name (e.g., `todo-list-stack`).
- Provide an S3 bucket name for SAM artifacts.
- Accept the default values or customize as needed.

---

## Application Overview

The app includes the following endpoints:

1. **Create To-Do**: `POST /todo`
2. **Get All To-Dos**: `GET /todos`
3. **Get To-Do by ID**: `GET /todos/{id}`
4. **Update To-Do**: `PUT /todos`
5. **Delete To-Do**: `DELETE /todos/{id}`

These endpoints are backed by AWS Lambda functions and a DynamoDB table.

---

## Least Privilege IAM Configuration

I ensured all Lambda functions have the minimum necessary permissions by using IAM policies like `DynamoDBCrudPolicy`. The `template.yaml` file includes these scoped-down permissions:
```yaml
Policies:
  - DynamoDBCrudPolicy:
      TableName: !Ref TodosDynamoDbTable
```
You can customize these policies further based on your specific requirements.

---

## Testing the Application

Once deployed, you can test the endpoints using tools like Postman or curl. For example, to create a new to-do:
```bash
curl -X POST -H "Content-Type: application/json" \
-d '{"id": "1", "task": "Write documentation"}' \
https://<api-endpoint>/todo
```

---

## Cleanup

To delete the resources created by this application, run:
```bash
sam delete
```
This will remove the stack and all associated AWS resources.

---
