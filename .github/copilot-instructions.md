# Project Guidelines: Commit Without Secrets

## Project Purpose

This is a GitHub Skills learning repository focused on preventing secrets from being accidentally committed to version control using pre-commit hooks with gitleaks.

## Architecture

- **app.py**: Simple Python application using langchain (placeholder for user code)
- **.env**: Contains sensitive credentials (Hugging Face tokens, API keys, etc.)
- **.github/skills/**: GitHub Skills tutorial structure
- **Pre-commit setup**: Prevents secrets from entering git history

## Build and Test

### Prerequisites
Ensure Python 3.8+ is installed and on PATH:
```bash
python --version
```

### Install Dependencies
```bash
python -m pip install pre-commit
pre-commit install
```

### Run Secret Detection Locally
```bash
pre-commit run --all-files
```

### Verify Git Setup
```bash
git status
git log --oneline
```

## Project Conventions

### Secrets Management
- **Never commit secrets**: API keys, tokens, credentials must never be in git
- **Use .env files**: Store secrets in .env and add `.env` to `.gitignore`
- **Gitleaks scanning**: Pre-commit hook automatically detects high-entropy strings and known patterns

### Pre-commit Configuration
The `.pre-commit-config.yaml` file enables gitleaks scanning on every commit attempt:
- Blocks commits containing suspected secrets
- Prevents pushing secrets to remote

### Environment Variables
- Add sensitive values to `.env`
- Load at runtime via environment variable interpolation
- Example: `hugging_face_hub_token="hf_..."` in .env

## Integration Points

- **GitHub Skills**: This repo follows GitHub Skills tutorial structure in `.github/skills/`
- **Git hooks**: Pre-commit framework integrates with local git workflow
- **Gitleaks**: Third-party tool for entropy-based and pattern-based secret detection

## Security Best Practices

1. **Always use pre-commit**: Run `pre-commit run --all-files` before first push
2. **Rotate exposed secrets**: If a secret reaches git history, rotate it immediately
3. **Git history cleanup**: Use `git filter-branch` or BFG to remove secrets from history
4. **Environment-based config**: Use environment variables for secrets, never hardcode

## Key Files to Reference

- [app.py](app.py): User application code
- [.env](.env): Secret credentials (git-ignored)
- [.gitignore](.gitignore): Ensures .env is never committed
