# Notes API — Serverless AWS

## Architecture
Client → API Gateway (REST) → Lambda → DynamoDB

## AWS Services
- API Gateway (REST API)
- AWS Lambda (Node.js 20.x)
- DynamoDB (On-demand)
- IAM (execution role)

## Setup
1. Create DynamoDB table `notes` with partition key `id`
2. Create IAM role with DynamoDB + Lambda permissions
3. Deploy each Lambda with TABLE_NAME env var
4. Create REST API in API Gateway and link methods
5. Deploy to `dev` stage

## Endpoints
| Method | Path          | Description     |
|--------|---------------|-----------------|
| POST   | /notes        | Create a note   |
| GET    | /notes        | Get all notes   |
| GET    | /notes/{id}   | Get one note    |
| PUT    | /notes/{id}   | Update a note   |
| DELETE | /notes/{id}   | Delete a note   |