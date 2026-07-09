# Task Ledger

A minimal full-stack task manager: an Express REST API backend with an in-memory data store, and a retro terminal-styled React frontend.

![Node](https://img.shields.io/badge/node-%3E%3D18-green)
![Express](https://img.shields.io/badge/express-4.x-black)
![React](https://img.shields.io/badge/react-18-blue)

## Features

- Create, read, update, and delete tasks via a REST API
- Toggle tasks as done / not done with optimistic UI updates
- Terminal / console-inspired UI (built with React + custom CSS)
- Graceful error handling with rollback on failed requests
- No database required — data is stored in memory (resets on server restart)

## Tech Stack

**Backend**
- [Express](https://expressjs.com/) — REST API server
- [cors](https://www.npmjs.com/package/cors) — cross-origin requests from the frontend
- In-memory array as the data store

**Frontend**
- [React](https://react.dev/) (hooks: `useState`, `useEffect`, `useCallback`)
- Vite (or Create React App — adjust based on your setup)
- Plain CSS with custom properties for theming

## Project Structure

```
.
├── server/
│   └── index.js        # Express API
└── client/
    ├── src/
    │   ├── App.jsx      # Main React component
    │   └── App.css      # Console/terminal-themed styles
    └── ...
```

> Adjust this tree to match your actual folder layout.

## Getting Started

### Prerequisites

- [Node.js](https://nodejs.org/) v18 or higher
- npm (comes with Node.js)

### 1. Clone the repository

```bash
git clone https://github.com/<your-username>/<your-repo>.git
cd <your-repo>
```

### 2. Start the backend

```bash
cd server
npm install
npm start
```

The API will run at `http://localhost:3000`.

### 3. Start the frontend

In a separate terminal:

```bash
cd client
npm install
npm run dev
```

The React app will open at `http://localhost:5173` (Vite default) or `http://localhost:3000` if using Create React App — check your terminal output for the exact URL.

> **Note:** The frontend expects the API at `http://localhost:3000` (see `API_BASE` in `App.jsx`). Update this constant if your backend runs on a different port.

## API Reference

Base URL: `http://localhost:3000`

| Method | Endpoint      | Description              | Body                          |
|--------|---------------|---------------------------|--------------------------------|
| GET    | `/tasks`      | Get all tasks             | —                              |
| GET    | `/tasks/:id`  | Get a single task by ID   | —                              |
| POST   | `/tasks`      | Create a new task         | `{ "title": "string" }`       |
| PUT    | `/tasks/:id`  | Update a task's title/done| `{ "title"?: string, "done"?: boolean }` |
| DELETE | `/tasks/:id`  | Delete a task              | —                              |

### Example task object

```json
{
  "id": 1,
  "title": "Learn Express",
  "done": false
}
```

### Example requests

**Create a task**
```bash
curl -X POST http://localhost:3000/tasks \
  -H "Content-Type: application/json" \
  -d '{"title": "Write README"}'
```

**Mark a task done**
```bash
curl -X PUT http://localhost:3000/tasks/1 \
  -H "Content-Type: application/json" \
  -d '{"done": true}'
```

**Delete a task**
```bash
curl -X DELETE http://localhost:3000/tasks/1
```

## Notes & Limitations

- Data is stored **in memory only** — restarting the server resets tasks back to the two seed items (`Learn Express`, `Build a REST API`).
- No authentication or persistence layer (e.g. a database) is included; this is intended as a learning/demo project.
- CORS is fully open (`app.use(cors())`) — restrict this in a production setting.

## Possible Next Steps

- Add a persistent database (SQLite, MongoDB, PostgreSQL, etc.)
- Add authentication
- Add task editing (not just toggling `done`)
- Add tests (e.g. Jest + Supertest for the API)
- Deploy backend and frontend separately (e.g. Render/Fly.io + Vercel/Netlify)

## License

[MIT](LICENSE) — feel free to use this project as a starting point for your own work.
