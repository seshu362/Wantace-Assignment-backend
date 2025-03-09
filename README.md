# Recipe Management System - Backend

This is the backend for a Recipe Management System built with **Node.js**, **Express**, and **SQLite**. It provides APIs for user authentication, recipe management, and image uploads.

## Features

- **User Authentication**:
  - Signup and login with JWT token-based authentication.
  - Password hashing using bcrypt.
- **Recipe Management**:
  - Create, read, update, and delete recipes.
  - Associate recipes with categories and users.
- **Image Upload**:
  - Upload recipe images using Multer.
  - Serve uploaded images statically.
- **Database**:
  - SQLite database for storing users, recipes, and categories.
  - Automatic table creation on startup.

## Technologies Used

- **Node.js**: JavaScript runtime for building the backend.
- **Express**: Web framework for handling HTTP requests.
- **SQLite**: Lightweight database for storing data.
- **bcrypt**: Library for hashing passwords.
- **jsonwebtoken (JWT)**: Library for generating and verifying authentication tokens.
- **Multer**: Middleware for handling file uploads.
- **express-validator**: Middleware for request validation.

---

## Setup Instructions

### 1. Install Dependencies
```
  npm install
```

### 2. Run the Server
Start the server in development mode:
```
  node server.js
```
The server will start on http://localhost:5000.

## API Documentation
Base Render Deploy URL
```
  https://wantace-assignment-backend.onrender.com
```
## API Endpoints 

## 1. User Authentication

### 1.1 Signup a New User
**Path:** `/signup`  
**Method:** `POST`  

#### Request Body:
```json
{
  "name": "John Doe",
  "email": "john@example.com",
  "password": "password123"
}
```

#### Response Body:
```json
{
  "id": 1,
  "name": "John Doe",
  "email": "john@example.com",
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
}
```

### 1.2 Login a User
**Path:** `/login`  
**Method:** `POST`  

#### Request Body:
```json
{
  "email": "john@example.com",
  "password": "password123"
}
```

#### Response Body:
```json
{
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
}
```

## 2. Recipes

### 2.1 Get All Recipes:
**Path:** `/recipes`  
**Method:** `GET`  
**Headers:** `Authorization: Bearer <JWT_TOKEN>`  

#### Response Body:
```json
[
  {
    "id": 1,
    "title": "Pasta",
    "description": "Delicious pasta recipe",
    "ingredients": "Pasta, Sauce, Cheese",
    "instructions": "Boil pasta, add sauce, and cheese.",
    "imageUrl": "http://localhost:5000/uploads/image.jpg",
    "categoryId": 1,
    "userId": 1,
    "createdAt": "2025-03-09T11:44:50.000Z"
  }
]
```
### 2.2 Get a Single Recipe:
**Path:** `/recipes/:id`  
**Method:** `GET`  
**Headers:** `Authorization: Bearer <JWT_TOKEN>`  

#### Response Body:
```json
{
  "id": 1,
  "title": "Pasta",
  "description": "Delicious pasta recipe",
  "ingredients": "Pasta, Sauce, Cheese",
  "instructions": "Boil pasta, add sauce, and cheese.",
  "imageUrl": "http://localhost:5000/uploads/image.jpg",
  "categoryId": 1,
  "userId": 1,
  "createdAt": "2025-03-09T11:44:50.000Z"
}
```
### 2.3 Update a Recipe:
**Path:** `/recipes/:id`  
**Method:** `PUT`  
**Headers:** `Authorization: Bearer <JWT_TOKEN>`  

#### Response Body:
```json
{
  "title": "Updated Pasta",
  "description": "Updated pasta recipe",
  "ingredients": "Pasta, Sauce, Cheese, Olive Oil",
  "instructions": "Boil pasta, add sauce, cheese, and olive oil.",
  "categoryId": 1,
  "imageUrl": "http://localhost:5000/uploads/updated_image.jpg"
}
```

#### Request Body:
```json
  {
    "message": "Recipe updated successfully"
  }
```
### 2.4 Create a Recipe:
**Path:** `/recipes`  
**Method:** `POST`  
**Headers:** `Authorization: Bearer <JWT_TOKEN>`  

#### Response Body:
```json
{
  "title": "Pasta",
  "description": "Delicious pasta recipe",
  "ingredients": "Pasta, Sauce, Cheese",
  "instructions": "Boil pasta, add sauce, and cheese.",
  "categoryId": 1,
  "imageUrl": "http://localhost:5000/uploads/image.jpg"
}
```

#### Request Body:
```json
  {
  "id": 1,
  "title": "Pasta",
  "description": "Delicious pasta recipe",
  "ingredients": "Pasta, Sauce, Cheese",
  "instructions": "Boil pasta, add sauce, and cheese.",
  "imageUrl": "http://localhost:5000/uploads/image.jpg",
  "categoryId": 1
}
```

## 3. Image Upload

### 3.1 Upload an Image:
**Path:** `/upload`  
**Method:** `POST`  
**Headers:** `Authorization: Bearer <JWT_TOKEN>` 
**Request Body:** `multipart/form-data with a file field named image.` 

#### Response Body:
```json
{
  "imageUrl": "http://localhost:5000/uploads/image.jpg"
}
```

## Database Schema

### Tables

#### 1. **Users**
| Column Name   | Data Type       | Description                          |
|---------------|-----------------|--------------------------------------|
| `id`          | INTEGER         | Primary key (auto-increment).        |
| `name`        | TEXT            | User's name.                         |
| `email`       | TEXT            | User's email (unique).               |
| `password`    | TEXT            | Hashed password.                     |
| `createdAt`   | TEXT            | Timestamp of creation.               |

#### 2. **Recipes**
| Column Name   | Data Type       | Description                          |
|---------------|-----------------|--------------------------------------|
| `id`          | INTEGER         | Primary key (auto-increment).        |
| `title`       | TEXT            | Recipe title.                        |
| `description` | TEXT            | Recipe description.                  |
| `ingredients` | TEXT            | Recipe ingredients.                  |
| `instructions`| TEXT            | Recipe instructions.                 |
| `imageUrl`    | TEXT            | URL of the recipe image.             |
| `categoryId`  | INTEGER         | Foreign key referencing `categories(id)`. |
| `userId`      | INTEGER         | Foreign key referencing `users(id)`. |
| `createdAt`   | TEXT            | Timestamp of creation.               |

#### 3. **Categories**
| Column Name   | Data Type       | Description                          |
|---------------|-----------------|--------------------------------------|
| `id`          | INTEGER         | Primary key (auto-increment).        |
| `name`        | TEXT            | Category name.                       |
| `userId`      | INTEGER         | Foreign key referencing `users(id)`. |
| `createdAt`   | TEXT            | Timestamp of creation.               |


