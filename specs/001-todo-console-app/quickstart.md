# Quickstart Guide: Todo Console Application

## Installation

### Prerequisites
- Python 3.13 or higher
- pip (comes with Python)

### Setup

```bash
# Clone the repository
git clone <repository-url>
cd todo_app

# Create virtual environment
python -m venv venv

# Activate virtual environment
# On Windows:
venv\Scripts\activate
# On macOS/Linux:
source venv/bin/activate

# Install dependencies
pip install -e .
```

### Verify Installation

```bash
todo --help
```

You should see the help output:
```
usage: todo [-h] [--version] {add,list,complete,delete,update} ...

Manage your todo list

options:
  -h, --help            show this help message and exit
  --version             show program's version number and exit

commands:
  {add,list,complete,delete,update}
    add                 Add a new task
    list                List all tasks
    complete            Mark a task as complete
    delete              Delete a task
    update              Update a task
```

---

## Usage Tutorial

### Adding Tasks

Create your first task:

```bash
todo add "Learn Python"
```

Output:
```
✓ Task created: [1] Learn Python
```

Add a task with description:

```bash
todo add "Buy groceries" -d "Milk, eggs, bread, cheese"
```

Output:
```
✓ Task created: [2] Buy groceries
```

### Listing Tasks

View all your tasks:

```bash
todo list
```

Output:
```
ID  | Status     | Title
----|------------|------------------
1   | [ ]        | Learn Python
2   | [ ]        | Buy groceries
```

View only completed tasks:

```bash
todo list --completed
```

Output:
```
No completed tasks.
```

View pending tasks:

```bash
todo list --pending
```

### Completing Tasks

Mark a task as done:

```bash
todo complete 1
```

Output:
```
✓ Task [1] marked as completed
```

Verify the status change:

```bash
todo list
```

Output:
```
ID  | Status     | Title
----|------------|------------------
1   | [x]        | Learn Python
2   | [ ]        | Buy groceries
```

### Updating Tasks

Change a task title:

```bash
todo update 2 "Buy groceries and household items"
```

Output:
```
✓ Task [2] updated
```

### Deleting Tasks

Remove a completed task:

```bash
todo delete 1
```

Output:
```
✓ Task [1] deleted
```

Verify deletion:

```bash
todo list
```

Output:
```
ID  | Status     | Title
----|------------|------------------
2   | [ ]        | Buy groceries and household items
```

---

## Common Workflows

### Daily Planning Session

```bash
# Start fresh - list current tasks
todo list

# Add new tasks for the day
todo add "Review pull requests"
todo add "Team standup meeting" -d "10:00 AM"
todo add "Complete feature implementation"

# Mark completed work
todo complete 1

# Check remaining work
todo list --pending
```

### Getting Help

Global help:
```bash
todo --help
```

Command-specific help:
```bash
todo add --help
```

Output:
```
usage: todo add [-h] [-d DESCRIPTION] title

positional arguments:
  title                 Task title

options:
  -h, --help            show this help message and exit
  -d DESCRIPTION, --description DESCRIPTION
                        Task description
```

---

## Error Handling Examples

### Invalid Task ID

```bash
todo complete 999
```

Output:
```
Error: Task 999 not found.
```

### Empty Title

```bash
todo add ""
```

Output:
```
Error: Title cannot be empty.
```

### Title Too Long

```bash
todo add "A" * 201
```

Output:
```
Error: Title must be 200 characters or less.
```

---

## Best Practices

### Task Naming
- Use clear, concise titles
- Keep titles action-oriented (e.g., "Review PR" not "PR review")
- Add descriptions for complex tasks

### Managing Large Lists
- Use `todo list --pending` to focus on active work
- Delete obsolete tasks regularly
- Break large tasks into smaller ones

### Session Management
- Remember: tasks persist only during the session
- Data is lost when the application closes
- For persistence, wait for Phase 2+

---

## Project Structure

```
todo_app/
├── src/
│   ├── models/
│   │   └── task.py          # Task dataclass
│   ├── services/
│   │   └── task_service.py  # Business logic
│   ├── cli/
│   │   ├── parser.py        # argparse setup
│   │   └── commands.py      # Command handlers
│   └── main.py              # Entry point
├── tests/
│   ├── unit/                # Unit tests
│   └── integration/         # Integration tests
├── pyproject.toml
└── README.md
```

---

## Next Steps

After this quickstart:

1. **Run Tests**: `pytest tests/ -v`
2. **View Coverage**: `pytest --cov=src tests/`
3. **Explore Code**: Review `src/` directory structure
4. **Start Implementing**: Run `/sp.tasks` to generate task list

---

## Troubleshooting

### "todo: command not found"
Ensure the virtual environment is activated:
```bash
# On Windows
venv\Scripts\activate

# On macOS/Linux
source venv/bin/activate
```

### "Python version not supported"
Install Python 3.13+ from [python.org](https://www.python.org/downloads/)

### Module not found errors
Reinstall dependencies:
```bash
pip install -e .
```
