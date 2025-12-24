# Mess Finder - Mess Management System

A full-stack web application that helps users find and subscribe to mess services, and allows mess owners to manage their mess information and subscribers.

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Installation](#installation)
- [API Documentation](#api-documentation)
- [Frontend Pages](#frontend-pages)
- [Database Schema](#database-schema)
- [Running the Application](#running-the-application)

---

## 🎯 Overview

Mess Finder is a platform that connects mess owners with potential customers. Users can browse available mess services, subscribe/unsubscribe to mess services, while mess owners can register their mess and manage their subscriber base.

---

## ✨ Features

### For Users:
- User registration and authentication
- Browse available mess services
- View mess details (location, about, established year)
- Subscribe/Unsubscribe to mess services
- User profile management

### For Mess Owners:
- Mess registration with detailed information
- Profile management
- View subscriber list
- Track total subscribers count

---

## 🛠️ Tech Stack

### Backend
- **Runtime**: Node.js
- **Framework**: Express.js v5.1.0
- **Database**: MongoDB (Local)
- **ODM**: Mongoose v8.16.3
- **Authentication**: JSON Web Tokens (JWT) v9.0.2
- **Password Hashing**: Bcrypt v6.0.0
- **File Upload**: Multer v2.0.1
- **CORS**: CORS v2.8.5
- **Dev Tool**: Nodemon v3.1.10

### Frontend
- **HTML5**
- **CSS3** (with responsive design)
- **Vanilla JavaScript**
- **Fetch API** for HTTP requests

---

## 📁 Project Structure

```
mess project/
│
├── backend/
│   ├── config/
│   │   └── db.js                 # MongoDB connection configuration
│   ├── middleware/               # Custom middleware (if any)
│   ├── model/
│   │   ├── mess.model.js         # Mess schema and model
│   │   └── user.model.js         # User schema and model
│   ├── routes/
│   │   ├── mess.routes.js        # Mess-related API routes
│   │   └── user.routes.js        # User authentication routes
│   ├── uploads/                  # Directory for uploaded files
│   ├── index.js                  # Main server file
│   └── package.json              # Backend dependencies
│
└── frontend/
    ├── index.html                # Landing/Home page
    ├── auth.html                 # Authentication page
    ├── login.html                # User login page
    ├── userauth.html             # User-specific authentication
    ├── messauth.html             # Mess owner authentication
    ├── findmess.html             # Browse mess services
    ├── profile.html              # User/Mess profile page
    ├── stle.css                  # Main stylesheet (responsive)
    └── auth.css                  # Authentication page styles
```

---

## 🚀 Installation

### Prerequisites
- Node.js (v14 or higher)
- MongoDB (Local installation)
- npm or yarn package manager

### Steps

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd "mess project"
   ```

2. **Install Backend Dependencies**
   ```bash
   cd backend
   npm install
   ```

3. **Configure Database**
   - Ensure MongoDB is running locally on `mongodb://127.0.0.1:27017/`
   - Database name: `messfinder`
   - No additional configuration needed (uses default settings)

4. **Start the Backend Server**
   ```bash
   npm run server
   ```
   The server will run on `http://localhost:8080`

5. **Access Frontend**
   - The frontend is served statically by the Express server
   - Open your browser and navigate to `http://localhost:8080`

---

## 📡 API Documentation

### Base URL
```
http://localhost:8080
```

---

### User Routes (`/user`)

#### 1. Register User
- **Endpoint**: `POST /user/register`
- **Description**: Register a new user
- **Request Body**:
  ```json
  {
    "name": "John Doe",
    "email": "john@example.com",
    "password": "securepassword"
  }
  ```
- **Response**: `"Registered successfully"` or `400` if user exists

#### 2. Login User
- **Endpoint**: `POST /user/login`
- **Description**: Authenticate user and receive JWT token
- **Request Body**:
  ```json
  {
    "email": "john@example.com",
    "password": "securepassword"
  }
  ```
- **Response**:
  ```json
  {
    "token": "jwt_token_here",
    "name": "John Doe"
  }
  ```

#### 3. Get User Profile
- **Endpoint**: `GET /user/find`
- **Description**: Get authenticated user details
- **Headers**: 
  ```
  Authorization: <jwt_token>
  ```
- **Response**: User object with details

---

### Mess Routes (`/mess`)

#### 1. Register Mess
- **Endpoint**: `POST /mess/register`
- **Description**: Register a new mess
- **Request Body**:
  ```json
  {
    "name": "Mess Name",
    "email": "mess@example.com",
    "password": "password",
    "about": "Description",
    "year": "2020",
    "owner": "Owner Name",
    "address": "Full Address",
    "state": "State Name",
    "city": "City Name",
    "area": "Area/Locality",
    "image": "image_url"
  }
  ```
- **Response**: 
  ```json
  {
    "message": "Mess Owner Registered",
    "data": { ...mess_object }
  }
  ```

#### 2. Get Mess Profile
- **Endpoint**: `GET /mess/profile?email=<email>`
- **Description**: Get mess details by email
- **Query Parameters**: `email` (required)
- **Response**: 
  ```json
  {
    "owner": { ...mess_details }
  }
  ```

#### 3. Find All Mess
- **Endpoint**: `GET /mess/find`
- **Description**: Get list of all registered mess services
- **Response**: Array of mess objects

#### 4. Subscribe to Mess
- **Endpoint**: `PATCH /mess/subscribe/:id`
- **Description**: Subscribe a user to a mess
- **URL Parameters**: `id` (mess ID)
- **Request Body**:
  ```json
  {
    "name": "User Name/ID"
  }
  ```
- **Response**: 
  ```json
  {
    "message": "Subscribed",
    "users": 5
  }
  ```

#### 5. Unsubscribe from Mess
- **Endpoint**: `PATCH /mess/unsubscribe/:id`
- **Description**: Unsubscribe a user from a mess
- **URL Parameters**: `id` (mess ID)
- **Request Body**:
  ```json
  {
    "name": "User Name/ID"
  }
  ```
- **Response**: 
  ```json
  {
    "message": "Unsubscribed",
    "users": 4
  }
  ```

---

## 🌐 Frontend Pages

### 1. **index.html** - Home/Landing Page
- Main landing page with mess finder features
- Displays benefits and how it works
- Navigation to authentication pages

### 2. **auth.html** - Authentication Gateway
- Entry point for authentication
- Links to user/mess specific auth pages

### 3. **login.html** - User Login
- User login form
- JWT token generation on success

### 4. **userauth.html** - User Registration
- New user registration form
- Password hashing before storage

### 5. **messauth.html** - Mess Owner Registration
- Mess owner registration with detailed information
- Image upload support

### 6. **findmess.html** - Browse Mess Services
- Display all available mess services
- Subscribe/Unsubscribe functionality
- Filter by location

### 7. **profile.html** - User/Mess Profile
- View profile information
- Edit profile details
- View subscribers (for mess owners)

---

## 🗄️ Database Schema

### User Model
```javascript
{
  name: String,
  email: String (unique),
  password: String (hashed),
  createdAt: Date
}
```

### Mess Model
```javascript
{
  name: String,
  email: String (unique),
  password: String,
  about: String,
  year: String,
  owner: String,
  address: String,
  state: String,
  city: String,
  area: String,
  image: String,
  subscribers: [String],
  users: Number,
  createdAt: Date
}
```

---

## 🏃 Running the Application

### Development Mode
```bash
cd backend
npm run server
```
This uses nodemon for auto-restart on file changes.

### Production Mode
```bash
cd backend
node index.js
```

### Access Points
- **API Server**: http://localhost:8080
- **Frontend**: http://localhost:8080 (served by Express)
- **MongoDB**: mongodb://127.0.0.1:27017/messfinder

---

## 🔒 Security Features

- **Password Hashing**: Uses bcrypt with salt rounds of 10
- **JWT Authentication**: Tokens expire after 2 hours
- **CORS Enabled**: Allows cross-origin requests
- **Input Validation**: Server-side validation for all routes

---

## 🎨 Responsive Design

The frontend is fully responsive with:
- Mobile-first approach
- Flexible grid layouts
- Media queries for different screen sizes
- Touch-friendly UI elements

---

## 📝 Environment Variables (Recommended)

For production, consider using environment variables:

```env
PORT=8080
MONGODB_URI=mongodb://127.0.0.1:27017/messfinder
JWT_SECRET=mysecret
JWT_EXPIRE=2h
```

---

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Commit your changes
4. Push to the branch
5. Open a Pull Request

---

## 📄 License

This project is licensed under the ISC License.

---

## 👥 Authors

- Your Name/Team

---

## 📞 Support

For support, email your-email@example.com or open an issue in the repository.

---

## 🔮 Future Enhancements

- [ ] Add payment integration
- [ ] Implement review and rating system
- [ ] Add meal menu management
- [ ] Email notifications for subscriptions
- [ ] Advanced search filters
- [ ] Real-time chat support
- [ ] Mobile app version
- [ ] Admin dashboard

---

**Happy Coding! 🚀**
