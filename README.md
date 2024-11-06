# User Management API

This is a Node.js API for managing users with basic CRUD operations (Create, Read, Update, Delete). MongoDB is used as the database, and user authentication is enabled to ensure secure data access.

## Table of Contents

- [User Management API](#user-management-api)
  - [Table of Contents](#table-of-contents)
  - [Project Architecture](#project-architecture)
  - [Requirements](#requirements)
  - [Setup Instructions](#setup-instructions)
  - [Environment Variables](#environment-variables)
  - [Docker Setup](#docker-setup)
  - [Running the Application](#running-the-application)
  - [API Endpoints](#api-endpoints)
  - [Example Payloads for Testing](#example-payloads-for-testing)
  - [Additional Information](#additional-information)

## Project Architecture

The project is structured using the MVC (Model-View-Controller) pattern for better organization:
```
user_management_api
├── config
│   └── database.js
├── controllers
│   └── userController.js
├── models
│   └── userModel.js
├── routes
│   └── userRoutes.js
├── .env
├── server.js
└── package.json
```
## Requirements

- [Node.js](https://nodejs.org/) (v12+)
- [Docker](https://www.docker.com/) (to run MongoDB in a container)
- `bcrypt` for password hashing
- MongoDB (if not using Docker)

## Setup Instructions

1. **Clone the Repository**

   ```bash
   git clone https://github.com/your-username/user_management_api.git
   cd user_management_api
   ```

2. **Install Dependencies**

   ```bash
   npm install
   ```

## Environment Variables

Create a `.env` file in the root directory with the following variables:

```plaintext
MONGODB_URI=mongodb://admin:secret@localhost:27017/user_management_api?authSource=admin
PORT=3000
```

- `MONGODB_URI`: MongoDB connection URI with `authSource=admin` for authentication.
- `PORT`: The port where the Node.js server will run (default is 3000).

## Docker Setup

Run MongoDB in a Docker container with user authentication enabled.

1. **Run the MongoDB Container**

   ```bash
   docker run -d --name mongodb_container -p 27017:27017 -v mongo_data:/data/db -e MONGO_INITDB_ROOT_USERNAME=admin -e MONGO_INITDB_ROOT_PASSWORD=secret mongo
   ```

2. **Verify MongoDB Connection** (optional):
   To ensure MongoDB is working, connect with `mongosh`:

   ```bash
   mongosh "mongodb://admin:secret@localhost:27017/admin"
   ```

## Running the Application

1. **Ensure MongoDB is running** (either locally or via Docker).
2. **Start the Node.js server**:

   ```bash
   npm start
   ```

3. The API will be accessible at `http://localhost:3000/api`.

## API Endpoints

- **POST /api/users**: Register a new user. Passwords are securely hashed before storage.
- **POST /api/users/login**: Authenticate a user using email and password.
- **GET /api/users**: Retrieve all users.
- **PUT /api/users/:id**: Update a user by ID.
- **DELETE /api/users/:id**: Delete a user by ID.

## Example Payloads for Testing

Use Postman or any REST client to test the following endpoints.

1. **Register a New User** (`POST /api/users`)

   ```json
   {
     "name": "John Doe",
     "email": "johndoe@example.com",
     "password": "mySecretPassword"
   }
   ```

2. **Login User** (`POST /api/users/login`)

   ```json
   {
     "email": "johndoe@example.com",
     "password": "mySecretPassword"
   }
   ```

## Additional Information

For troubleshooting, ensure:

- The `.env` file is correctly loaded.
- MongoDB is running with the appropriate credentials.
- The connection URI includes `authSource=admin` if the user was created in the `admin` database.
