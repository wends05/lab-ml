# AI Agent Instructions

## Project Overview

Machine Learning laboratory project using Jupyter notebooks for data analysis and model development.

- **Language**: Python 3.14
- **Package Manager**: uv
- **Environment**: Virtual environment at `.venv/`
- **Primary Format**: Jupyter notebooks (.ipynb)

## Build/Development Commands

```bash
# Install dependencies
uv sync

# Activate virtual environment
source .venv/bin/activate

# Run Jupyter notebook server
jupyter notebook

# Or using uv run
uv run jupyter notebook

# Install new package
uv add <package-name>

# Update lock file
uv lock
```

## Code Style Guidelines

### Python Code (in notebooks)

**Imports**: Group and order imports:
1. Standard library imports
2. Third-party imports (numpy, pandas, sklearn, matplotlib, seaborn)
3. Local imports (if any)

```python
# Standard library
import os
from pathlib import Path

# Third-party - data science stack
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
from sklearn.model_selection import train_test_split

# Configure plotting
%matplotlib inline
sns.set_style('whitegrid')
```

**Formatting**:
- Follow PEP 8 for code cells
- Use 4 spaces for indentation
- Maximum line length: 88 characters (Black-compatible)
- Use type hints where practical

**Naming Conventions**:
- Variables/functions: `snake_case`
- Constants: `UPPER_SNAKE_CASE`
- Classes: `PascalCase`
- Private: `_leading_underscore`
- DataFrames: descriptive names like `df_raw`, `df_processed`, `df_train`
- Models: `model`, `clf`, `regressor` with version suffixes if needed

**Notebook Organization**:
```markdown
# 1. Imports and Setup
# 2. Data Loading
# 3. Exploratory Data Analysis (EDA)
# 4. Data Preprocessing
# 5. Model Training
# 6. Evaluation
# 7. Results/Visualization
```

**Error Handling**:
- Use try/except for file operations and external API calls
- Validate data shapes and types after transformations
- Check for missing values explicitly

```python
# Good pattern
try:
    df = pd.read_csv('data.csv')
    assert not df.empty, "Dataset is empty"
except FileNotFoundError:
    print("Error: data.csv not found")
```

**ML-Specific Guidelines**:
- Always set `random_state` for reproducibility
- **Train/Test Split**: Use 80/20 ratio (80% train, 20% test) with `shuffle=True` to prevent data order memorization
- Split data before any preprocessing that learns from data
- Document feature engineering decisions in markdown cells
- Save model artifacts with version numbers
- Include data validation checks

```python
# Good train/test split pattern
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42, shuffle=True
)
```

**Cell Structure**:
- One concept per code cell
- Use markdown cells to explain analysis steps
- Keep outputs clean (clear unnecessary warnings)
- Restart kernel and run all cells before committing

## File Organization

```
lab-ml/
├── lab_1/              # Lab 1 notebooks
├── lab_2/              # Lab 2 notebooks  
├── lab_3/              # Lab 3 notebooks
├── *.ipynb             # Main notebooks
├── *.csv               # Datasets (tracked if small)
├── pyproject.toml      # Dependencies
├── uv.lock            # Lock file
└── .venv/             # Virtual environment (gitignored)
```

## Best Practices

1. **Reproducibility**: Set random seeds, document package versions
2. **Data**: Never modify raw data in-place; create processed copies
3. **Memory**: Clean up large variables when done (`del large_df`)
4. **Git**: Clear cell outputs before committing large notebooks
5. **Paths**: Use relative paths from notebook location
6. **Documentation**: Every analysis step should have explanatory markdown

## No Formal Test Suite

This project uses Jupyter notebooks for experimentation rather than a formal test suite. Validate code by:
- Running all cells sequentially
- Checking for errors or warnings
- Verifying output shapes and values
- Reviewing visualizations for correctness
