# Twitter / X Clone - Full Stack

A full stack Twitter/X clone built with React, Redux Toolkit, Node.js, Express, and MongoDB.

## Features

- Register and login with JWT authentication
- Post and delete tweets
- Like and dislike tweets (toggle)
- Follow and unfollow users
- Bookmark tweets
- View user profiles
- For You feed (your tweets + following users tweets)
- Following-only feed
- Who to follow suggestions
- Persistent login with Redux Persist
- Toast notifications for all actions

## Tech Stack

### Frontend

| Package | Version | Purpose |
|---------|---------|---------|
| react | ^18.2.0 | UI framework |
| react-router-dom | ^6.22.2 | Client-side routing |
| @reduxjs/toolkit | ^2.2.1 | State management |
| react-redux | ^9.1.0 | React-Redux binding |
| redux-persist | ^6.0.0 | Persist Redux state on refresh |
| axios | ^1.6.7 | HTTP requests |
| react-hot-toast | ^2.4.1 | Toast notifications |
| react-avatar | ^5.0.3 | User avatars |
| react-icons | ^5.0.1 | Icons |
| tailwindcss | ^3.4.1 | Styling |

### Backend

| Package | Version | Purpose |
|---------|---------|---------|
| express | ^4.18.3 | Web framework |
| mongoose | ^8.2.0 | MongoDB ODM |
| bcryptjs | ^2.4.3 | Password hashing |
| jsonwebtoken | ^9.0.2 | JWT tokens |
| cookie-parser | ^1.4.6 | Read cookies |
| cors | ^2.8.5 | Cross-origin requests |
| dotenv | ^16.4.5 | Environment variables |
| nodemon | ^3.1.0 | Auto-restart in development |

## Project Structure

```
twitter-clone/
│
├── backend/
│   ├── index.js
│   ├── package.json
│   ├── .env
│   ├── config/
│   │   └── database.js
│   ├── middleware/
│   │   └── auth.js
│   ├── models/
│   │   ├── userSchema.js
│   │   └── tweetSchema.js
│   ├── controllers/
│   │   ├── userController.js
│   │   └── tweetController.js
│   └── routes/
│       ├── userRoute.js
│       └── tweetRoute.js
│
└── frontend/
    ├── public/
    ├── package.json
    ├── tailwind.config.js
    └── src/
        ├── App.js
        ├── index.js
        ├── index.css
        ├── components/
        │   ├── Body.js
        │   ├── Home.js
        │   ├── Login.js
        │   ├── Feed.js
        │   ├── Tweet.js
        │   ├── LeftSidebar.js
        │   ├── RightSidebar.js
        │   └── Profile.js
        ├── hooks/
        │   ├── useGetMyTweets.js
        │   ├── useGetProfile.js
        │   └── useOtherUsers.js
        └── redux/
            ├── store.js
            ├── userSlice.js
            └── tweetSlice.js
```

## Getting Started

### Prerequisites

- Node.js v18+
- MongoDB local or MongoDB Atlas account

### 1. Clone the repository

```bash
git clone https://github.com/your-username/twitter-clone.git
cd twitter-clone
```

### 2. Setup Backend

```bash
cd backend
npm install
```

Create a `.env` file inside the `backend/` folder:

```
PORT=8000
MONGO_URI=mongodb://localhost:27017/twitter
TOKEN_SECRET=your_secret_key_here
```

Start the backend:

```bash
npm run dev
```

Backend runs at `http://localhost:8000`

### 3. Setup Frontend

```bash
cd frontend
npm install
npm start
```

Frontend runs at `http://localhost:3000`

## Pages

**`/login`**
- Toggle between Login and Signup form
- On login JWT cookie is set, user saved to Redux, redirected to Home

**`/` Home**
- For You tab shows your tweets plus following users tweets
- Following tab shows only tweets from people you follow
- Create and post new tweets
- Like or dislike tweets
- Delete your own tweets

**`/profile/:id`**
- View any user profile
- Follow or unfollow button
- Shows Edit Profile on your own profile

## API Endpoints

### User Routes `/api/v1/user`

| Method | Endpoint | Description | Auth |
|--------|----------|-------------|------|
| POST | `/register` | Register new user | No |
| POST | `/login` | Login and set JWT cookie | No |
| GET | `/logout` | Clear JWT cookie | No |
| GET | `/profile/:id` | Get user profile | Yes |
| GET | `/otherUsers/:id` | Get all users except self | Yes |
| POST | `/follow/:id` | Follow a user | Yes |
| POST | `/unfollow/:id` | Unfollow a user | Yes |
| PUT | `/bookmark/:id` | Toggle tweet bookmark | Yes |

### Tweet Routes `/api/v1/tweet`

| Method | Endpoint | Description | Auth |
|--------|----------|-------------|------|
| POST | `/create` | Create a new tweet | Yes |
| DELETE | `/delete/:id` | Delete a tweet | Yes |
| PUT | `/like/:id` | Like or dislike toggle | Yes |
| GET | `/allTweets/:id` | My tweets plus following tweets | Yes |
| GET | `/followingTweets/:id` | Only following users tweets | Yes |

## Authentication

- On login the backend creates a JWT token set as an HTTP-only cookie expiring in 1 day
- Frontend sends `withCredentials: true` with every Axios request so the cookie is sent automatically
- `isAuthenticated` middleware verifies the cookie on all protected routes
- On logout the cookie is cleared and Redux state is reset

## Environment Variables

| Variable | Description |
|----------|-------------|
| `PORT` | Backend server port |
| `MONGO_URI` | MongoDB connection string |
| `TOKEN_SECRET` | Secret key for signing JWT |

## Scripts

**Backend**

```bash
npm run dev      # Start with nodemon
node index.js    # Start without nodemon
```

**Frontend**

```bash
npm start        # Start development server
npm run build    # Build for production
```

## Deployment

**Backend** — Deploy on Render or Railway

- Add `PORT`, `MONGO_URI`, `TOKEN_SECRET` as environment variables
- Use MongoDB Atlas for the database

**Frontend** — Deploy on Vercel or Netlify

- Update `USER_API_END_POINT` and `TWEET_API_END_POINT` in `utils/constant.js` to your live backend URL
- Update CORS origin in backend `index.js` to your live frontend URL

## License

MIT

