# ⚡ DevFlow – Task Manager

A full-stack project management tool for developer teams. Features a real-time Kanban board, sprint planning, task management, team collaboration, and GitHub integration.

![DevFlow](https://img.shields.io/badge/DevFlow-v1.0.0-6366f1?style=flat-square)
![React](https://img.shields.io/badge/React-18-61dafb?style=flat-square&logo=react)
![Node.js](https://img.shields.io/badge/Node.js-Express-339933?style=flat-square&logo=node.js)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-Prisma-4169e1?style=flat-square&logo=postgresql)
![Socket.io](https://img.shields.io/badge/Socket.io-Realtime-010101?style=flat-square&logo=socket.io)

---

## ✨ Features

| Feature | Description |
|---|---|
| 🔐 **Authentication** | Register, login, JWT tokens, bcrypt password hashing |
| 📋 **Project Management** | Create projects, invite team members, project dashboard |
| 🗂️ **Kanban Board** | Drag-and-drop across columns (Todo, In Progress, Review, Done) |
| ✅ **Task Management** | Create/edit/delete tasks, assign users, set priority & due dates |
| 🚀 **Sprint Planning** | Create sprints, assign tasks, track progress |
| ⚡ **Real-time** | WebSocket updates — all users see board changes instantly |
| 🔔 **Notifications** | Real-time in-app notifications for assignments, mentions, etc |
| 🐙 **GitHub Integration** | Connect repos, link commits to tasks, auto-close with commit messages |

---

## 🏗️ Tech Stack

```
client/          → React 18 + Vite + Tailwind CSS
├─ DnD Kit       → Drag and drop Kanban board
├─ Socket.io     → Real-time WebSocket client
├─ Axios         → HTTP client
└─ React Router  → Client-side routing

server/          → Node.js + Express
├─ Prisma ORM    → Database queries and migrations
├─ PostgreSQL    → Primary database
├─ Socket.io     → Real-time WebSocket server
├─ JWT + bcrypt  → Authentication
└─ MVC Pattern   → Controllers, Routes, Middleware
```

---

## 📁 Project Structure

```
devflow/
├── package.json              ← Root scripts (run both services)
│
├── client/                   ← React Frontend (Vite)
│   ├── src/
│   │   ├── components/
│   │   │   ├── auth/         ← (future: OAuth components)
│   │   │   ├── board/
│   │   │   │   ├── KanbanColumn.jsx
│   │   │   │   └── TaskCard.jsx
│   │   │   ├── tasks/
│   │   │   │   ├── TaskModal.jsx
│   │   │   │   └── CreateTaskModal.jsx
│   │   │   ├── layout/
│   │   │   │   ├── AppLayout.jsx
│   │   │   │   ├── Sidebar.jsx
│   │   │   │   └── TopBar.jsx
│   │   │   └── common/
│   │   │       ├── Modal.jsx
│   │   │       ├── CreateProjectModal.jsx
│   │   │       └── NotificationPanel.jsx
│   │   ├── context/
│   │   │   ├── AuthContext.jsx
│   │   │   └── NotificationContext.jsx
│   │   ├── pages/
│   │   │   ├── LoginPage.jsx
│   │   │   ├── RegisterPage.jsx
│   │   │   ├── DashboardPage.jsx
│   │   │   ├── ProjectPage.jsx
│   │   │   ├── BoardPage.jsx
│   │   │   ├── SprintsPage.jsx
│   │   │   └── SettingsPage.jsx
│   │   ├── services/
│   │   │   ├── api.js         ← Axios API client
│   │   │   └── socket.js      ← Socket.io client
│   │   └── App.jsx
│
└── server/                   ← Node.js Backend (Express)
    ├── prisma/
    │   └── schema.prisma     ← Database models
    └── src/
        ├── index.js          ← App entry point
        ├── config/
        │   └── database.js   ← Prisma client
        ├── controllers/
        │   ├── auth.controller.js
        │   ├── project.controller.js
        │   ├── task.controller.js
        │   ├── sprint.controller.js
        │   ├── column.controller.js
        │   ├── user.controller.js
        │   ├── notification.controller.js
        │   └── github.controller.js
        ├── middleware/
        │   ├── auth.js        ← JWT middleware
        │   └── errorHandler.js
        ├── routes/
        │   ├── index.js
        │   ├── auth.routes.js
        │   ├── project.routes.js
        │   ├── task.routes.js
        │   ├── sprint.routes.js
        │   ├── column.routes.js
        │   ├── user.routes.js
        │   ├── notification.routes.js
        │   └── github.routes.js
        ├── sockets/
        │   └── index.js       ← Socket.io setup
        └── utils/
            └── seed.js        ← Database seed
```

---

## 🚀 Quick Start

### Prerequisites

- Node.js 18+
- PostgreSQL 14+ running locally
- npm or yarn

---

### Step 1 – Clone and Install

```bash
git clone <your-repo-url> devflow
cd devflow
npm run install:all
```

### Step 2 – Configure Environment

```bash
cd server
cp .env.example .env
```

Edit `server/.env`:

```env
PORT=5000
DATABASE_URL="postgresql://postgres:YOUR_PASSWORD@localhost:5432/devflow?schema=public"
JWT_SECRET=change_this_to_a_secure_random_string_at_least_32_chars
JWT_EXPIRES_IN=7d
CLIENT_URL=http://localhost:5173
```

### Step 3 – Create the Database

```bash
# Create database in PostgreSQL
psql -U postgres -c "CREATE DATABASE devflow;"
```

### Step 4 – Run Migrations

```bash
npm run db:generate
npm run db:migrate
# When prompted, name the migration: "initial"
```

### Step 5 – Seed Demo Data (Optional)

```bash
npm run db:seed
```

This creates two demo accounts:
- `alice@devflow.dev` / `password123`
- `bob@devflow.dev` / `password123`

### Step 6 – Start Development Servers

```bash
# From the root directory — starts both client and server
npm run dev
```

| Service | URL |
|---|---|
| 🌐 Frontend | http://localhost:5173 |
| 🔧 Backend API | http://localhost:5000 |
| 🗄️ Prisma Studio | `npm run db:studio` → http://localhost:5555 |

---

## 🔌 API Reference

### Authentication
| Method | Path | Description |
|---|---|---|
| POST | `/api/auth/register` | Register a new user |
| POST | `/api/auth/login` | Login and get JWT |
| GET | `/api/auth/me` | Get current user |
| POST | `/api/auth/logout` | Logout |

### Projects
| Method | Path | Description |
|---|---|---|
| GET | `/api/projects` | List user's projects |
| POST | `/api/projects` | Create project |
| GET | `/api/projects/:id` | Get project |
| PUT | `/api/projects/:id` | Update project |
| DELETE | `/api/projects/:id` | Delete project |
| POST | `/api/projects/:id/invite` | Invite member |
| GET | `/api/projects/:id/members` | Get members |
| GET | `/api/projects/:id/dashboard` | Dashboard stats |

### Tasks
| Method | Path | Description |
|---|---|---|
| GET | `/api/projects/:id/tasks` | List tasks (filter: columnId, sprintId) |
| POST | `/api/projects/:id/tasks` | Create task |
| GET | `/api/projects/:id/tasks/:taskId` | Get task with comments |
| PUT | `/api/projects/:id/tasks/:taskId` | Update task |
| DELETE | `/api/projects/:id/tasks/:taskId` | Delete task |
| PATCH | `/api/projects/:id/tasks/:taskId/move` | Move task to column |
| POST | `/api/projects/:id/tasks/:taskId/comments` | Add comment |

### Sprints
| Method | Path | Description |
|---|---|---|
| GET | `/api/projects/:id/sprints` | List sprints with progress |
| POST | `/api/projects/:id/sprints` | Create sprint |
| PATCH | `/api/projects/:id/sprints/:sid/start` | Start sprint |
| PATCH | `/api/projects/:id/sprints/:sid/complete` | Complete sprint |
| POST | `/api/projects/:id/sprints/:sid/tasks` | Assign tasks |

---

## ⚡ WebSocket Events

### Client → Server
| Event | Payload | Description |
|---|---|---|
| `join:project` | `projectId` | Subscribe to project updates |
| `leave:project` | `projectId` | Unsubscribe |
| `task:move` | `{ projectId, taskId, columnId }` | Broadcast local drag |

### Server → Client
| Event | Description |
|---|---|
| `task:created` | New task added |
| `task:updated` | Task edited |
| `task:deleted` | Task removed |
| `task:moved` | Task dragged to new column |
| `comment:added` | New comment on a task |
| `sprint:started` | Sprint activated |
| `sprint:completed` | Sprint closed |
| `member:joined` | New team member added |
| `commit:linked` | GitHub commit associated |

---

## 🐙 GitHub Integration

1. Connect a repository from the Project page
2. Add a webhook in your GitHub repo settings:
   - URL: `https://your-domain.com/api/github/webhook`
   - Events: **Push**
3. Use special commit message keywords to link/close tasks:
   ```
   git commit -m "fixes #TASK_ID: implement login page"
   git commit -m "refs #TASK_ID: working on this"
   git commit -m "closes #TASK_ID: done!"
   ```

---

## 🗄️ Database Schema

```
User ────┬──── ProjectMember ──── Project ──── Column ──── Task
         │                              └────── Sprint ────┘
         ├──── Task (assignee)
         ├──── Task (creator)
         ├──── Comment
         └──── Notification

Task ────┬──── Comment
         ├──── Label (many-to-many)
         └──── GitCommit
```

---

## 🧑‍💻 Development Tips

```bash
# View database in browser GUI
npm run db:studio

# Reset database and re-seed
cd server && npx prisma migrate reset && npm run db:seed

# Generate Prisma client after schema changes
npm run db:generate

# Run migrations after schema changes
npm run db:migrate
```

---

## 📦 Environment Variables

```env
# server/.env
PORT=5000
NODE_ENV=development
DATABASE_URL=postgresql://user:pass@host:5432/devflow
JWT_SECRET=your-secret-min-32-chars
JWT_EXPIRES_IN=7d
CLIENT_URL=http://localhost:5173

# Optional GitHub OAuth
GITHUB_CLIENT_ID=
GITHUB_CLIENT_SECRET=
```

---

## 🤝 Contributing

1. Fork the repo
2. Create a feature branch: `git checkout -b feature/amazing-feature`
3. Commit: `git commit -m 'feat: add amazing feature'`
4. Push: `git push origin feature/amazing-feature`
5. Open a Pull Request

---

Built with ⚡ by the DevFlow team
