# Developer Guide: SimuBridge

This guide documents the technical architecture and code structure of the SimuBridge project, focusing on the rewritten **Frontend** (`SimuBridge--Main`) and the **Simod Backend** (`simod_http_augemented`).

## Project Overview

SimuBridge serves as a unified interface for Process Mining (via Simod) and Business Process Simulation (via Scylla). It allows users to discover process models from event logs and configure/run simulations.

The system consists of:
1.  **Frontend**: A desktop application (Electron + React) for user interaction.
2.  **Simod Backend**: A Python-based API wrapper around the Simod process discovery tool.
3.  **Scylla Backend**: (External) A service for running Scylla simulations (expected on port 8080).

---

## 1. Frontend Architecture (`SimuBridge--Main`)

The frontend is a **React** application wrapped in **Electron**. It provides the UI for uploading logs, configuring process parameters, running discovery tasks, and viewing simulation results.

### Tech Stack
*   **Framework**: React (Create React App + Electron)
*   **UI Library**: Chakra UI, Ant Design (antd)
*   **State/Logic**: React Hooks, Axios for API calls
*   **Visualization**: BPMN.js (process models), Recharts (charts/analytics)
*   **Packaging**: Electron Builder

### Directory Structure

Located in `SimuBridge--Main/`:

*   **`frontend/`**: The main React application.
    *   **`src/`**: Source code.
        *   **`components/`**: React components arranged by feature.
            *   **`Processminer/`**: Components for the Process Mining view. Handles interaction with the Simod backend.
                *   `ProcessMinerPage.jsx`: Main page for discovery. Uploads logs to Simod API.
            *   **`Simulation/`**: Components for the Simulation view. Handles interaction with Scylla.
            *   **`EditorSidebar/`**: Configuration sidebars for editing model parameters.
            *   **`Comparision/`, `Sensitivity/`**: Analytics and result visualization.
        *   **`util/`**: Utility functions (parsing, formatting).
        *   **`App.jsx`**: Main application entry point and layout.
    *   **`public/`**: Static assets and Electron main process (`electron.js`).
*   **`simodConverter/`**: A helper module for converting data formats for Simod.
*   **`scyllaConverter/`**: A helper module for converting data formats for Scylla.
*   **`dataModel/`**: shared data definitions (likely used by converters).

### Key Integration Points
*   **Simod API**: `http://127.0.0.1:8880` (Configured in `ProcessMinerPage.jsx`)
*   **Scylla API**: `http://127.0.0.1:8080` (Configured in `SimulationPage.jsx`)

### Running the Frontend
1.  Navigate to `SimuBridge--Main/frontend`.
2.  Install dependencies:
    ```bash
    npm install
    ```
3.  Start in development mode (Browser + Electron):
    ```bash
    npm start
    ```

---

## 2. Simod Backend Architecture (`simod_http_augemented`)

This is a **Python FastAPI** service that wraps the Simod command-line tool. It exposes an HTTP API to trigger process discovery tasks and retrieve results.

### Tech Stack
*   **Framework**: FastAPI, Uvicorn
*   **Core Logic**: Simod (executed via `poetry run` subprocess)
*   **Data Handling**: Pandas

### Directory Structure

Located in `simod_http_augemented/`:

*   **`main.py`**: The entry point. Refines the FastAPI app and routes.
    *   `POST /discoveries`: Starts a discovery job.
    *   `GET /discoveries/{id}`: Checks job status.
    *   `background_tasks`: Uses `subprocess` to call the `simod` CLI tool.
*   **`requirements.txt`**: Python dependencies (FastAPI, Pandas, etc.).
*   **`Dockerfile`**: Container definition for deployment.

### How it Works
1.  **Request**: Frontend sends an event log (CSV/XES) to `POST /discoveries`.
2.  **Storage**: Files are saved to a temporary storage path (`SIMOD_HTTP_STORAGE_PATH` or `/tmp/simod`).
3.  **Execution**: The API triggers `simod` in a background thread using a shell command (`poetry run simod ...`).
    *   *Note: This assumes the environment has Simod installed and accessible via Poetry.*
4.  **Response**: The frontend polls the status and eventually downloads the results (BPMN models, statistics).

### Running the Backend
1.  Navigate to `simod_http_augemented`.
2.  Install requirements:
    ```bash
    pip install -r requirements.txt
    ```
3.  Run the server:
    ```bash
    python main.py
    # OR
    uvicorn main:app --host 0.0.0.0 --port 8880
    ```
    *Note: Ensure the underlying `simod` tool is properly installed in the environment for the actual discovery to work.*
