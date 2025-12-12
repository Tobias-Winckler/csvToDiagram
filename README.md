# csvToMermaidGantt

A Python CLI tool that converts CSV files to Mermaid Gantt charts.

## Features

- Convert CSV files to Mermaid Gantt chart syntax
- Support for task names, start dates, durations/end dates, and status
- CLI interface with stdin/stdout support
- 100% test coverage
- Type-checked with mypy
- Linted with flake8
- Formatted with black

## Installation

```bash
pip install -e .
```

For development:

```bash
pip install -e ".[dev]"
```

## Usage

### Basic usage with file input

```bash
csv-to-mermaid-gantt input.csv
```

### With custom title

```bash
csv-to-mermaid-gantt input.csv -t "My Project Timeline"
```

### Output to file

```bash
csv-to-mermaid-gantt input.csv -o output.md
```

### Using stdin/stdout

```bash
cat input.csv | csv-to-mermaid-gantt > output.md
```

### As a Python module

```python
from csv_to_mermaid_gantt import convert_csv_to_mermaid

csv_content = """task_name,start_date,duration,status
Planning,2024-01-01,5d,done
Development,2024-01-06,10d,active"""

mermaid_output = convert_csv_to_mermaid(csv_content, title="My Project")
print(mermaid_output)
```

## CSV Format

The tool expects CSV files with the following columns:

- `task_name` (required): The name of the task
- `start_date` (optional): Start date in YYYY-MM-DD format
- `duration` or `end_date` (optional): Duration (e.g., "5d") or end date (YYYY-MM-DD)
- `status` (optional): Task status - `active`, `done`, or `crit` (critical)

### Example CSV

```csv
task_name,start_date,duration,status
Planning Phase,2024-01-01,5d,done
Design Phase,2024-01-06,7d,active
Development,2024-01-13,14d,
Testing,2024-01-27,7d,
Deployment,2024-02-03,2d,crit
```

### Example Output

```mermaid
gantt
    title Gantt Chart
    dateFormat YYYY-MM-DD
    Planning Phase :planning_phase, done, 2024-01-01, 5d
    Design Phase :design_phase, active, 2024-01-06, 7d
    Development :development, 2024-01-13, 14d
    Testing :testing, 2024-01-27, 7d
    Deployment :deployment, crit, 2024-02-03, 2d
```

## Development

### Running Tests

```bash
pytest
```

### Running Tests with Coverage

```bash
pytest --cov=csv_to_mermaid_gantt --cov-report=term-missing
```

### Type Checking

```bash
mypy csv_to_mermaid_gantt.py tests/
```

### Linting

```bash
flake8 csv_to_mermaid_gantt.py tests/
```

### Formatting

```bash
black csv_to_mermaid_gantt.py tests/
```

### Run All Checks

```bash
# Format code
black csv_to_mermaid_gantt.py tests/

# Lint
flake8 csv_to_mermaid_gantt.py tests/

# Type check
mypy csv_to_mermaid_gantt.py tests/

# Test with coverage
pytest --cov=csv_to_mermaid_gantt --cov-report=term-missing --cov-fail-under=100
```

## License

This project maintains 100% test coverage and follows strict code quality standards using pytest-cov, mypy, flake8, and black formatter.
