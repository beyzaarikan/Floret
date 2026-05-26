# 🌸 Usermanager

A small social media web application built for the WebP2 course (IT1002, SoSe26) at THM Gießen. Users can register, post messages, comment on posts, and manage their profiles.

## Features

- **Public feed** — view all posts and threaded comments without logging in
- **User search** — search for users by name or username directly in the feed
- **Authentication** — register, login, logout with session handling
- **Posts** — create, edit, and delete your own posts
- **Comments** — comment on posts with nested reply support
- **Profile page** — edit your profile info and bio, view your posts and comments
- **Public profiles** — view any user's profile and posts
- **Password change** — change password with old password verification
- **Relative timestamps** — "vor 2 Minuten", "vor 1 Stunde"
- **Emoji reactions** — react to posts and comments with emojis
- **API documentation** — full ApiDoc available at `/apidoc/`

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Backend | Node.js, Express.js |
| Frontend | Vanilla JS, custom CSS |
| Database | MySQL |
| Session | express-session |
| Auth | bcryptjs |
| Docs | ApiDoc |

## Getting Started

### Prerequisites

- Node.js >= 18
- MySQL

### Installation

```bash
# Clone the repository
git clone <repo-url>
cd usermanager

# Install dependencies
npm install

# Import the database
mysql -u root usermanager < db/usermanager.sql

# Start the server
node server.js
```

The app runs at `http://localhost:3000`.

### Generate API Documentation

```bash
npm run apidoc
```

Docs will be available at `http://localhost:3000/apidoc/`.

## Project Structure

```
usermanager/
├── server.js
├── db/
│   ├── connection.js
│   └── usermanager.sql
├── routes/
│   ├── users.js
│   ├── posts.js
│   └── comments.js
├── models/
│   ├── userModel.js
│   ├── postModel.js
│   └── commentModel.js
└── public/
    ├── index.html
    ├── profile.html
    ├── user.html
    ├── css/
    │   └── style.css
    └── js/
        ├── main.js
        ├── profile.js
        └── user.js
```

## API Overview

| Method | Endpoint | Description | Auth |
|--------|----------|-------------|------|
| GET | `/api/users` | Get all users | No |
| POST | `/api/users` | Register | No |
| POST | `/api/users/login` | Login | No |
| POST | `/api/users/logout` | Logout | Yes |
| GET | `/api/users/me` | Current session user | Yes |
| GET | `/api/users/:id` | Get user by ID | No |
| PUT | `/api/users/:id` | Update user | Owner |
| PUT | `/api/users/:id/password` | Change password | Owner |
| DELETE | `/api/users/:id` | Delete user | Owner |
| GET | `/api/posts` | Get all posts | No |
| GET | `/api/posts/:id` | Get post by ID | No |
| POST | `/api/posts` | Create post | Yes |
| PUT | `/api/posts/:id` | Update post | Owner |
| DELETE | `/api/posts/:id` | Delete post | Owner |
| GET | `/api/comments?postId=` | Get comments by post | No |
| GET | `/api/comments/:id` | Get comment by ID | No |
| POST | `/api/comments` | Create comment | Yes |
| PUT | `/api/comments/:id` | Update comment | Owner |
| DELETE | `/api/comments/:id` | Delete comment | Owner |

## Database Schema

```sql
User      (userId, firstname, lastname, username, email, password, bio)
Post      (postId, text, creationDate, creator → User)
Comment   (commentId, text, origin → Post, creator → User, parentId → Comment)
```

All foreign keys use `ON DELETE CASCADE`.
