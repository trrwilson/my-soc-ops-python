# Project Guidelines

## Mandatory Checklist
Before finishing any change, complete these steps in order:

- [ ] Lint: `uv run ruff check .`
- [ ] Build/run: `uv run uvicorn app.main:app --reload --host 0.0.0.0 --port 8000`
- [ ] Test: `uv run pytest`

## Code Style
Use Python 3.13, type hints, and snake_case throughout. Keep functions small and follow the patterns in [app/main.py](app/main.py), [app/game_service.py](app/game_service.py), and [app/game_logic.py](app/game_logic.py). Prefer immutable data and pure functions where practical.

## Architecture
Soc Ops is a FastAPI app with Jinja2 templates and HTMX-driven partial updates. Keep changes inside these boundaries unless there is a clear reason not to:

- [app/main.py](app/main.py): routes, session bootstrap, templates, static files
- [app/game_service.py](app/game_service.py): in-memory `GameSession` state
- [app/game_logic.py](app/game_logic.py): board generation, toggling, bingo detection
- [app/data.py](app/data.py): question bank and free-space text
- [app/templates/](app/templates/): page and component templates
- [app/static/](app/static/): CSS and bundled JS

`app/models.py` defines the Pydantic models, `app/game_logic.py` holds board/rule logic, and `app/game_service.py` owns session state.

## Conventions
Keep request flow and state transitions simple. Tests should stay split by concern:

- [tests/test_game_logic.py](tests/test_game_logic.py) for pure logic
- [tests/test_api.py](tests/test_api.py) for route and session behavior

For UI work, use the utility classes in [app/static/css/app.css](app/static/css/app.css) and follow [.github/instructions/css-utilities.instructions.md](.github/instructions/css-utilities.instructions.md) and [.github/instructions/frontend-design.instructions.md](.github/instructions/frontend-design.instructions.md).

## Documentation
Link to [README.md](README.md), [CONTRIBUTING.md](CONTRIBUTING.md), and [workshop/](workshop/) instead of duplicating their content.