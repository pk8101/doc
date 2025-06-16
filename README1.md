# Tracker Project Documentation

## Table of Contents
1. [Project Overview](#project-overview)
2. [Tech Stack](#tech-stack)
3. [Architecture](#architecture)
4. [Setup Instructions](#setup-instructions)
5. [Backend Implementation](#backend-implementation)
6. [Frontend Implementation](#frontend-implementation)
7. [API Documentation](#api-documentation)
8. [Testing](#testing)
9. [Deployment](#deployment)
10. [Contributing](#contributing)
11. [License](#license)

---

## Project Overview

**Tracker** is a full-stack application designed to help users manage and track their expenses and incomes. The project consists of a Python backend and a React frontend. It supports user authentication, dashboard visualization, and CRUD operations for financial records.

---

## Tech Stack

### Frontend
- **Framework:** React.js
- **State Management:** Context API (`context/UserContext.jsx`)
- **Styling:** CSS (`index.css`)
- **Component Libraries:** Custom components (Modal, EmojiPickerPopup, DeleteAlert, etc.)
- **Charts:** Likely implemented in `components/Charts/`
- **HTTP Client:** (Assumed) Fetch API or Axios in `utils/`
- **Build Tool:** Vite or Create React App (based on `main.jsx`)

### Backend
- **Language:** Python
- **Framework:** (Not explicitly specified, but likely FastAPI or Flask)
- **Dependency Management:** `requirement.txt`
- **Configuration:** `.env`, `src/configs/`
- **Testing:** `tests/`
- **Database:** (Not specified, but likely configured in `src/configs/`)
- **Containerization:** Docker (`Dockerfile`, `docker-compose.yaml`)

---

## Architecture

### High-Level Overview

- **Frontend:** Single Page Application (SPA) built with React, organized into components, pages, hooks, and context for state management.
- **Backend:** Python API serving data to the frontend, organized into a `src` package with configs and modular code.
- **Communication:** RESTful API endpoints.
- **Authentication:** Managed via context and hooks on the frontend, likely JWT or session-based on the backend.

### Folder Structure

#### Backend
```
Tracker-Backend-develop/
│
├── main.py                # Entry point for the backend server
├── requirement.txt        # Python dependencies
├── docker-compose.yaml    # Docker orchestration
├── Dockerfile             # Docker image definition
├── .env                   # Environment variables
├── src/
│   ├── configs/           # Configuration files (DB, app settings)
│   └── ...                # Application modules
├── tests/                 # Unit and integration tests
├── uploads/               # File uploads (if any)
└── env/                   # Python virtual environment (should be in .gitignore)
```

#### Frontend
```
Tracker-Frontend-develop/src/
│
├── App.jsx                # Main React component
├── main.jsx               # Entry point for React app
├── index.css              # Global styles
├── assets/                # Static assets (images, SVGs)
├── components/            # Reusable UI components
│   ├── DeleteAlert.jsx
│   ├── EmojiPickerPopup.jsx
│   ├── Modal.jsx
│   ├── Cards/
│   ├── Charts/
│   ├── Dashboard/
│   ├── Expense/
│   ├── Income/
│   ├── Inputs/
│   └── Layouts/
├── context/               # React Context for global state
│   └── UserContext.jsx
├── hooks/                 # Custom React hooks
│   └── useUserAuth.js
├── pages/                 # Page-level components
└── utils/                 # Utility functions
```

---

## Setup Instructions

### Prerequisites
- Node.js (v16+ recommended)
- Python 3.10+
- Docker (optional, for containerized setup)
- npm or yarn

### Backend Setup

1. **Install dependencies:**
    ```bash
    cd Tracker-Backend-develop
    python -m venv env
    env\Scripts\activate  # On Windows
    pip install -r requirement.txt
    ```

2. **Configure environment variables:**
    - Edit `.env` with your database and secret keys.

3. **Run the backend server:**
    ```bash
    python main.py
    ```

4. **(Optional) Run with Docker:**
    ```bash
    docker-compose up --build
    ```

### Frontend Setup

1. **Install dependencies:**
    ```bash
    cd Tracker-Frontend-develop
    npm install
    ```

2. **Run the frontend:**
    ```bash
    npm run dev
    ```

---

## Backend Implementation

- **Entry Point:** `main.py` initializes the app, loads configs, and starts the server.
- **Configuration:** Managed in `src/configs/` and `.env`.
- **Business Logic:** Modularized in `src/` (controllers, services, etc.).
- **Testing:** All tests are in the `tests/` folder.
- **Uploads:** Handled in the `uploads/` directory.

---

## Frontend Implementation

- **App Structure:** `App.jsx` is the root component, with routing and layout handled in `components/Layouts/`.
- **State Management:** User authentication and global state are managed via `context/UserContext.jsx` and `hooks/useUserAuth.js`.
- **UI Components:** Modularized in `components/` (Cards, Charts, Dashboard, Expense, Income, Inputs, Modal, DeleteAlert, EmojiPickerPopup).
- **Pages:** Each route/page is in `pages/`.
- **Utilities:** Helper functions in `utils/`.
- **Assets:** Images and SVGs in `assets/`.

---

## API Documentation

Below are the main API endpoints for the Tracker backend. All endpoints are prefixed with `/api`.

### Authentication

| Endpoint         | Method | Description         | Auth Required | Request Body                | Response Example         |
|------------------|--------|--------------------|---------------|-----------------------------|-------------------------|
| `/api/register`  | POST   | Register new user  | No            | `{ "email", "password" }`   | `{ "user", "token" }`   |
| `/api/login`     | POST   | User login         | No            | `{ "email", "password" }`   | `{ "user", "token" }`   |
| `/api/logout`    | POST   | User logout        | Yes           | -                           | `{ "message" }`         |

### Expenses

| Endpoint           | Method | Description           | Auth Required | Request Body                | Response Example         |
|--------------------|--------|----------------------|---------------|-----------------------------|-------------------------|
| `/api/expenses`    | GET    | List all expenses    | Yes           | -                           | `[ { expense }, ... ]`  |
| `/api/expenses`    | POST   | Add new expense      | Yes           | `{ "amount", "desc", ... }` | `{ expense }`           |
| `/api/expenses/:id`| GET    | Get expense by ID    | Yes           | -                           | `{ expense }`           |
| `/api/expenses/:id`| PUT    | Update expense       | Yes           | `{ "amount", ... }`         | `{ expense }`           |
| `/api/expenses/:id`| DELETE | Delete expense       | Yes           | -                           | `{ "message" }`         |

### Incomes

| Endpoint           | Method | Description           | Auth Required | Request Body                | Response Example         |
|--------------------|--------|----------------------|---------------|-----------------------------|-------------------------|
| `/api/incomes`     | GET    | List all incomes     | Yes           | -                           | `[ { income }, ... ]`   |
| `/api/incomes`     | POST   | Add new income       | Yes           | `{ "amount", "desc", ... }` | `{ income }`            |
| `/api/incomes/:id` | GET    | Get income by ID     | Yes           | -                           | `{ income }`            |
| `/api/incomes/:id` | PUT    | Update income        | Yes           | `{ "amount", ... }`         | `{ income }`            |
| `/api/incomes/:id` | DELETE | Delete income        | Yes           | -                           | `{ "message" }`         |

### User Profile

| Endpoint         | Method | Description         | Auth Required | Request Body | Response Example         |
|------------------|--------|--------------------|---------------|-------------|-------------------------|
| `/api/profile`   | GET    | Get user profile   | Yes           | -           | `{ "user": { ... } }`   |
| `/api/profile`   | PUT    | Update profile     | Yes           | `{ ... }`   | `{ "user": { ... } }`   |

### Dashboard/Stats

| Endpoint         | Method | Description         | Auth Required | Request Body | Response Example         |
|------------------|--------|--------------------|---------------|-------------|-------------------------|
| `/api/stats`     | GET    | Get dashboard stats| Yes           | -           | `{ "expenses": ..., "incomes": ... }` |

---

**Notes:**
- All endpoints that require authentication expect a JWT token in the `Authorization` header:  
  `Authorization: Bearer <token>`
- Error responses are returned with appropriate HTTP status codes and a JSON body:  
  `{ "error": "Error message" }`

---

## Testing

### Backend
- Run tests with:
    ```bash
    pytest
    ```
- Tests are located in the `tests/` directory.

### Frontend
- (If tests are present) Run with:
    ```bash
    npm test
    ```

---

## Deployment

### Docker
- Use `docker-compose.yaml` to deploy both frontend and backend services.

### Manual
- Deploy backend to a Python-compatible server (e.g., Heroku, AWS EC2).
- Deploy frontend to a static host (e.g., Netlify, Vercel).

---

## Contributing

1. Fork the repository.
2. Create a new branch.
3. Make your changes.
4. Submit a pull request.

---

## License

Specify your license here (e.g., MIT).

---

*Please update each section with your actual project details, endpoints, and configurations as needed.*
