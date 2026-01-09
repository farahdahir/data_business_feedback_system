# KRA Feedback Management System - Setup Guide

This guide will help you set up the Feedback Management System on your local machine. This project consists of a **Node.js/Express Backend** and a **React Frontend**.

## 📋 Prerequisites

Before you begin, ensure you have the following installed on your computer:

1.  **Node.js & npm** (Long Term Support version recommended)
    *   [Download Node.js](https://nodejs.org/)
2.  **PostgreSQL** (Database)
    *   [Download PostgreSQL](https://www.postgresql.org/download/)
    *   *During installation, remember the password you set for the `postgres` user.*
3.  **Git** (Version Control)
    *   [Download Git](https://git-scm.com/downloads)

## 🚀 Installation & Setup

https://github.com/farahdahir/data_business_feedback_system

### 1. Clone the Repository

Open your terminal (Command Prompt, PowerShell, or Terminal) and run:

```bash
git clone <repository_url>
cd "Data_business_team - Feedback_system"
```

### 2. Install Dependencies

You need to install libraries for both the server (backend) and client (frontend).

**Root Dependencies:**
```bash
npm install
```

**Server Dependencies:**
```bash
cd server
npm install
```

**Client Dependencies:**
```bash
cd ../client
npm install
```

### 3. Database Setup

1.  **Open PostgreSQL Shell (psql) or pgAdmin.**
2.  **Create the database:**
    ```sql
    CREATE DATABASE feedback_system;
    ```
3.  **Configure Environment Variables:**
    *   Go to the `server` folder.
    *   Create a file named `.env` (if it doesn't exist, you can copy `.env.example` if available, or use the template below).
    *   Add the following content:

    ```env
    PORT=5000
    NODE_ENV=development
    JWT_SECRET=mysecuresecretkey123
    DB_HOST=localhost
    DB_PORT=5432
    DB_NAME=feedback_system
    DB_USER=postgres
    DB_PASSWORD=YOUR_POSTGRES_PASSWORD_HERE
    UPLOAD_DIR=./uploads
    CLIENT_URL=http://localhost:3000
    ```
    *   **Important:** Replace `YOUR_POSTGRES_PASSWORD_HERE` with the password you set when installing PostgreSQL.

4.  **Create Database Tables:**
    *   In your terminal (from the root project folder), run:
    ```bash
    psql -U postgres -d feedback_system -f server/database/schema.sql
    ```
    *   *If the command `psql` is not found, you may need to add PostgreSQL to your system PATH or run the SQL commands from `server/database/schema.sql` manually inside pgAdmin.*

### 4. Create Uploads Folder

The server needs a place to store uploaded files.

```bash
mkdir server/uploads
```

---

## 🏃‍♂️ Running the Application

You need to run both the backend and frontend servers.

**Option 1: Run everything at once (Recommended)**

From the main project folder:
```bash
npm run dev
```
*   This will start the backend on port 5000 and the frontend on port 3000.

**Option 2: Run separately**

*   **Terminal 1 (Backend):**
    ```bash
    cd server
    npm run dev
    ```
*   **Terminal 2 (Frontend):**
    ```bash
    cd client
    npm start
    ```

Access the app at: **[http://localhost:3000](http://localhost:3000)**

---

## 🛠 Troubleshooting

**1. "pksql is not recognized..."**
*   This means PostgreSQL is not in your system PATH.
*   **Fix:** Open pgAdmin, connect to the database, open the Query Tool, and copy-paste the contents of `server/database/schema.sql`.

**2. "Connection refused" (Database error)**
*   Make sure PostgreSQL is running (search for "Services" in Windows and check PostgreSQL).
*   Check your `.env` file in the `server` folder. Ensure `DB_PASSWORD` is correct.

**3. "Module not found"**
*   Make sure you ran `npm install` in both `server` and `client` folders.

**4. Port 5000/3000 already in use**
*   Close other running Node.js processes or change the ports in `.env`.

-----------------------------------------------------------------------------------------------------
## Initial Setup

### Create Admin User

You can create an admin user directly in the database:

```sql
-- Hash a password first (use bcrypt or an online tool)
-- Example password: "admin123" hashed
INSERT INTO users (name, email, password_hash, role) 
VALUES ('Admin User', 'admin@kra.go.ke', '$2a$10$...', 'admin');
```

### Create Teams

1. Log in as admin
2. Go to Admin Dashboard > Teams
3. Create teams (e.g., Team 1, Team 2, Team 3, Team 4, Team 5)

### Create Dashboards

1. Log in as admin
2. Go to Admin Dashboard > Dashboards
3. Create dashboards and assign them to teams

## Features Overview

### Business Users
- View dashboards with threads
- Create new threads
- Second existing threads
- Reply to their own threads
- Delete their threads (pending or complete only)
- View notifications

### Data Science Teams
- View issues assigned to their team
- Reply to threads
- Update thread status (Pending → In Progress → Complete)
- View team statistics
- Leaderboard tracking

### Admin
- Manage dashboards
- Manage teams and assign team leads
- Manage users and assign them to teams
- Assign issues to teams/users
- View system statistics
- Override issue status

## Production Deployment

1. Set `NODE_ENV=production` in `server/.env`
2. Build the frontend: `cd client && npm run build`
3. Serve the build folder with a web server (nginx, Apache, etc.)
4. Use a process manager (PM2) for the Node.js server
5. Set up SSL/HTTPS
6. Use environment variables for all secrets

## Support

For issues or questions, please contact the development team.

