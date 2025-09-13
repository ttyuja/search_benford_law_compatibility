# `README.md`

# A Scalable Framework for Benford's Law Conformity Testing of Financial Data

<!-- PROJECT SHIELDS -->
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Python Version](https://img.shields.io/badge/python-3.9%2B-blue.svg)](https://www.python.org/downloads/)
[![Code style: black](https://img.shields.io/badge/code%20style-black-000000.svg)](https://github.com/psf/black)
[![Imports: isort](https://img.shields.io/badge/%20imports-isort-%231674b1?style=flat&labelColor=ef8336)](https://pycqa.github.io/isort/)
[![Type Checking: mypy](https://img.shields.io/badge/type_checking-mypy-blue)](http://mypy-lang.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-%23F37626.svg?style=flat&logo=Jupyter&logoColor=white)](https://jupyter.org/)
[![arXiv](https://img.shields.io/badge/arXiv-2509.09415-b31b1b.svg)](https://arxiv.org/abs/2509.09415)
[![Year](https://img.shields.io/badge/Year-2025-purple)](https://github.com/chirindaopensource/search_benford_law_compatibility)
[![Discipline](https://img.shields.io/badge/Discipline-Forensic%20Accounting%20%26%20Econometrics-blue)](https://github.com/chirindaopensource/search_benford_law_compatibility)
[![Methodology](https://img.shields.io/badge/Methodology-Benford's%20Law%20%7C%20Goodness--of--Fit-orange)](https://github.com/chirindaopensource/search_benford_law_compatibility)
[![Data Source](https://img.shields.io/badge/Data-Refinitiv%20EIKON-lightgrey)](https://www.refinitiv.com/en/products/eikon-trading-software)
[![Pandas](https://img.shields.io/badge/pandas-%23150458.svg?style=flat&logo=pandas&logoColor=white)](https://pandas.pydata.org/)
[![NumPy](https://img.shields.io/badge/numpy-%23013243.svg?style=flat&logo=numpy&logoColor=white)](https://numpy.org/)
[![SciPy](https://img.shields.io/badge/SciPy-%23025596?style=flat&logo=scipy&logoColor=white)](https://scipy.org/)
[![PyYAML](https://img.shields.io/badge/PyYAML-4B5F6E.svg?style=flat)](https://pyyaml.org/)

--

**Repository:** `https://github.com/chirindaopensource/search_benford_law_compatibility`

**Owner:** 2025 Craig Chirinda (Open Source Projects)

This repository contains an **independent**, professional-grade Python implementation of the research methodology from the 2025 paper entitled **"Note on pre-taxation reported data by UK FTSE-listed companies. A search for Benford's laws compatibility"** by:

*   Marcel Ausloos
*   Probowo Erawan Sastroredjo
*   Polina Khrennikova

The project provides a complete, end-to-end computational framework for testing the conformity of financial datasets with Benford's Law. It delivers a modular, auditable, and extensible pipeline that replicates the paper's entire workflow: from rigorous data and configuration validation, through robust, mathematically-grounded digit extraction, to the precise calculation of Chi-Squared and Mean Absolute Deviation (MAD) test statistics and the final generation of publication-quality results tables.

## Table of Contents

- [Introduction](#introduction)
- [Theoretical Background](#theoretical-background)
- [Features](#features)
- [Methodology Implemented](#methodology-implemented)
- [Core Components (Notebook Structure)](#core-components-notebook-structure)
- [Key Callable: execute_full_project_workflow](#key-callable-execute_full_project_workflow)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Input Data Structure](#input-data-structure)
- [Usage](#usage)
- [Output Structure](#output-structure)
- [Project Structure](#project-structure)
- [Customization](#customization)
- [Contributing](#contributing)
- [Recommended Extensions](#recommended-extensions)
- [License](#license)
- [Citation](#citation)
- [Acknowledgments](#acknowledgments)

## Introduction

This project provides a Python implementation of the methodologies presented in the 2025 paper "Note on pre-taxation reported data by UK FTSE-listed companies. A search for Benford's laws compatibility." The core of this repository is the iPython Notebook `search_benford_law_compatibility_draft.ipynb`, which contains a comprehensive suite of functions to replicate the paper's findings, from initial data validation to the final generation and analysis of conformity test results.

The paper addresses a classic problem in forensic accounting and auditing: using statistical laws to identify potential anomalies in reported financial data. This codebase operationalizes the paper's approach, allowing users to:
-   Rigorously validate input data and methodological parameters against a predefined schema.
-   Perform a detailed data quality audit, identifying outliers and missing value patterns without altering the source data.
-   Create derived analytical variables (e.g., PI/TA ratio) and segmented datasets (e.g., profitable vs. unprofitable firms).
-   Apply robust, mathematically-grounded algorithms to extract the first, second, and first-two significant digits from numerical data.
-   Calculate the theoretical probability distributions for Benford's Law (BL1, BL2, BL12) with high precision.
-   Execute Pearson's Chi-Squared (χ²) and Mean Absolute Deviation (MAD) goodness-of-fit tests to quantify deviations from the theoretical benchmarks.
-   Generate a full suite of publication-quality tables that precisely replicate the findings in the source paper.
-   Conduct a comprehensive series of robustness checks, including bootstrap resampling, parameter sensitivity analysis, and temporal stability analysis.

## Theoretical Background

The implemented methods are grounded in Probability Theory, Statistics, and Forensic Accounting.

**1. Benford's Law (The First-Digit Law):**
Benford's Law states that in many naturally occurring sets of numbers, the leading significant digit is more likely to be small. The probability of a first digit `d` is given by:
$$ P(d_1 = i) = \log_{10}\left(1 + \frac{1}{i}\right) \quad \text{for } i \in \{1, ..., 9\} $$
This principle extends to second and subsequent digits, as well as to blocks of digits, with specific logarithmic formulas. Deviations from these expected frequencies can suggest that a dataset was not naturally generated and may be the result of manipulation, fabrication, or systemic error.

**2. Chi-Squared (χ²) Goodness-of-Fit Test:**
This is a classical statistical test used to determine if there is a significant difference between observed and expected frequencies. The test statistic is calculated as:
$$ \chi^2 = \sum_{i=1}^{K} \frac{(O_i - E_i)^2}{E_i} $$
where `O` are the observed counts and `E` are the expected counts across `K` bins. A large χ² statistic suggests that the observed data does not fit the theoretical distribution.

**3. Mean Absolute Deviation (MAD) Test:**
The MAD test provides a direct measure of the magnitude of the deviation between the observed proportions (`fₒ`) and the expected proportions (`fₑ`). The paper uses the sum of absolute deviations:
$$ \text{MAD} = \sum_{i=1}^{K} |f_{o,i} - f_{e,i}| $$
This statistic is less sensitive to sample size than the χ² test and provides an intuitive measure of non-conformity, which is then compared against established thresholds.

## Features

The provided iPython Notebook (`search_benford_law_compatibility_draft.ipynb`) implements the full research pipeline, including:

-   **Modular, Task-Based Architecture:** The entire pipeline is broken down into 18 distinct, modular tasks, from data validation to final packaging.
-   **Configuration-Driven Design:** All methodological parameters are managed in an external `config.yaml` file, allowing for easy customization without code changes.
-   **Professional-Grade Data Validation:** A comprehensive validation suite ensures all inputs (data and configurations) conform to the required schema before execution.
-   **Robust, Mathematical Digit Extraction:** Numerically stable, from-scratch implementations of logarithmic algorithms for extracting significant digits, avoiding common pitfalls of string-based methods.
-   **High-Fidelity Statistical Testing:** Precise, vectorized implementations of the Chi-Squared and Mean Absolute Deviation tests.
-   **Automated Report Generation:** Programmatic generation of all 6 analytical tables (Tables 3-8) from the paper with high fidelity to the original formatting.
-   **Advanced Robustness Toolkit:**
    -   A framework for conducting **bootstrap resampling** to assess the stability of test statistics.
    -   A framework for **parameter sensitivity analysis** to test the impact of varying alpha levels and MAD thresholds.
    -   A framework for **temporal stability analysis** to check for consistency of results over time.
-   **Automated Replication Validation:** A final quality assurance step that programmatically compares the generated results against the paper's published statistics and produces a certification report.

## Methodology Implemented

The core analytical steps directly implement the methodology from the paper:

1.  **Validation (Tasks 1-3):** Ingests and rigorously validates the raw data and `config.yaml` file, and performs a detailed data quality audit.
2.  **Preprocessing (Tasks 4-6):** Prepares the data by flagging outliers, creating the PI/TA ratio, segmenting the data by profitability, and generating the summary statistics table (Table 1).
3.  **Digit Extraction (Tasks 7-9):** Applies robust mathematical algorithms to extract the first, second, and first-two significant digits for all relevant variables.
4.  **Theoretical Distribution Generation (Tasks 10-12):** Calculates the high-precision theoretical probabilities and expected frequencies for BL1, BL2, and BL12.
5.  **Statistical Testing & Reporting (Tasks 13-15):** Executes the Chi-Squared and MAD tests for all variable-digit combinations and compiles the results into replications of Tables 3-8.
6.  **Robustness & Packaging (Tasks 16-18):** Orchestrates the entire pipeline, runs the optional robustness checks, and performs the final validation and packaging of all outputs.

## Core Components (Notebook Structure)

The `search_benford_law_compatibility_draft.ipynb` notebook is structured as a logical pipeline with modular orchestrator functions for each of the major tasks. All functions are self-contained, fully documented with type hints and docstrings, and designed for professional-grade execution.

## Key Callable: execute_full_project_workflow

The central function in this project is `execute_full_project_workflow`. It orchestrates the entire analytical workflow, providing a single entry point for running the baseline study replication and the advanced robustness checks.

```python
def execute_full_project_workflow(
    raw_financial_data: pd.DataFrame,
    study_configuration: Dict[str, Any],
    output_directory: str,
    run_robustness_checks: bool = True
) -> Dict[str, Any]:
    """
    Executes the entire, end-to-end research project workflow.
    """
    # ... (implementation is in the notebook)
```

## Prerequisites

-   Python 3.9+
-   Core dependencies: `pandas`, `numpy`, `scipy`, `pyyaml`, `tqdm`.

## Installation

1.  **Clone the repository:**
    ```sh
    git clone https://github.com/chirindaopensource/search_benford_law_compatibility.git
    cd search_benford_law_compatibility
    ```

2.  **Create and activate a virtual environment (recommended):**
    ```sh
    python -m venv venv
    source venv/bin/activate  # On Windows, use `venv\Scripts\activate`
    ```

3.  **Install Python dependencies:**
    ```sh
    pip install pandas numpy scipy pyyaml tqdm
    ```

## Input Data Structure

The pipeline requires two primary inputs:
1.  **`raw_financial_data`:** A `pandas.DataFrame` containing the panel data. It **must** have a `MultiIndex` with the levels `['CompanyID', 'Year']` and the columns `['CompanyName', 'PreTaxIncome_GBP', 'TotalAssets_GBP']`. Financial columns must be `float64`.
2.  **`study_configuration`:** A Python dictionary loaded from the `config.yaml` file, which controls all methodological parameters.

A mock data generation function is provided in the main notebook to create a valid example DataFrame for testing the pipeline.

## Usage

The `search_benford_law_compatibility_draft.ipynb` notebook provides a complete, step-by-step guide. The core workflow is:

1.  **Prepare Inputs:** Load your `raw_financial_data` DataFrame. Ensure the `config.yaml` file is present in the same directory.
2.  **Execute Pipeline:** Call the grand orchestrator function.

    ```python
    # This single call runs the entire project.
    final_project_outputs = execute_full_project_workflow(
        raw_financial_data=my_company_data_df,
        study_configuration=my_config_dict,
        output_directory="research_outputs",
        run_robustness_checks=False  # Set to True for the full analysis
    )
    ```
3.  **Inspect Outputs:** All results are saved to the specified output directory. You can also programmatically access any result from the returned dictionary.

## Output Structure

The `execute_full_project_workflow` function returns a single, comprehensive dictionary containing all generated artifacts. Additionally, the `output_directory` will be populated with:
-   `replication_validation_report.json`: A report certifying the accuracy of the replication.
-   `data_quality_report.json`: A detailed audit of the input data quality.
-   `table_1_summary_statistics.csv`: The replicated descriptive statistics table.
-   `table_3_body.csv`, `table_3_stats.csv`, etc.: Pairs of CSV files for each analytical table (3-8).
-   `raw_test_results.json`: A comprehensive file with the detailed numerical outputs of all statistical tests.
-   `robustness_analysis_report.json`: (If run) A file with the results of all robustness checks.

## Project Structure

```
search_benford_law_compatibility/
│
├── search_benford_law_compatibility_draft.ipynb   # Main implementation notebook
├── config.yaml                                    # Master configuration file
├── requirements.txt                               # Python package dependencies
├── LICENSE                                        # MIT license file
└── README.md                                      # This documentation file
```

## Customization

The pipeline is highly customizable via the `config.yaml` file. Users can easily modify all methodological parameters, such as statistical thresholds, critical values, and bin definitions, without altering the core Python code.

## Contributing

Contributions are welcome. Please fork the repository, create a feature branch, and submit a pull request with a clear description of your changes. Adherence to PEP 8, type hinting, and comprehensive docstrings is required.

## Recommended Extensions

Future extensions could include:
-   **Additional Goodness-of-Fit Tests:** Implementing other statistical tests for Benford's Law conformity, such as the Kolmogorov-Smirnov test or Kuiper's test.
-   **Visualization Module:** Creating a function that takes the final results and generates plots of the observed vs. expected distributions, similar to Figures 2-4 in the paper.
-   **Automated Reporting:** Building a module that uses the generated tables and plots to automatically create a full PDF or HTML summary report of the findings.
-   **Integration with Database:** Developing a data ingestion module to pull data directly from a SQL database instead of a CSV file.

## License

This project is licensed under the MIT License. See the `LICENSE` file for details.

## Citation

If you use this code or the methodology in your research, please cite the original paper:

```bibtex
@article{ausloos2025note,
  title={{Note on pre-taxation reported data by UK FTSE-listed companies. A search for Benford's laws compatibility}},
  author={Ausloos, Marcel and Sastroredjo, Probowo Erawan and Khrennikova, Polina},
  journal={arXiv preprint arXiv:2509.09415},
  year={2025}
}
```

For the implementation itself, you may cite this repository:
```
Chirinda, C. (2025). A Python Implementation for Benford's Law Conformity Testing of Financial Data.
GitHub repository: https://github.com/chirindaopensource/search_benford_law_compatibility
```

## Acknowledgments

-   Credit to **Marcel Ausloos, Probowo Erawan Sastroredjo, and Polina Khrennikova** for their foundational research, which forms the entire basis for this computational replication.
-   This project is built upon the exceptional tools provided by the open-source community. Sincere thanks to the developers of the scientific Python ecosystem, including **Pandas, NumPy, SciPy, and PyYAML**, whose work makes complex computational analysis accessible and robust.

--

*This README was generated based on the structure and content of `search_benford_law_compatibility_draft.ipynb` and follows best practices for research software documentation.*
