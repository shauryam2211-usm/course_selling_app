# Course Selling Backend API

A backend API for a course-selling platform built with **Node.js, Express, MongoDB, Mongoose, JWT Authentication, and dotenv**. The project supports two roles:

- **Users**: Sign up, log in, view courses, and purchase courses.
- **Admins**: Sign up, log in, create courses, delete courses, and add course content.

---

## Features

### User Features
- User Signup
- User Login
- View all available courses
- Purchase a course
- View purchased courses

### Admin Features
- Admin Signup
- Admin Login
- Create a new course
- Delete a course
- Add course content

---

## Tech Stack

- Node.js
- Express.js
- MongoDB Atlas
- Mongoose
- JSON Web Tokens (JWT)
- dotenv
- bcrypt (for password hashing)

---

## Project Setup

### 1. Clone the Repository

```bash
git clone <repository-url>
cd course-selling-backend
```

---

### 2. Initialize Node Project

```bash
npm init -y
```

---

### 3. Install Dependencies

```bash
npm install express mongoose jsonwebtoken dotenv bcrypt
```

---

### 4. Install Development Dependency

```bash
npm install --save-dev nodemon
```

---

## Project Structure

```
course-selling-backend/
│
├── index.js
│
├── config/
│   └── db.js
│
├── models/
│   ├── User.js
│   ├── Admin.js
│   ├── Course.js
│   └── Purchase.js
│
├── middleware/
│   ├── userAuth.js
│   └── adminAuth.js
│
├── routes/
│   ├── userRoutes.js
│   └── adminRoutes.js
│
├── .env
├── package.json
└── README.md
```

---

## Environment Variables

Create a `.env` file in the root directory:

```env
PORT=3000

MONGO_URL=mongodb+srv://username:password@cluster.mongodb.net/courseselling

JWT_USER_SECRET=your_user_secret

JWT_ADMIN_SECRET=your_admin_secret
```

---

## Database Connection

The project uses Mongoose to connect to MongoDB.

Example:

```javascript
mongoose.connect(process.env.MONGO_URL)
.then(() => {
    console.log("Database Connected");
})
.catch((err) => {
    console.log(err);
});
```

---

# Database Schemas

## User Schema

Stores user information.

Fields:

- name
- email (unique)
- password

---

## Admin Schema

Stores admin information.

Fields:

- name
- email (unique)
- password

---

## Course Schema

Stores course details.

Fields:

- title
- description
- price
- imageUrl
- content
- createdBy (Admin reference)

---

## Purchase Schema

Stores information about purchased courses.

Fields:

- userId (User reference)
- courseId (Course reference)
- purchasedAt

---

# API Routes

## User Routes

Base URL:

```
/api/user
```

### Signup

```
POST /signup
```

Request:

```json
{
    "name": "John",
    "email": "john@gmail.com",
    "password": "123456"
}
```

---

### Login

```
POST /login
```

Returns a JWT token.

---

### Get All Courses

```
GET /courses
```

Returns all available courses.

---

### Purchase Course

```
POST /purchase/:courseId
```

Protected route.

Requires:

```
Authorization: Bearer <user-token>
```

---

### Get Purchased Courses

```
GET /purchases
```

Protected route.

Returns all courses purchased by the logged-in user.

---

# Admin Routes

Base URL:

```
/api/admin
```

## Signup

```
POST /signup
```

Creates a new admin account.

---

## Login

```
POST /login
```

Returns an admin JWT token.

---

## Create Course

```
POST /course
```

Protected route.

Requires admin JWT.

---

## Delete Course

```
DELETE /course/:id
```

Protected route.

Only admins can delete courses.

---

## Add Course Content

```
PUT /course/:id/content
```

Protected route.

Allows an admin to update course content.

---

# Authentication

Authentication is handled using JWT.

Two middlewares are used:

## User Authentication

- Checks user JWT token.
- Verifies token using `JWT_USER_SECRET`.
- Adds user information to `req.user`.

---

## Admin Authentication

- Checks admin JWT token.
- Verifies token using `JWT_ADMIN_SECRET`.
- Adds admin information to `req.admin`.

---

# Running the Application

## Development Mode

```bash
npm run dev
```

Using nodemon.

---

## Production Mode

```bash
npm start
```

---

## Scripts in package.json

```json
{
  "scripts": {
    "start": "node index.js",
    "dev": "nodemon index.js"
  }
}
```

---

## Security Practices

- Passwords should be hashed using bcrypt.
- JWT secrets should never be exposed publicly.
- Database connection string should be stored in `.env`.
- Sensitive files should be added to `.gitignore`.

---

## Future Improvements

- Course categories and tags.
- Payment gateway integration.
- User profile management.
- Course progress tracking.
- Reviews and ratings.
- Admin dashboard.

---

## Author

Course Selling Backend API built using Node.js, Express, MongoDB, and JWT Authentication.