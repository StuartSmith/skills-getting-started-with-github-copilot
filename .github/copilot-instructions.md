# Mergington High School Activities API - AI Coding Instructions

## Project Overview
This is a **simple educational FastAPI application** for high school extracurricular activities signup. The architecture is intentionally minimal: single-file API (`src/app.py`) with in-memory data storage and vanilla JavaScript frontend.

## Key Architecture Patterns

### Data Model Design
- **Activities use name as primary key** (not IDs): `activities["Chess Club"]`
- **Students identified by email**: `michael@mergington.edu` format
- **In-memory storage only** - data resets on server restart (this is intentional for the educational context)

### API Structure
- Root `/` redirects to static frontend at `/static/index.html`
- RESTful endpoints: `GET /activities` and `POST /activities/{activity_name}/signup`
- **Query parameter pattern**: Email passed as `?email=student@mergington.edu` not in request body
- Static files mounted at `/static/` serve the vanilla JS frontend

### Frontend Architecture
- **Vanilla JavaScript** (no frameworks) in `src/static/app.js`
- **Fetch-based API calls** with proper error handling and URL encoding
- **DOM manipulation** for dynamic activity cards and form population
- **CSS classes for state**: `.hidden`, `.success`, `.error` for UI feedback

## Development Workflow

### Running the Application
```bash
# Install dependencies
pip install fastapi uvicorn

# Run from src/ directory
cd src
python app.py
```

### API Testing
- **Interactive docs**: http://localhost:8000/docs (FastAPI auto-generated)
- **Alternative docs**: http://localhost:8000/redoc
- **Frontend**: http://localhost:8000/ (auto-redirects to static/index.html)

## Code Conventions

### FastAPI Patterns
- Use `raise HTTPException(status_code=404, detail="...")` for errors
- Mount static files with explicit path joining: `os.path.join(Path(__file__).parent, "static")`
- Function-based endpoints (not classes) with descriptive docstrings

### Frontend Patterns
- **Event-driven**: Use `DOMContentLoaded` for initialization
- **Async/await** for all API calls with try-catch error handling
- **URL encoding**: Always use `encodeURIComponent()` for user input in URLs
- **Form reset**: Clear forms on successful submission

### Data Validation
- **Client-side**: HTML5 validation (`required`, `type="email"`)
- **Server-side**: Minimal validation - check activity exists before signup
- **No duplicate prevention**: Students can sign up multiple times (educational simplicity)

## Project-Specific Considerations
- This is a **GitHub Skills tutorial project** - keep implementations simple and educational
- **No database setup** - in-memory storage is the intended pattern
- **No authentication** - email is treated as user identifier without verification
- **No business logic complexity** - focus on demonstrating API/frontend integration patterns

When extending this codebase, maintain the educational simplicity while demonstrating good FastAPI and vanilla JavaScript practices.