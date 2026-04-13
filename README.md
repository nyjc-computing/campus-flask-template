# Campus Flask Template

Minimal Flask template with Campus authentication example.

## Quick Start

1. **Use this template** → Create a new repository
2. **Update project metadata** in `pyproject.toml`:
   ```toml
   name = "your-project-name"
   description = "Your description"
   authors = ["Your Name <you@email.com>"]
   ```
3. **Set up environment variables:**
   ```bash
   cp .env.example .env
   # Edit .env with your actual values
   ```
4. **Install and run:**
   ```bash
   poetry install
   poetry run python main.py
   ```

### Environment Variables

Copy `.env.example` to `.env` and configure:
- `SECRET_KEY`: Required for Flask session security (generate with `python -c 'import secrets; print(secrets.token_hex(32))'`)
- `CLIENT_ID`, `CLIENT_SECRET`: Campus OAuth credentials (if using Campus auth)
- `CAMPUS_TIMEOUT`, `CAMPUS_MODE`: Optional Campus configuration

## Campus Authentication

This template includes a Campus OAuth authentication example.

**Protect routes:**
```python
@app.get("/home")
@login_manager.login_required
def home():
    user: User = flask.g.user
    return flask.render_template('home.html', user=user)
```

**Access user data:**
```python
user: User = flask.g.user  # user.name, user.email, etc.
```

**Remove Campus auth:** Delete from `main.py`:
- `login_manager` setup (lines 23-29)
- `flask_campus` import (line 8)
- Campus client initialization (line 21)

## Project Structure

```
├── main.py           # Flask app with Campus auth example
├── templates/        # Minimal HTML templates
│   ├── base.html     # Base template (extend this)
│   ├── index.html    # Landing page example
│   └── home.html     # Authenticated page example
├── static/           # Static assets (CSS, JS)
└── pyproject.toml    # Poetry dependencies
```

## Deployment

Use `requirements.txt` for production deployments.