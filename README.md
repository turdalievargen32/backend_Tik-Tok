Certainly! Here's a detailed documentation for your backend Tik-Tok project on GitHub.

---

# Backend Tik-Tok Project Documentation

## Table of Contents

1. [Introduction](#introduction)
2. [Features](#features)
3. [Requirements](#requirements)
4. [Installation](#installation)
5. [Usage](#usage)
6. [API Endpoints](#api-endpoints)
7. [Project Structure](#project-structure)
8. [Database Schema](#database-schema)
9. [Contribution](#contribution)
10. [License](#license)
11. [Contact](#contact)

## Introduction

This project is a backend implementation for a Tik-Tok-like application. It includes functionalities for user management, video upload and streaming, likes and comments, and user follow system.

## Features

- User registration and authentication
- Video upload, retrieval, and streaming
- Like and comment on videos
- Follow and unfollow users
- User feed generation based on follows

## Requirements

- Node.js (version 14 or higher)
- MongoDB
- Git
- Postman or similar tool for API testing

## Installation

1. **Clone the repository:**

   ```bash
   git clone https://github.com/turdalievargen32/backend_Tik-Tok.git
   ```

2. **Navigate to the project directory:**

   ```bash
   cd backend_Tik-Tok
   ```

3. **Install the dependencies:**

   ```bash
   npm install
   ```

4. **Set up environment variables:**

   Create a `.env` file in the root directory and add the following variables:

   ```plaintext
   PORT=5000
   MONGO_URI=your_mongodb_connection_string
   JWT_SECRET=your_jwt_secret
   ```

5. **Start the server:**

   ```bash
   npm start
   ```

## Usage

Use Postman or a similar tool to test the API endpoints. The server should be running on `http://localhost:5000`.

## API Endpoints

### User Routes

- **POST /api/users/register**: Register a new user.
- **POST /api/users/login**: Authenticate a user and get a token.
- **GET /api/users/profile**: Get the profile of the authenticated user.
- **PUT /api/users/profile**: Update the profile of the authenticated user.

### Video Routes

- **POST /api/videos**: Upload a new video.
- **GET /api/videos**: Get all videos.
- **GET /api/videos/:id**: Get a video by ID.
- **DELETE /api/videos/:id**: Delete a video by ID.

### Like Routes

- **POST /api/videos/:id/like**: Like a video.
- **DELETE /api/videos/:id/like**: Unlike a video.

### Comment Routes

- **POST /api/videos/:id/comment**: Add a comment to a video.
- **GET /api/videos/:id/comments**: Get all comments for a video.

### Follow Routes

- **POST /api/users/:id/follow**: Follow a user.
- **DELETE /api/users/:id/follow**: Unfollow a user.

## Project Structure

```
backend_Tik-Tok/
├── controllers/            # Controller functions for each route
│   ├── userController.js
│   ├── videoController.js
│   ├── likeController.js
│   └── commentController.js
├── models/                 # Mongoose models for MongoDB collections
│   ├── User.js
│   ├── Video.js
│   ├── Like.js
│   └── Comment.js
├── routes/                 # Route definitions
│   ├── userRoutes.js
│   ├── videoRoutes.js
│   ├── likeRoutes.js
│   └── commentRoutes.js
├── middleware/             # Custom middleware functions
│   └── authMiddleware.js
├── config/                 # Configuration files
│   └── db.js
├── .env                    # Environment variables
├── server.js               # Entry point of the application
├── package.json            # Project metadata and dependencies
└── README.md               # Project documentation
```

## Database Schema

### User Schema

```javascript
const mongoose = require('mongoose');

const userSchema = mongoose.Schema({
  username: {
    type: String,
    required: true,
    unique: true
  },
  email: {
    type: String,
    required: true,
    unique: true
  },
  password: {
    type: String,
    required: true
  },
  followers: [{
    type: mongoose.Schema.Types.ObjectId,
    ref: 'User'
  }],
  following: [{
    type: mongoose.Schema.Types.ObjectId,
    ref: 'User'
  }],
}, {
  timestamps: true
});

module.exports = mongoose.model('User', userSchema);
```

### Video Schema

```javascript
const mongoose = require('mongoose');

const videoSchema = mongoose.Schema({
  user: {
    type: mongoose.Schema.Types.ObjectId,
    ref: 'User',
    required: true
  },
  videoUrl: {
    type: String,
    required: true
  },
  description: {
    type: String
  },
  likes: [{
    type: mongoose.Schema.Types.ObjectId,
    ref: 'Like'
  }],
  comments: [{
    type: mongoose.Schema.Types.ObjectId,
    ref: 'Comment'
  }],
}, {
  timestamps: true
});

module.exports = mongoose.model('Video', videoSchema);
```

### Like Schema

```javascript
const mongoose = require('mongoose');

const likeSchema = mongoose.Schema({
  user: {
    type: mongoose.Schema.Types.ObjectId,
    ref: 'User',
    required: true
  },
  video: {
    type: mongoose.Schema.Types.ObjectId,
    ref: 'Video',
    required: true
  },
}, {
  timestamps: true
});

module.exports = mongoose.model('Like', likeSchema);
```

### Comment Schema

```javascript
const mongoose = require('mongoose');

const commentSchema = mongoose.Schema({
  user: {
    type: mongoose.Schema.Types.ObjectId,
    ref: 'User',
    required: true
  },
  video: {
    type: mongoose.Schema.Types.ObjectId,
    ref: 'Video',
    required: true
  },
  text: {
    type: String,
    required: true
  },
}, {
  timestamps: true
});

module.exports = mongoose.model('Comment', commentSchema);
```

## Contribution

Contributions are welcome! To contribute to this project, please follow these steps:

1. Fork the repository.
2. Create a new branch: `git checkout -b feature-name`.
3. Make your changes and commit them: `git commit -m 'Add some feature'`.
4. Push to the branch: `git push origin feature-name`.
5. Submit a pull request.

Please ensure your code follows the project's coding standards and includes appropriate tests.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for more information.

