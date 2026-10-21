# OmniCopy API

A learning project built with **FastAPI**: a backend for managing marketing campaigns and the copy (social posts, newsletters, blog posts) that goes with them. The idea is to write content once and distribute it across all channels.

This README documents the project **up to the "Hello World" and auto-generated docs stage**. It will grow as the project does.

## Tech Stack

- **Python 3.10+**
- **[FastAPI](https://fastapi.tiangolo.com/)**: web framework (async, type-hint driven)
- **Pydantic**: data validation (bundled with FastAPI)
- **Uvicorn / FastAPI CLI**: dev server (installed via `fastapi[standard]`)
- **Swagger UI**: interactive API docs, auto-generated from the OpenAPI spec

## Why FastAPI?

- Fast to run and fast to write.
- **Automatic interactive documentation** that follows the OpenAPI specification.
- Built on Pydantic, so request and response data is validated against the types you declare.
- Docs describe the expected data structures, so API consumers know how to call it.

## Getting Started

### 1. Clone the repository

```bash
git clone <your-repo-url>
cd omnicopy
```

### 2. Create a virtual environment

**macOS / Linux**
```bash
python3 -m venv .venv
source .venv/bin/activate
```

**Windows (PowerShell)**
```powershell
py -m venv .venv
.venv\Scripts\Activate.ps1
```

**Windows (Command Prompt)**
```bat
py -m venv .venv
.venv\Scripts\activate.bat
```

> **PowerShell blocks the activate script?** Run this once, then activate again:
> ```powershell
> Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned
> ```

When it works, `(.venv)` appears at the start of your prompt.

### 3. Install dependencies

```bash
python -m pip install --upgrade pip
pip install -r requirements.txt
```

### 4. Run the development server

```bash
fastapi dev main.py
```

The server auto-reloads whenever you save a file.

## Open the App

| URL | Description |
|---|---|
| http://127.0.0.1:8000/ | API root (returns the Hello World message) |
| http://127.0.0.1:8000/docs | Swagger UI, interactive documentation |
| http://127.0.0.1:8000/openapi.json | The generated OpenAPI specification |

## Building This From Scratch

If you want to recreate the project rather than clone it:

**macOS / Linux**
```bash
mkdir omnicopy && cd omnicopy
python3 -m venv .venv
source .venv/bin/activate
echo ".venv" > .gitignore
echo "__pycache__/" >> .gitignore
python3 -m pip install --upgrade pip
pip install "fastapi[standard]"
pip freeze > requirements.txt
git init
git add .
git commit -m "Initial commit"
touch main.py
```

**Windows (PowerShell)**
```powershell
mkdir omnicopy; cd omnicopy
py -m venv .venv
.venv\Scripts\Activate.ps1
Set-Content -Path .gitignore -Value ".venv"
Add-Content -Path .gitignore -Value "__pycache__/"
python -m pip install --upgrade pip
pip install "fastapi[standard]"
pip freeze | Out-File -Encoding utf8 requirements.txt
git init
git add .
git commit -m "Initial commit"
New-Item main.py -ItemType File
```

Notes:
- `"fastapi[standard]"` installs FastAPI plus the CLI and dev server. The quotes matter in zsh (macOS).
- `.venv` is git-ignored so the environment isn't committed. `requirements.txt` lets anyone recreate it.
- On Windows PowerShell, `pip freeze | Out-File -Encoding utf8 ...` avoids a UTF-16 file encoding problem that `>` can cause in Windows PowerShell 5.1.

## The First App (`main.py`)

```python
from fastapi import FastAPI

app = FastAPI()


@app.get("/")
async def root():
    return {"message": "Hello World"}
```

How it works:

- `app = FastAPI()` creates the application instance everything attaches to.
- `@app.get("/")` is a **decorator** that links an HTTP method (`GET`) and a path (`/`) to the function below it.
- That function is a **path operation function**. Each method + path combination gets its own.
- Returning a dictionary produces a JSON response.

## Auto-Generated Documentation

FastAPI builds an **OpenAPI** specification from your code and serves it at `/openapi.json`. **Swagger UI** reads that spec and renders the interactive page at `/docs`.

| Term | Meaning |
|---|---|
| **OpenAPI** | The specification: a JSON description of your API |
| **Swagger** | A suite of tools that implement the spec, including the interactive docs UI |

From `/docs` you can expand each endpoint, see its possible responses, and use **Try it out** to send real requests, with no extra tooling needed.

## Editor Setup (VS Code)

1. Install the **Python** and **Pylance** extensions.
2. Select the `.venv` interpreter: `Ctrl/Cmd + Shift + P` → **Python: Select Interpreter**.
3. Optional: turn on strict type checking in your user `settings.json`:

   ```json
   "python.analysis.typeCheckingMode": "strict"
   ```

   Restart VS Code if it doesn't take effect.

## Project Structure

```
omnicopy/
├── .venv/               # virtual environment (git-ignored)
├── .gitignore
├── main.py              # FastAPI application
├── requirements.txt     # pinned dependencies
└── README.md
```

## Roadmap

- [x] Project setup (virtual environment, git, dependencies)
- [x] Hello World endpoint
- [x] Interactive docs at `/docs` and OpenAPI spec at `/openapi.json`
- [ ] Define the Campaign data structure
- [ ] CRUD endpoints for campaigns (`/api/v1/campaigns`)
- [ ] Database persistence (SQLModel + SQLite)
- [ ] Typed request and response models
- [ ] Relationships (campaign → content pieces)
- [ ] Pagination and query parameters
- [ ] Middleware and authentication

## Resources

- [FastAPI documentation](https://fastapi.tiangolo.com/)
- [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Swagger UI](https://swagger.io/tools/swagger-ui/)
- Based on Caleb's FastAPI tutorial series
