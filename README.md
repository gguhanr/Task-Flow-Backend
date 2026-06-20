# TaskFlow — Task Manager

Full-stack task manager: HTML/CSS/JS frontend + Node.js/Express backend + MongoDB.

## Folder structure  
```  
back-end/
├── .env
├── server.js
├── package.json
├── models/Task.js
├── routes/tasks.js
└── public/index.html
```

## Setup (Windows)

1. Open this folder in terminal (the one containing `server.js`).
2. Install dependencies:
   ```
   npm install
   ```
3. Confirm `.env` exists in this same folder and contains your MongoDB Atlas URI.
4. Start the server:
   ```
   node server.js
   ```
5. You should see:
   ```
   ✅ .env loaded
   ✅ Connected to MongoDB Atlas
   🚀 Server running at http://localhost:5000
   ```
6. Open `http://localhost:5000` in your browser.

## What changed in this version

- Frontend rewritten with `addEventListener` instead of inline `onclick="..."` attributes — this avoids the
  `"next is not a function"` error caused by browser extensions (Grammarly, password managers, etc.) intercepting
  global function names referenced directly in HTML.
- All API calls use `window.location.origin` so the frontend always talks to whichever host/port is actually serving it.
- `/api/tasks/meta/stats` route is declared before `/api/tasks/:id` so it's never swallowed by the ID route.
- Save button shows "Saving…" and disables itself during the request, so duplicate clicks can't fire two requests.
- Server loads `.env` manually with Node's `fs` module (no dependency on `dotenv`/`dotenvx`), with a safe hardcoded
  fallback URI if `.env` is missing.

## Troubleshooting

| Symptom | Fix |
|---|---|
| `ECONNREFUSED 127.0.0.1:27017` | `.env` not loaded / wrong URI — check `MONGO_URI` in `.env` |
| `Could not connect to any servers...IP whitelist` | Atlas → Network Access → Add IP → Allow Access From Anywhere (`0.0.0.0/0`) |
| Page loads but tasks don't save | Open browser DevTools (F12) → Console tab, try again, read the exact error there |
| `.env` shows "not found" | Make sure the file is literally named `.env` (not `.env.txt`) and sits next to `server.js` |
## DEMO LINK :
https://task-flow-backend-kyq8.onrender.com/
