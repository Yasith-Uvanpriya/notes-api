# 📘 Notes API — Serverless CRUD Backend on AWS

## 📌 Overview

This project is a **serverless CRUD (Create, Read, Update, Delete) API** built using AWS services.
It allows users to manage notes through RESTful endpoints without requiring a frontend.

The system is designed using a **serverless architecture**, ensuring scalability, cost efficiency, and minimal infrastructure management.

---

## 🏗️ Architecture

Client (Postman) → API Gateway → Lambda Functions → DynamoDB

* **Client**: API testing via Postman
* **API Gateway**: Handles HTTP requests and routes them to Lambda
* **Lambda**: Executes backend logic
* **DynamoDB**: Stores notes data

---

## ☁️ AWS Services Used

* API Gateway (REST API)
* AWS Lambda (Node.js 20.x runtime)
* DynamoDB (NoSQL database with on-demand capacity)
* IAM (Identity and Access Management for permissions)

---

## ⚙️ Project Structure

```
notes-api/
├── src/
│   ├── create.js      # Create note
│   ├── getAll.js      # Get all notes
│   ├── getOne.js      # Get single note
│   ├── update.js      # Update note
│   └── delete.js      # Delete note
├── package.json
├── package-lock.json
└── README.md
```

---

## 🗄️ Database Design (DynamoDB)

Table Name: `notes`

| Attribute | Type   | Description           |
| --------- | ------ | --------------------- |
| id        | String | Primary key (UUID)    |
| title     | String | Note title            |
| content   | String | Note content          |
| createdAt | String | Creation timestamp    |
| updatedAt | String | Last update timestamp |

---

## 🚀 Setup Instructions

### 1. Create DynamoDB Table

* Navigate to DynamoDB
* Create table named `notes`
* Set partition key as `id` (String)
* Use default settings (on-demand mode)

---

### 2. Create IAM Role

* Go to IAM → Roles → Create Role
* Select **Lambda** as trusted entity
* Attach policies:

  * AmazonDynamoDBFullAccess
  * AWSLambdaBasicExecutionRole
* Name: `lambda-dynamodb-role`

---

### 3. Prepare Project Locally

```bash
npm install
```

* This installs required dependencies:

  * AWS SDK v3
  * UUID generator

---

### 4. Deploy Lambda Functions

Create 5 Lambda functions:

| Function Name | Handler            |
| ------------- | ------------------ |
| createNote    | src/create.handler |
| getAllNotes   | src/getAll.handler |
| getOneNote    | src/getOne.handler |
| updateNote    | src/update.handler |
| deleteNote    | src/delete.handler |

For each function:

* Upload ZIP file
* Select runtime: Node.js 20.x
* Choose IAM role: `lambda-dynamodb-role`
* Add environment variable:

```
TABLE_NAME = notes
```

---

### 5. Configure API Gateway

Create REST API named `notes-api`

#### Routes:

| Method | Path        | Lambda Function |
| ------ | ----------- | --------------- |
| POST   | /notes      | createNote      |
| GET    | /notes      | getAllNotes     |
| GET    | /notes/{id} | getOneNote      |
| PUT    | /notes/{id} | updateNote      |
| DELETE | /notes/{id} | deleteNote      |

Enable **Lambda Proxy Integration** for all endpoints.

---

### 6. Deploy API

* Create stage: `dev`
* Deploy API
* Copy invoke URL


---

## 🔗 API Endpoints

| Method | Endpoint    | Description        |
| ------ | ----------- | ------------------ |
| POST   | /notes      | Create a new note  |
| GET    | /notes      | Retrieve all notes |
| GET    | /notes/{id} | Retrieve a note    |
| PUT    | /notes/{id} | Update a note      |
| DELETE | /notes/{id} | Delete a note      |

---

## 🧪 Testing (Postman)

Set header:

```
Content-Type: application/json
```

### Sample Request

#### Create Note

```json
{
  "title": "My Note",
  "content": "Hello World"
}
```

---

## ✅ Features Implemented

* Full CRUD operations
* UUID-based unique IDs
* Timestamp tracking (createdAt, updatedAt)
* Proper error handling (400, 404, 500)
* Clean JSON responses
* Serverless architecture
* Environment variable usage

---

## 💰 Free Tier Usage

* DynamoDB: Free tier with on-demand capacity
* Lambda: 1 million requests/month free
* API Gateway: Free tier available for first 12 months

---

## 📦 Deliverables

* GitHub Repository
* Postman Collection (exported)
* Screenshots / Demo video
* README documentation

