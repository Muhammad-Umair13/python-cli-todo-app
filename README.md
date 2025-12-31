# Todo Console Application

A Python 3.13+ console-based todo application built with spec-driven development.

## Features

- **Add Tasks**: Create tasks with title and optional description
- **List Tasks**: View all tasks, filter by completed/pending status
- **Complete Tasks**: Mark tasks as completed
- **Delete Tasks**: Remove tasks from the list
- **Update Tasks**: Modify task title and description
- **Toggle Tasks**: Switch task completion status

## Quick Start

### Installation

```bash
# Clone the repository
git clone <repository-url>
cd todo_app

# Install dependencies
pip install -e ".[dev]"

# Or using UV
uv pip install -e ".[dev]"
```

### Usage

```bash
# Add a task
todo add "Buy groceries"

# Add a task with description
todo add "Buy groceries" -d "Milk, eggs, bread"

# List all tasks
todo list

# List only completed tasks
todo list --completed

# List only pending tasks
todo list --pending

# Mark a task as complete
todo complete 1

# Update a task
todo update 1 "New title" -d "New description"

# Delete a task
todo delete 1

# Toggle task status
todo toggle 1

# Get help
todo --help
todo add --help
```

## Project Structure

```
todo_app/
├── src/
│   ├── __init__.py
│   ├── main.py              # Entry point
│   ├── exceptions.py        # Custom exceptions
│   ├── models/
│   │   ├── __init__.py
│   │   └── task.py          # Task dataclass
│   ├── services/
│   │   ├── __init__.py
│   │   ├── memory.py        # In-memory storage
│   │   └── task_service.py  # Business logic
│   └── cli/
│       ├── __init__.py
│       ├── parser.py        # argparse configuration
│       └── commands.py      # Command handlers
├── tests/
│   ├── __init__.py
│   ├── conftest.py          # Pytest fixtures
│   ├── unit/
│   │   ├── test_task.py
│   │   ├── test_memory.py
│   │   └── test_task_service.py
│   └── integration/
│       └── test_cli.py
├── pyproject.toml
└── README.md
```

## Development

### Running Tests

```bash
# Run all tests
pytest

# Run with coverage
pytest --cov=src --cov-report=term-missing

# Run specific test file
pytest tests/unit/test_task.py

# Run specific test
pytest tests/unit/test_task.py::TestTaskCreation::test_task_creation_with_title_only
```

### Type Checking

```bash
# Run mypy
mypy src/

# Run ruff linter
ruff check src/ tests/

# Format code
ruff format src/ tests/
```

### Spec-Driven Development

This project follows Spec-Kit Plus methodology:

1. **Constitution** → Project principles (`.specify/memory/constitution.md`)
2. **Specify** → Feature specs (`.specs/001-todo-console-app/spec.md`)
3. **Plan** → Implementation plan (`.specs/001-todo-console-app/plan.md`)
4. **Tasks** → Executable tasks (`.specs/001-todo-console-app/tasks.md`)
5. **Implement** → Red-Green-Refactor cycle

## Architecture

```
┌─────────────────────────────────────────────────────────┐
│                      main.py                             │
│                    (entry point)                         │
└─────────────────────┬───────────────────────────────────┘
                      │
                      ▼
┌─────────────────────────────────────────────────────────┐
│                    cli/parser.py                         │
│              (argparse configuration)                    │
└──────────┬──────────────────────────┬──────────────────┘
           │                          │
           ▼                          ▼
┌─────────────────────┐    ┌─────────────────────────────┐
│   cli/commands.py   │    │    services/task_service.py │
│  (command handlers) │    │     (business logic)         │
└──────────┬──────────┘    └──────────────┬──────────────┘
           │                             │
           │                             ▼
           │                     ┌─────────────────┐
           │                     │  models/task.py │
           │                     │  (Task dataclass)│
           │                     └─────────────────┘
           ▼
      ┌────────────────────────────────────────────┐
      │         In-Memory Storage (dict)            │
      │  {1: Task(...), 2: Task(...), ...}         │
      └────────────────────────────────────────────┘
```

## Phase Evolution

This is Phase 1 of a 5-phase project:

- **Phase 1** (Current): In-memory Python console app
- **Phase 2**: Add file-based persistence (JSON/JSONL)
- **Phase 3**: Web API with FastAPI
- **Phase 4**: AI-powered features (smart categorization)
- **Phase 5**: Cloud deployment with sync

## License

MIT
