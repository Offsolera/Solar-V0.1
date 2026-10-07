# Solar Agent - Autonomous AI Company

Solar is an AI-native operating system that turns goals into autonomous execution.

## Overview

Solar Agent implements an autonomous AI organization with:

- **Manager Agent** - Orchestrates missions, creates workers, assigns tasks, synthesizes results
- **Researcher Agent** - Performs web research and information gathering
- **Developer Agent** - Writes, modifies, and tests code in a sandboxed environment
- **Task Graph** - Manages task dependencies and parallel execution
- **Parallel Runner** - Executes tasks concurrently with resource limits
- **SQLite Persistence** - Survives restarts without losing mission state
- **Permission System** - Granular permissions per agent role

## Architecture

```
┌─────────────────────────────────────┐
│           Manager Agent             │          
│  (Mission → Tasks → Workers)        │
└──────────────┬──────────────────────┘
               │
     ┌─────────┴─────────┐
     ▼                   ▼
┌─────────┐         ┌─────────┐
│Researcher│         │Developer│
│ Agent   │         │ Agent   │
└────┬────┘         └────┬────┘
     │                   │
     ▼                   ▼
┌─────────┐         ┌─────────┐
│ Web     │         │ Sandbox │
│ Research│         │ (Code)  │
└─────────┘         └─────────┘
Human
  ↓
Mission
  ↓
Solar Core
  ↓
Planning
  ↓
Dynamic AI Workforce
  ↓
Tools + Memory
  ↓
Execution
  ↓
Evaluation
  ↓
Learning
  ↺
```

## Installation

```bash
cd solar-agent
pip install -e ".[dev]"
```

## Quick Start

```bash
# Initialize database
solar-agent init

# Run a research mission
solar-agent mission "Research 5 legitimate software business opportunities"

# List missions
solar-agent list-missions

# Show mission details
solar-agent show-mission <mission-id>
```

## Configuration

Environment variables (or `.env` file):

```bash
DATABASE_PATH=data/solar_agent.db
MAX_ACTIVE_AGENTS=10
MAX_AGENT_DEPTH=3
MAX_TASKS=300
MAX_RUNTIME_SECONDS=5900
LLM_PROVIDER=mock  # or openai, anthropic
LLM_MODEL=gpt-4o-mini
WEB_SEARCH_ENABLED=true
SANDBOX_ENABLED=true
LOG_LEVEL=INFO
```

## Agent Roles & Permissions

| Role | Permissions |
|------|-------------|
| Manager | web_research, file_read, file_write, db_read, db_write |
| Researcher | web_research, file_read, file_write |
| Developer | file_read, file_write, code_execution, terminal_access, db_read, db_write |
| Marketing | web_research, file_read, file_write, external_api |
| Sales | web_research, file_read, file_write, external_api |
| Analyst | web_research, file_read, file_write, db_read, db_write |
| QA | file_read, code_execution, terminal_access |
| Security | file_read, db_read, security_settings |

## Project Structure

```
solar-agent/
├── src/solar_agent/
│   ├── config/          # Settings & configuration
│   ├── memory/          # SQLite models & database
│   ├── agents/          # Agent implementations
│   │   ├── base.py      # Base agent class
│   │   ├── manager.py   # Manager agent
│   │   ├── researcher.py # Researcher agent
│   │   └── developer.py # Developer agent
│   ├── orchestration/   # Task graph & parallel runner
│   ├── permissions/     # Permission system
│   ├── tools/           # Web research, sandbox, registry
│   └── cli.py           # CLI entry point
├── tests/               # Test suite
├── pyproject.toml       # Project config
└── README.md
```

## Development

```bash
# Run tests
pytest

# Run with coverage
pytest --cov=solar_agent

# Lint
ruff check src/

# Type check
mypy src/
```

## First Milestone Test

The system can execute:

> "Research five legitimate software business opportunities and identify the strongest opportunity based on demand, competition, complexity, and potential revenue."

The Manager will:
1. Create multiple research workers
2. Give each worker a research assignment
3. Run independent research tasks concurrently
4. Collect results
5. Evaluate the results
6. Produce a final ranked report

## Safety Features

- **Resource Limits**: Configurable max agents, depth, tasks, runtime
- **Permissions**: Role-based access control
- **Human Approval**: Required for sensitive operations
- **Sandboxing**: Code execution isolated from host
- **Observability**: Structured logging of all actions

## License

MIT
