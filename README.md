# Tasks Flask CRUD

A simple REST API for managing tasks, built with Python and Flask. This project demonstrates the fundamentals of CRUD (Create, Read, Update, Delete) operations using an in-memory data store.

## Table of Contents

- [About the Project](#about-the-project)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Getting Started](#getting-started)
  - [Prerequisites](#prerequisites)
  - [Installation](#installation)
  - [Running the Server](#running-the-server)
- [API Endpoints](#api-endpoints)
  - [Create a Task](#create-a-task)
  - [Get All Tasks](#get-all-tasks)
  - [Get a Task by ID](#get-a-task-by-id)
  - [Update a Task](#update-a-task)
  - [Delete a Task](#delete-a-task)
- [Running Tests](#running-tests)

---

## About the Project

This API allows you to manage a list of tasks. Each task has a title, an optional description, and a completion status. All data is stored in memory, so it is reset every time the server restarts. It is intended as a learning resource for Flask REST API development.

## Tech Stack

| Tool | Version | Purpose |
|------|---------|---------|
| Python | 3.12+ | Programming language |
| Flask | ≥ 3.1.3 | Web framework |
| Werkzeug | ≥ 3.1.6 | WSGI utilities (Flask dependency) |
| pytest | 7.4.3 | Testing framework |
| requests | 2.31.0 | HTTP client used in tests |
| uv | — | Fast Python package manager |

## Project Structure

```
Tasks-Flask-CRUD/
├── app.py                    # Flask application and route definitions
├── models/
│   └── task.py              # Task model class
├── tests.py                 # Integration tests
├── pyproject.toml           # Project metadata and dependencies
├── uv.lock                  # Locked dependency versions
├── assets/
│   ├── documentation.x-yaml # OpenAPI 3.0 specification
│   └── postman.x-yaml       # Postman collection
└── README.md
```

## Getting Started

### Prerequisites

- Python 3.12 or higher
- [uv](https://docs.astral.sh/uv/) (recommended) **or** pip

### Installation

**Using uv (recommended):**

```bash
uv sync
```

**Using pip:**

```bash
pip install flask werkzeug
```

### Running the Server

```bash
python app.py
```

The server will start in debug mode and be available at `http://127.0.0.1:5000`.

---

## API Endpoints

> **Note:** The API returns response messages in Portuguese.

### Create a Task

**POST** `/tasks`

Creates a new task.

**Request body:**

```json
{
  "title": "Buy groceries",
  "description": "Milk, eggs, bread"
}
```

> `description` is optional.

**Response** `200 OK`:

```json
{
  "message": "Nova tarefa criada com sucesso!",
  "id": 1
}
```

---

### Get All Tasks

**GET** `/tasks`

Returns a list of all tasks.

**Response** `200 OK`:

```json
{
  "tasks": [
    {
      "id": 1,
      "title": "Buy groceries",
      "description": "Milk, eggs, bread",
      "completed": false
    }
  ],
  "total_tasks": 1
}
```

---

### Get a Task by ID

**GET** `/tasks/<id>`

Returns a single task by its ID.

**Response** `200 OK`:

```json
{
  "id": 1,
  "title": "Buy groceries",
  "description": "Milk, eggs, bread",
  "completed": false
}
```

**Response** `404 Not Found`:

```json
{
  "message": "Não foi possível encontrar a atividade"
}
```

---

### Update a Task

**PUT** `/tasks/<id>`

Updates the title, description, and completion status of a task.

**Request body:**

```json
{
  "title": "Buy groceries",
  "description": "Milk, eggs, bread, butter",
  "completed": true
}
```

**Response** `200 OK`:

```json
{
  "message": "Tarefa atualizada com sucesso"
}
```

**Response** `404 Not Found`:

```json
{
  "message": "Não foi possível encontrar a atividade"
}
```

---

### Delete a Task

**DELETE** `/tasks/<id>`

Deletes a task by its ID.

**Response** `200 OK`:

```json
{
  "message": "Tarefa deletada com sucesso"
}
```

**Response** `404 Not Found`:

```json
{
  "message": "Não foi possível encontrar a atividade"
}
```

---

## Running Tests

The test suite uses `pytest` and makes live HTTP requests, so **the Flask server must be running** before executing the tests.

1. Start the server in one terminal:

```bash
python app.py
```

2. In a second terminal, run the tests:

```bash
pytest tests.py -v
```