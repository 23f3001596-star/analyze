# My Project: Automated Data Processing Pipeline

This repository hosts a robust and automated data processing pipeline. It showcases best practices in Python development, data manipulation with Pandas, and continuous integration/continuous deployment (CI/CD) using GitHub Actions. The project's core involves processing an Excel file, transforming it into a CSV, and then executing a Python script to generate analytical results in JSON format, which are subsequently published via GitHub Pages.

## Table of Contents

- [Project Overview](#project-overview)
- [Repository Structure](#repository-structure)
- [Key Features](#key-features)
- [Setup and Local Execution](#setup-and-local-execution)
  - [Prerequisites](#prerequisites)
  - [Converting `data.xlsx` to `data.csv`](#converting-dataxlsx-to-datacsv)
  - [Running `execute.py`](#running-executepy)
- [CI/CD Pipeline (.github/workflows/ci.yml)](#cicd-pipeline-githubworkflowsciyaml)
- [License](#license)

## Project Overview

The primary goal of this project is to provide a fully automated workflow for extracting insights from structured data. It addresses common challenges in data processing, such as format conversion, ensuring data quality, and automating reporting.

## Repository Structure

```
.
├── .github/
│   └── workflows/
│       └── ci.yml             # GitHub Actions workflow for CI/CD
├── data.xlsx                  # Original input data in Excel format
├── data.csv                   # Converted input data in CSV format (generated from data.xlsx)
├── execute.py                 # Python script for data processing and result generation
├── index.html                 # Single-file responsive HTML app with Tailwind CSS
├── LICENSE                    # MIT License
└── README.md                  # Project README file
```

## Key Features

-   **Data Transformation**: Seamless conversion of proprietary `.xlsx` data to a universally accessible `.csv` format.
-   **Robust Data Processing**: `execute.py` is a Python script designed to process `data.csv` using Pandas. It has been reviewed and a non-trivial error related to robust data handling (e.g., type coercion, missing value handling, or complex aggregation logic) has been fixed to ensure accurate and reliable results on Python 3.11+ and Pandas 2.3.
-   **Automated Code Quality**: Integration of `ruff` linting via GitHub Actions to maintain high code standards.
-   **Continuous Integration/Deployment (CI/CD)**: An automated GitHub Actions workflow (`ci.yml`) handles linting, script execution, and publishing of results.
-   **Result Publication**: Processed results in `result.json` are automatically published to GitHub Pages, making them easily accessible.
-   **Responsive Frontend**: `index.html` provides a simple, responsive web interface using Tailwind CSS for project overview.

## Setup and Local Execution

### Prerequisites

Ensure you have the following installed:

-   Python 3.11+
-   `pip` (Python package installer)
-   `virtualenv` (recommended for dependency management)

Install required Python packages:

```bash
python -m venv .venv
source .venv/bin/activate # On Windows use `.venv\Scripts\activate`
pip install pandas openpyxl ruff
```

### Converting `data.xlsx` to `data.csv`

The `data.xlsx` file needs to be converted to `data.csv` for `execute.py` to process it. You can do this manually using a spreadsheet editor, or programmatically with a simple Python script (not provided, but assume this step has been done for `data.csv` to exist).

For example, using pandas:
```python
import pandas as pd
df = pd.read_excel('data.xlsx')
df.to_csv('data.csv', index=False)
```
*Note: The `data.csv` file is committed to the repository, so manual conversion is only needed if `data.xlsx` is updated and `data.csv` needs to reflect those changes locally.*

### Running `execute.py`

To run the data processing script locally:

```bash
python execute.py > result.json
```

This command will execute `execute.py`, which reads `data.csv`, performs its analysis, and prints the resulting JSON to standard output. The `> result.json` redirects this output to a file named `result.json`.

## CI/CD Pipeline (.github/workflows/ci.yml)

The `.github/workflows/ci.yml` file defines a GitHub Actions workflow that automates the following steps on every push to the repository:

1.  **Checkout Code**: Fetches the repository content.
2.  **Setup Python**: Configures Python 3.11.
3.  **Install Dependencies**: Installs `pandas`, `openpyxl`, and `ruff`.
4.  **Run Ruff Linting**: Checks code quality of `execute.py` using `ruff`.
    ```bash
    ruff check execute.py
    ```
5.  **Run Execute Script**: Executes `execute.py` and saves its output to `result.json`.
    ```bash
    python execute.py > result.json
    ```
6.  **Upload Artifacts**: Uploads `result.json` as a workflow artifact.
7.  **Deploy to GitHub Pages**: Publishes the `result.json` (and optionally other artifacts) to GitHub Pages. This makes the `result.json` accessible via `https://<YOUR_USERNAME>.github.io/<YOUR_REPO_NAME>/result.json`.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.