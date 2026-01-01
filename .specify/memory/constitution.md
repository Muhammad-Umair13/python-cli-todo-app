<!--
SYNC IMPACT REPORT
==================
Version change: NEW (initial creation)
Added sections:
- 6 Core Principles (I-VI)
- Technical Constraints section
- Development Workflow section
Removed sections: None (initial creation)

Templates Status:
- .specify/templates/spec-template.md: ✅ Compatible (no changes needed)
- .specify/templates/plan-template.md: ✅ Compatible (no changes needed)
- .specify/templates/tasks-template.md: ✅ Compatible (no changes needed)
-->

# Todo Application Constitution

## Core Principles

### I. Spec-Driven Development First

ALL code MUST be generated from specifications. No manual coding allowed. Every feature follows the pipeline: Constitution → Specify → Plan → Tasks → Implement. Specifications are the single source of truth. Manual implementation without prior specification is prohibited.

**Rationale**: Ensures consistency, traceability, and quality across all development work. Prevents ad-hoc coding that leads to technical debt.

### II. Python Excellence Standard

MUST follow PEP 8 style guidelines. Type hints REQUIRED for all function signatures and public APIs. Docstrings REQUIRED for all modules, classes, and functions using Google or NumPy style. No hardcoded secrets or tokens—use environment variables and `.env` files. Imports MUST be sorted according to `isort` conventions.

**Rationale**: Maintains code readability, enables static analysis, and prevents security vulnerabilities.

### III. TDD Mandatory (NON-NEGOTIABLE)

Test-First Development is REQUIRED: Tests written → User approved → Tests fail → Then implement. Red-Green-Refactor cycle MUST be strictly enforced. Minimum 2 positive tests and 1 negative test per feature. Tests MUST use `pytest` framework with descriptive names.

**Rationale**: Ensures code correctness, enables confident refactoring, and documents expected behavior.

### IV. In-Memory Storage Phase 1

For Phase 1, storage MUST be in-memory only. Task data persists within session only. Data loss on exit is acceptable for this phase. Auto-incrementing IDs starting from 1 MUST be implemented. Thread-safe design MUST be considered for future evolution.

**Rationale**: Establishes foundation for Phase 2+ evolution without premature complexity.

### V. CLI Interface Standards

MUST use command pattern: `todo <command> [arguments] [options]`. Global help via `todo --help`. Command-specific help via `todo <command> --help`. Output MUST be human-readable with error messages to stderr.

**Rationale**: Provides intuitive, discoverable interface consistent with Unix conventions.

### VI. Measurable Acceptance Criteria

Every feature MUST have 3-5 measurable acceptance criteria. Requirements MUST be testable and verifiable. Edge cases MUST be explicitly documented. Error handling paths MUST be defined for all operations.

**Rationale**: Ensures clear completion criteria and prevents scope creep.

## Technical Constraints

### Data Model Specification

```python
class Task:
    id: int                    # Auto-incrementing unique identifier
    title: str                 # Required (1-200 characters)
    description: str = ""      # Optional (max 1000 characters)
    completed: bool = False    # Completion status
    created_at: datetime       # Automatic timestamp
    updated_at: datetime       # Update timestamp
```

### Application Usage

The application provides a fully interactive menu-driven interface:

- Run with: `python todo_apps/main.py` or `uv run main.py`
- Features include:
  - Add tasks with title, description, priority, tags, and due dates
  - View/filter/sort tasks by multiple criteria
  - Mark tasks as completed
  - Update and delete tasks
  - Search by keywords and tags
  - View statistics and completion rates

## Development Workflow

### Phase Pipeline

1. **Constitution** → Project principles and constraints (this document)
2. **Specify** → Feature specifications with user stories (`.specify/specs/`)
3. **Plan** → Implementation plans with technical decisions (`.specify/specs/`)
4. **Tasks** → Executable task list with test cases (`.specify/specs/`)
5. **Implement** → Red-Green-Refactor development cycle

### Quality Gates

All code changes MUST:
- Pass linting (flake8, isort, black)
- Pass type checking (mypy)
- Have 100% test coverage for new code
- Include docstrings for all public APIs
- Reference specification in commit messages

### Code Review Requirements

- Self-review before commit
- Verify spec compliance
- Check for anti-patterns
- Confirm error handling completeness

## Governance

This constitution supersedes all other development practices. Amendments require documentation of changes and rationale. Version increments follow Semantic Versioning:

- **MAJOR**: Backward incompatible principle changes
- **MINOR**: New principles or expanded guidance
- **PATCH**: Clarifications and wording fixes

All team members MUST verify compliance with these principles in every pull request.

**Version**: 1.0.0 | **Ratified**: 2025-12-29 | **Last Amended**: 2025-12-29
