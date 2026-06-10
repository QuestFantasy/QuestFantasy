# QuestFantasy

QuestFantasy is a modular multiplayer game application featuring a C#-powered **Godot Engine 3.6.2 Mono** client and a **Django Python** backend running inside a PostgreSQL Docker container.

---

## 📂 Repository Structure

The project is split into two main modules:
*   [frontend/](file:///home/darrin/QuestFantasy/frontend): The game client built with Godot 3.6.2 Mono Edition (C#).
*   [backend/](file:///home/darrin/QuestFantasy/backend): The Django web server managing user authentication, game session synchronization, and the online trade shop.

---

## 🛠️ Prerequisites

Before you start, make sure you have the following installed on your machine:

1.  **For the Backend**:
    *   [Docker](https://docs.docker.com/get-docker/) & [Docker Compose](https://docs.docker.com/compose/install/)
2.  **For the Frontend**:
    *   [Godot Engine 3.6.2 Mono Edition](https://godotengine.org/download/archive/3.6.2-stable/) (Make sure it is the **Mono** version with C# support)
    *   [.NET SDK 6.0](https://dotnet.microsoft.com/download)

---

## 🚀 Quick Start Guide

### 1. Initialize Submodules
If you cloned the repository without recursive submodules, run the following command to download the frontend and backend modules:
```bash
git submodule update --init --recursive
```

---

### 2. Run the Backend (Docker)
1.  Navigate to the backend folder:
    ```bash
    cd backend
    ```
2.  Set up the environment variables:
    ```bash
    cp .env.example .env
    ```
    *(Open `.env` and fill in a strong `SECRET_KEY`, database credentials, and session token expiration settings).*
3.  Launch the services in detached mode:
    ```bash
    docker compose up --build -d
    ```
    *The web server will automatically boot up, connect to the PostgreSQL database, and run system migrations.*

---

### 3. Run the Frontend (Godot Mono)
1.  Navigate to the frontend folder:
    ```bash
    cd frontend
    ```
2.  Restore NuGet dependencies and compile the C# solution:
    ```bash
    dotnet restore
    dotnet build QuestFantasy.sln
    ```
3.  Open the game:
    *   Launch the **Godot 3.6.2 Mono** editor and import the `frontend/` directory.
    *   Or, run the game directly from the command line:
        ```bash
        godot --path .
        ```

---

## ⚙️ Configuration & Networking
By default, the frontend connects to the backend at `http://127.0.0.1:8000`. 
If you run the backend on a remote host or a different port:
*   Open the project in Godot.
*   Locate [AuthApiClient.cs](file:///home/darrin/QuestFantasy/frontend/Scripts/Auth/AuthApiClient.cs), [AuthFlowController.cs](file:///home/darrin/QuestFantasy/frontend/Scripts/Auth/AuthFlowController.cs), or [Main.cs](file:///home/darrin/QuestFantasy/frontend/Scripts/Main.cs) in the Godot inspector.
*   Modify the `BackendBaseUrl` parameter to point to your backend server.

---

## 🐳 Backend Maintenance Commands
*   **Check status**: `docker compose ps`
*   **View server logs**: `docker compose logs -f web`
*   **Stop backend**: `docker compose down`
*   **Full Reset (Wipes Database)**: `docker compose down -v`
