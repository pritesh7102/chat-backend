# Backend — fullstack-chat-app

This README explains how to run the backend locally for development.

## Prerequisites

- Node.js (v16+ recommended)
- npm (comes with Node)
- MongoDB instance (local or cloud like MongoDB Atlas)
- (Optional) Cloudinary account if you want profile picture uploads

## Quick start

1. Clone the repository and change into the backend directory:

```powershell
cd path\to\fullstack-chat-app\backend
```

2. Install dependencies:

```powershell
npm install
```

3. Create a `.env` file in the `backend` folder with the following variables (example):

```
PORT=5000
MONGO_URI=mongodb://localhost:27017/chat-app
JWT_SECRET=your_jwt_secret
NODE_ENV=development
CLOUDINARY_CLOUD_NAME=your_cloud_name
CLOUDINARY_API_KEY=your_api_key
CLOUDINARY_API_SECRET=your_api_secret
```

Only `PORT`, `MONGO_URI`, and `JWT_SECRET` are required for basic auth/message flows. Cloudinary variables are required only if you use profile picture uploads.

4. Run in development mode (auto-restarts on change):

```powershell
npm run dev
```

5. Or run production-like mode:

```powershell
npm start
```

The server entrypoint is `src/index.js`. By default it listens on the port from `process.env.PORT`.

## Endpoints overview

- Auth routes: `POST /api/auth/signup`, `POST /api/auth/login`, `POST /api/auth/forgot-password-email`, `POST /api/auth/change-password` (see controllers for full list).
- Messages: `GET/POST /api/messages` and related socket events (Socket.IO connected on the same server).

## Notes

- Socket.IO is attached to the same HTTP server; the backend serves both HTTP and websocket connections on the same port.
- The current password-reset controller accepts an email and password. For production, implement a token-based reset flow (email a one-time token/link).
- If you use MongoDB Atlas, make sure your `MONGO_URI` includes the correct username/password and allows connections from your IP or use 0.0.0.0/0 during testing.

## Troubleshooting

- If the server does not start, check the log printed in the console. Common issues:
  - Missing `.env` or wrong `MONGO_URI` → connection errors.
  - Port already in use → change `PORT`.

## License

This project uses ISC license (see `package.json`).
