Video Progress Tracking Application
This project is a full-stack application designed to track user progress in educational videos. It features user authentication, video Browse, and granular progress tracking, allowing users to resume videos exactly where they left off.

Table of Contents
Features

Technologies Used

Project Structure

Getting Started

Prerequisites

Backend Setup

Frontend Setup

Usage

API Endpoints

Contributing

License

Features
User Authentication: Register, log in, and manage user sessions securely using JWT (JSON Web Tokens).

Video Listing: Browse a collection of available videos.

Video Playback: Play videos directly within the application using react-player.

Progress Tracking: Automatically tracks watched intervals, total watched time, and calculates progress percentage for each video.

Resume Playback: Users can resume videos from their last watched position.

Dashboard: A personalized dashboard showing videos in progress and overall video history.

Responsive Design: Optimized for various screen sizes.

Technologies Used
Backend
Node.js: JavaScript runtime environment.

Express.js: Web application framework for Node.js.

MongoDB: NoSQL database for storing video and user data.

Mongoose: ODM (Object Data Modeling) library for MongoDB and Node.js.

bcryptjs: For password hashing.

jsonwebtoken: For implementing JWT-based authentication.

dotenv: For loading environment variables.

uuid: For generating UUIDs for primary keys.

Frontend
React.js: JavaScript library for building user interfaces.

React Router DOM: For declarative routing in React applications.

Axios: Promise-based HTTP client for making API requests.

react-player: React component for playing various URLs, including YouTube.

React Context API: For state management (Authentication and Video data).

Custom Hooks: For encapsulating reusable logic (e.g., useVideoProgress).

CSS: Modular and global styling.

Project Structure
The project is divided into two main parts: backend and frontend.

.
├── backend/
│   ├── config/
│   │   └── database.js
│   ├── controllers/
│   │   ├── authController.js
│   │   ├── progressController.js
│   │   └── videoController.js
│   ├── middleware/
│   │   └── auth.js
│   ├── models/
│   │   ├── User.js
│   │   ├── Video.js
│   │   └── VideoProgress.js
│   ├── routes/
│   │   ├── auth.js
│   │   ├── progress.js
│   │   ├── users.js
│   │   └── videos.js
│   ├── utils/
│   │   └── progressUtils.js
│   ├── seed.js             # For seeding demo data
│   ├── server.js
│   └── .env
│   └── package.json
│
└── frontend/
    ├── public/
    │   └── index.html
    ├── src/
    │   ├── components/
    │   │   ├── layout/
    │   │   │   ├── Footer.js
    │   │   │   ├── Header.js
    │   │   │   └── Layout.js
    │   │   ├── routing/
    │   │   │   └── PrivateRoute.js
    │   │   └── video/
    │   │       ├── ProgressBar.js
    │   │       ├── VideoCard.js
    │   │       └── VideoPlayerComponent.js
    │   ├── contexts/
    │   │   ├── AuthContext.js
    │   │   └── VideoContext.js
    │   ├── hooks/
    │   │   └── useVideoProgress.js
    │   ├── pages/
    │   │   ├── Dashboard.js
    │   │   ├── Home.js
    │   │   ├── Login.js
    │   │   ├── NotFound.js
    │   │   ├── Register.js
    │   │   └── VideoPlayer.js
    │   ├── services/
    │   │   ├── api.js
    │   │   ├── authService.js
    │   │   ├── progressService.js
    │   │   └── videoService.js
    │   ├── styles/
    │   │   ├── App.css
    │   │   └── global.css
    │   ├── utils/
    │   │   └── progressUtils.js
    │   ├── App.js
    │   ├── index.js
    │   └── reportWebVitals.js
    ├── .env
    ├── package.json
    └── setupProxy.js
Getting Started
Follow these instructions to set up and run the project on your local machine.

Prerequisites
Node.js and npm: Make sure you have Node.js (v14 or higher recommended) and npm installed. You can download it from nodejs.org.

MongoDB:

Local Installation: Install MongoDB Community Server. Follow the instructions on the MongoDB website.

MongoDB Atlas (Cloud): Alternatively, set up a free tier cluster on MongoDB Atlas.

Backend Setup
Clone the repository (or create project directories and move files):
If you haven't already, organize your backend files into a backend/ directory.

Navigate to the backend directory:

Bash

cd backend
Install dependencies:

Bash

npm install
Create a .env file:
In the backend/ directory, create a file named .env and add the following environment variables. Replace the placeholders with your actual MongoDB connection URI and a strong JWT secret.

Code snippet

PORT=5000
MONGO_URI="mongodb://localhost:27017/your_database_name" # For local MongoDB
# OR
# MONGO_URI="mongodb+srv://<username>:<password>@cluster0.abcde.mongodb.net/your_database_name?retryWrites=true&w=majority" # For MongoDB Atlas
JWT_SECRET="your_very_strong_secret_key_here"
JWT_EXPIRE="1d" # e.g., 1h, 2d, 30m
Make sure to replace <username>, <password>, and your_database_name if using MongoDB Atlas.

Seed the database (Optional, but recommended for demo videos):
This project includes a seed.js script to populate your database with demo video data.
To destroy any existing data and import fresh data:

Bash

npm run seed:destroy
npm run seed
Start the backend server:

Bash

npm start
# Or, for development with live reload (if you have nodemon installed):
# npm run dev
You should see messages like "MongoDB connection has been established successfully." and "Server running on port 5000."

Frontend Setup
Navigate to the frontend directory:

Bash

cd frontend
Install dependencies:

Bash

npm install
Ensure react, react-dom are at 18.3.1 and react-player is at 2.11.0 in your package.json for best compatibility.

Create a .env file:
In the frontend/ directory, create a file named .env and add the following environment variable to point to your backend API:

Code snippet

REACT_APP_API_URL=http://localhost:5000/api
Start the frontend development server:

Bash

npm start
This will typically open your application in your browser at http://localhost:3000.

Usage
Home Page (/): View a list of available videos.

Register (/register): Create a new user account.

Login (/login): Log in to your account.

Dashboard (/dashboard): (Protected Route) See your video progress and continue watching videos.

Video Player (/video/:id): Click on any video from the home page or dashboard to play it and track your progress.

API Endpoints
The backend provides the following RESTful API endpoints:

Authentication
POST /api/auth/register - Register a new user.

POST /api/auth/login - Log in a user and get a JWT.

GET /api/auth/me - Get current authenticated user's details (Protected).

Videos
GET /api/videos - Get all published videos.

GET /api/videos/:id - Get a single video by ID.

POST /api/videos - Create a new video (Protected, Admin only logic).

PUT /api/videos/:id - Update a video (Protected, Admin only logic).

DELETE /api/videos/:id - Delete a video (Protected, Admin only logic).

Progress
GET /api/progress - Get user's progress for all videos (Protected).

GET /api/progress/:videoId - Get user's progress for a specific video (Protected).

POST /api/progress/:videoId - Update user's progress for a video (Protected).

DELETE /api/progress/:videoId - Reset user's progress for a video (Protected).

Contributing
Feel free to fork the repository, open issues, or submit pull requests to improve the project.

