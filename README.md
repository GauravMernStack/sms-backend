# OneTap Backend - NFC Digital Visiting Card System

Backend API for NFC digital visiting card management system with role-based access control.

## Features

- **Authentication System** - JWT-based authentication
- **Role-Based Access Control** - Admin and SuperAdmin roles
- **Admin Management** - SuperAdmin can manage admins
- **Error Handling** - Centralized error handling with custom error classes
- **Validation** - Input validation for all endpoints
- **Security** - Password hashing, token-based auth

## Tech Stack

- Node.js + Express
- MongoDB + Mongoose
- JWT Authentication
- bcryptjs for password hashing

## Project Structure

```
src/
├── config/
│   └── db.js                 # Database connection
├── controllers/
│   ├── auth.Controller.js    # Auth operations
│   └── adminController.js    # Admin management
├── middleware/
│   ├── auth.js              # JWT verification & authorization
│   ├── error.js             # Error handling middleware
│   └── roleCheck.js         # Role-based middleware
├── models/
│   └── Admin.js             # Admin model
├── routes/
│   ├── authRoute.js         # Auth routes
│   └── adminRoute.js        # Admin management routes
├── utils/
│   ├── AppError.js          # Custom error class
│   ├── asyncHandler.js      # Async wrapper
│   ├── message.js           # Message constants
│   ├── response.js          # Response helpers
│   └── validation.js        # Validation utilities
└── server.js                # Entry point
```

## Environment Variables

Create `.env` file:

```env
PORT=4000
NODE_ENV=development
MONGO_URI=mongodb://localhost:27017/onetap
JWT_SECRET=your_jwt_secret_key
JWT_EXPIRES_IN=7d
BCRYPT_SALT_ROUNDS=10
```

## Installation

```bash
npm install
```

## Run

```bash
# Development
npm run dev

# Production
npm start
```

## API Endpoints

### Authentication

| Method | Endpoint | Access | Description |
|--------|----------|--------|-------------|
| POST | `/api/v1/auth/register` | Public | Register new admin |
| POST | `/api/v1/auth/login` | Public | Login |
| GET | `/api/v1/auth/profile` | Private | Get profile |
| PUT | `/api/v1/auth/profile` | Private | Update profile |

### Admin Management (SuperAdmin Only)

| Method | Endpoint | Access | Description |
|--------|----------|--------|-------------|
| GET | `/api/v1/admins` | SuperAdmin | Get all admins |
| GET | `/api/v1/admins/:id` | SuperAdmin | Get admin by ID |
| PUT | `/api/v1/admins/:id/block` | SuperAdmin | Block admin |
| PUT | `/api/v1/admins/:id/unblock` | SuperAdmin | Unblock admin |
| DELETE | `/api/v1/admins/:id` | SuperAdmin | Delete admin |

## Request Examples

### Register
```json
POST /api/v1/auth/register
{
  "firstName": "John",
  "lastName": "Doe",
  "email": "john@example.com",
  "password": "password123",
  "phone": "1234567890"
}
```

### Login
```json
POST /api/v1/auth/login
{
  "email": "john@example.com",
  "password": "password123"
}
```

### Update Profile
```json
PUT /api/v1/auth/profile
Headers: { "Authorization": "Bearer <token>" }
{
  "firstName": "John Updated",
  "phone": "9876543210"
}
```

## Response Format

### Success Response
```json
{
  "success": true,
  "message": "Operation successful",
  "data": { ... }
}
```

### Error Response
```json
{
  "success": false,
  "message": "Error message",
  "stack": "..." // Only in development
}
```

## Roles

- **admin** - Regular admin user
- **superadmin** - Full access, can manage admins

## Security Features

- Password hashing with bcrypt
- JWT token authentication
- Role-based authorization
- Input validation
- Error handling
- Request size limits
- CORS enabled
