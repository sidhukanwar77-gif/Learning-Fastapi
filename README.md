# Learning FastAPI

A personal learning journey with FastAPI — documenting progress day by day.

---

## Day 1 — Getting Started with FastAPI

# FastAPI Basics

## What is FastAPI?

FastAPI is a modern Python web framework used to build APIs quickly and efficiently.

### Why FastAPI?

* Very fast performance
* Easy to learn and write
* Automatic API documentation
* Built-in data validation
* Supports asynchronous programming (`async/await`)
* Based on modern Python type hints

---

## What is ASGI?

**ASGI (Asynchronous Server Gateway Interface)** is a standard that allows Python web applications to handle multiple requests efficiently.

FastAPI is built on ASGI.

### Popular ASGI Servers

* Uvicorn
* Hypercorn
* Daphne

Without an ASGI server, FastAPI cannot run.

---

## What is Starlette?

**Starlette** is a lightweight ASGI framework.

FastAPI is built on top of Starlette and uses it for:

* Routing
* Middleware
* WebSockets
* Background Tasks
* Request/Response handling

Think of Starlette as the foundation of FastAPI.

---

## What is Pydantic?

**Pydantic** is a data validation library.

FastAPI uses Pydantic to:

* Validate request data
* Convert data types automatically
* Generate API documentation

Example:

```python
from pydantic import BaseModel

class User(BaseModel):
    name: str
    age: int
```

If age is not an integer, FastAPI returns a validation error automatically.

---

## Concurrency vs Parallelism

### Concurrency

Handling multiple tasks by switching between them.

Example:

* Taking multiple customer orders at a restaurant.

### Parallelism

Executing multiple tasks at the same time.

Example:

* Multiple chefs cooking different dishes simultaneously.

### FastAPI Uses Concurrency

This helps FastAPI serve many requests efficiently.

---

## What is async and await?

### async

Used to define an asynchronous function.

```python
async def get_data():
    pass
```

### await

Used to wait for an asynchronous operation.

```python
result = await get_data()
```

### Why are they important?

When waiting for:

* Database queries
* API calls
* File operations

FastAPI can handle other requests instead of blocking the application.

This improves performance and scalability.

---

## What are Decorators?

Decorators add extra functionality to functions.

### Syntax

```python
@decorator_name
def my_function():
    pass
```

### FastAPI Example

```python
@app.get("/")
async def home():
    return {"message": "Hello"}
```

### Why FastAPI Uses Decorators?

Decorators tell FastAPI:

* Which URL to listen to
* Which HTTP method to use
* Which function should run

Example:

```python
@app.get("/")
```

Means:

"When someone sends a GET request to '/', run this function."

---

# First FastAPI File: main.py

```python
from fastapi import FastAPI

app = FastAPI()


@app.get("/")
async def read_root():
    return {"Hello": "World"}


@app.get("/items/{item_id}")
async def read_item(item_id: int, q: str | None = None):
    return {"item_id": item_id, "q": q}
```

---

## What is an Endpoint?

An endpoint is a URL that clients can access.

Examples:

```text
/
```

```text
/items/1
```

Each endpoint performs a specific action.

---

## What is a GET Request?

GET is used to retrieve data from the server.

Example:

```http
GET /items/1
```

The client asks the server for information.

---

## Understanding the Code

### Endpoint 1

```python
@app.get("/")
async def read_root():
    return {"Hello": "World"}
```

When a user visits:

```text
/
```

Response:

```json
{
  "Hello": "World"
}
```

---

### Endpoint 2

```python
@app.get("/items/{item_id}")
async def read_item(item_id: int, q: str | None = None):
    return {"item_id": item_id, "q": q}
```

This endpoint accepts:

* Path Parameter (`item_id`)
* Query Parameter (`q`)

Example:

```text
/items/10?q=laptop
```

Response:

```json
{
  "item_id": 10,
  "q": "laptop"
}
```

---

## Path Parameter

A value that is part of the URL path.

Example:

```text
/items/10
```

Here:

```python
item_id = 10
```

Path Parameter:

```python
/items/{item_id}
```

---

## Query Parameter

A value passed after the `?` symbol.

Example:

```text
/items/10?q=phone
```

Here:

```python
q = "phone"
```

Query Parameter:

```python
q: str | None = None
```

It is optional because the default value is `None`.

---

## FastAPI Converts Dictionary to JSON

When we return:

```python
return {"Hello": "World"}
```

FastAPI automatically converts it into JSON:

```json
{
  "Hello": "World"
}
```

No need to manually convert Python dictionaries into JSON.

---

## Run the Project

Install dependencies:

```bash
pip install fastapi uvicorn
```

Run the server:

```bash
uvicorn main:app --reload
```

### Explanation

* `main` → filename (`main.py`)
* `app` → FastAPI object (`app = FastAPI()`)
* `--reload` → automatically reloads the server when code changes

---

## Summary

* FastAPI is a modern framework for building APIs.
* FastAPI is built on Starlette and Pydantic.
* ASGI allows asynchronous request handling.
* `async` and `await` improve performance.
* Decorators define API routes.
* Endpoints are URLs exposed by the API.
* GET requests retrieve data.
* Path parameters come from the URL path.
* Query parameters come after `?`.
* FastAPI automatically converts Python dictionaries into JSON.
* Uvicorn is used to run FastAPI applications.


> More days coming soon...
