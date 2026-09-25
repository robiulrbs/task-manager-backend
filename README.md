# Task Manager Backend

A RESTful Task Manager API built with Spring Boot and Java 21. The application provides CRUD operations for tasks, request validation, structured error handling, and separate configuration for local development and production deployment.

The backend is deployed on Render and uses PostgreSQL in production.

## Live API

**Production API:**

https://task-manager-backend-31a4.onrender.com

Example:

```text
GET /api/tasks
```

## Features

- Create tasks
- View all tasks
- View a single task
- Update tasks
- Delete tasks
- Task completion status
- Request validation
- DTO-based API design
- Global exception handling
- Custom 404 responses
- Environment-based configuration
- CORS configuration
- Docker support
- PostgreSQL production database
- MySQL local development database

## Tech Stack

| Technology | Purpose |
|---|---|
| Java 21 | Programming language |
| Spring Boot | Backend framework |
| Spring Web | REST API |
| Spring Data JPA | Database access |
| Hibernate | ORM |
| MySQL | Local development database |
| PostgreSQL | Production database |
| Maven | Build and dependency management |
| Docker | Containerization |
| Render | Backend deployment |
| Git & GitHub | Version control |

## Project Structure

```text
src/
└── main/
    └── java/
        └── com/example/taskmanager/
            ├── config/
            │   └── CorsConfig.java
            ├── controller/
            │   └── TaskController.java
            ├── dto/
            │   ├── TaskRequest.java
            │   └── TaskResponse.java
            ├── entity/
            │   └── Task.java
            ├── exception/
            │   ├── GlobalExceptionHandler.java
            │   └── TaskNotFoundException.java
            ├── repository/
            │   └── TaskRepository.java
            └── service/
                └── TaskService.java
```

## API Endpoints

Base URL:

```text
https://task-manager-backend-31a4.onrender.com
```

### Get all tasks

```http
GET /api/tasks
```

### Get a task

```http
GET /api/tasks/{id}
```

Example:

```http
GET /api/tasks/1
```

### Create a task

```http
POST /api/tasks
Content-Type: application/json
```

Request:

```json
{
  "title": "Learn Docker",
  "description": "Containerize the Spring Boot application",
  "completed": false
}
```

### Update a task

```http
PUT /api/tasks/{id}
Content-Type: application/json
```

Request:

```json
{
  "title": "Learn Docker",
  "description": "Build and run the application using Docker",
  "completed": true
}
```

### Delete a task

```http
DELETE /api/tasks/{id}
```

Successful response:

```text
204 No Content
```

## Validation

Task titles are required and limited to 100 characters.

Descriptions are limited to 500 characters.

Example invalid request:

```json
{
  "title": "",
  "description": "Test"
}
```

Response:

```json
{
  "error": "Validation failed",
  "status": 400,
  "errors": {
    "title": "Title is required"
  }
}
```

## Error Handling

The API provides structured responses for common errors.

Example:

```http
GET /api/tasks/1000000
```

Response:

```json
{
  "error": "Not Found",
  "message": "Task not found",
  "status": 404
}
```

## Local Development

### Requirements

- Java 21
- Maven
- MySQL
- Git

### 1. Clone the repository

```bash
git clone https://github.com/robiulrbs/task-manager-backend.git
cd task-manager-backend
```

### 2. Create the database

Create a MySQL database:

```sql
CREATE DATABASE task_manager;
```

### 3. Configure environment variables

Create a `.env` file in the project root:

```env
DATABASE_URL=jdbc:mysql://localhost:3306/task_manager
DB_USERNAME=root
DB_PASSWORD=your_mysql_password
PORT=8080
FRONTEND_URL=http://localhost:5173
```

The `.env` file should never be committed to Git.

### 4. Run the application

```bash
./mvnw spring-boot:run
```

The API will be available at:

```text
http://localhost:8080
```

## Building the Application

```bash
./mvnw clean package
```

The generated JAR file will be placed inside:

```text
target/
```

## Docker

The project includes a multi-stage Dockerfile.

Build the image:

```bash
docker build -t task-manager-backend .
```

Run the container:

```bash
docker run --env-file .env -p 8080:8080 task-manager-backend
```

## Deployment

The backend is deployed using Render.

Deployment flow:

```text
GitHub
   ↓
Render
   ↓
Docker Build
   ↓
Spring Boot Application
   ↓
PostgreSQL
```

Every push to the `main` branch can trigger a new deployment on Render.

## Frontend

The React frontend is deployed separately on Vercel.

Frontend repository:

https://github.com/robiulrbs/task-manager-frontend

Live application:

https://task-manager-frontend-xi-three.vercel.app

## Testing

The API was tested using Postman.

Tested operations include:

- Create task
- Retrieve tasks
- Retrieve individual task
- Update task
- Delete task
- Validation errors
- Resource-not-found errors
- Production API requests

## Environment Configuration

Local development uses MySQL:

```text
MySQL → Spring Boot
```

Production uses PostgreSQL:

```text
PostgreSQL → Spring Boot
```

The application uses environment variables so database credentials and deployment-specific configuration are not stored directly in source code.

## License

This project is intended for learning and portfolio purposes.
