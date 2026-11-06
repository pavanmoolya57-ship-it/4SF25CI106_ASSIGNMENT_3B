# NumPy and Pandas Assignment

This project contains a Jupyter Notebook with practical NumPy and Pandas
examples. The notebook builds small reproducible DataFrames and demonstrates
calculation, aggregation, missing-value handling, grouping, merging,
hierarchical indexes, row/column transformations, and string operations.

## Project file

```text
project.ipynb/
└── projectt1.ipynb/
    └── projectpandasnumpy.ipynb
```

- `projectpandasnumpy.ipynb` contains the complete assignment.
- The notebook uses generated data, so no external CSV or database is
  required.

## Requirements

- Python 3.10 or later
- Jupyter Notebook, JupyterLab, or Visual Studio Code with the Jupyter
  extension
- NumPy
- Pandas

## Setup

Create a virtual environment from the repository root:

```bash
python -m venv .venv
```

Activate it on Windows PowerShell:

```powershell
.venv\Scripts\Activate.ps1
```

Activate it on Windows Command Prompt:

```bat
.venv\Scripts\activate.bat
```

Activate it on macOS or Linux:

```bash
source .venv/bin/activate
```

Install the dependencies:

```bash
python -m pip install --upgrade pip
python -m pip install numpy pandas jupyter
```

## Run the notebook

From the repository root, start Jupyter:

```bash
jupyter notebook
```

Open:

```text
project.ipynb/projectt1.ipynb/projectpandasnumpy.ipynb
```

Alternatively, open the repository in Visual Studio Code, select the virtual
environment as the notebook kernel, and run the cells from top to bottom.

All random examples use fixed NumPy seeds, so the generated values and
displayed results are reproducible.

## Notebook walkthrough

### Imports

The first cell imports:

```python
import numpy as np
import pandas as pd
```

NumPy is used to generate arrays and random values. Pandas is used to create
and manipulate Series and DataFrames.

### Task 1: Create a calculated DataFrame column

The notebook creates a 5-row DataFrame with columns `A`, `B`, and `C`.
`Product_AB` is then calculated by multiplying columns `A` and `B`:

```python
df1["Product_AB"] = df1["A"] * df1["B"]
```

This demonstrates vectorized column arithmetic in Pandas.

### Task 2: Column-wise and row-wise sums

The notebook creates a DataFrame with columns `X`, `Y`, and `Z`, then
calculates:

- Column totals with `df2.sum(axis=0)`
- Row totals with `df2.sum(axis=1)`

The `axis` argument controls whether the operation is performed vertically
by column or horizontally by row.

### Task 3: Mean imputation for missing values

Two values are replaced with `NaN` in a numeric DataFrame. The notebook fills
each missing value with the mean of its column:

```python
df3_imputed = df3.fillna(df3.mean())
```

This is a simple mean-imputation technique for numeric data.

### Task 4: Remove rows containing null values

Another DataFrame receives two missing values. The notebook removes every row
containing at least one missing value:

```python
df4_cleaned = df4.dropna()
```

Unlike Task 3, this task discards incomplete rows instead of replacing their
values.

### Task 5: Grouped summary statistics

The notebook creates category and value columns, then groups the data by
`Category`. It calculates both the sum and mean of `Value`:

```python
grouped5 = df5.groupby("Category")["Value"].agg(["sum", "mean"])
```

The result provides category-level summary statistics.

### Task 6: Total sales by category

A product sales DataFrame is grouped by `Category`. The sales for each
category are added and converted back to a regular DataFrame with
`reset_index()`:

```python
total_sales = df6.groupby("Category")["Sales"].sum().reset_index()
```

### Task 7: Merge two DataFrames

Two DataFrames contain related employee information. One contains employee
names and the other contains departments. They are combined using the shared
`Employee_ID` key:

```python
merged_df = pd.merge(df7_a, df7_b, on="Employee_ID")
```

This demonstrates an inner merge based on a common identifier.

### Task 8: Create and slice a MultiIndex

The notebook creates a two-level index containing class and student names.
It then selects the records belonging to `Class_A`:

```python
df8.loc["Class_A"]
```

This demonstrates hierarchical indexing and label-based selection.

### Task 9: Group data by MultiIndex levels

The notebook creates a MultiIndex from category and subcategory combinations.
It groups by both index levels and sums `Units_Sold`:

```python
sum_result = df9.groupby(
    level=["Category", "SubCategory"]
).sum()
```

This is useful for summarized data that is already organized by multiple
index dimensions.

### Task 10: Apply a function to every DataFrame value

The notebook creates a numeric DataFrame and doubles every value using
`DataFrame.apply()` with a lambda function:

```python
doubled_df = df10.apply(lambda val: val * 2)
```

This demonstrates applying an element-wise transformation to numeric data.

### Task 11: Calculate a custom row total

The notebook creates three numeric columns and calculates a `Row_Sum` column
from the values in each row:

```python
df11["Row_Sum"] = df11.apply(
    lambda row: row["Num1"] + row["Num2"] + row["Num3"],
    axis=1
)
```

Using `axis=1` passes each row to the function.

### Task 12: Convert text to uppercase

The notebook creates a Pandas Series of words and uses the string accessor to
convert every value to uppercase:

```python
upper_series = text_series12.str.upper()
```

Pandas string accessors provide vectorized text operations without an
explicit loop.

### Task 13: Extract the first three characters

The final task slices each string and keeps its first three characters:

```python
extracted_series = text_series13.str[:3]
```

This demonstrates vectorized substring extraction with the `.str` accessor.

## Concepts demonstrated

- NumPy random number generation with reproducible seeds
- DataFrame and Series creation
- Vectorized arithmetic
- Row and column aggregation
- Missing-value imputation with column means
- Missing-row removal
- `groupby()` and multiple aggregation functions
- DataFrame merging
- MultiIndex creation, slicing, and grouping
- `apply()` and lambda functions
- Vectorized string transformations

## Troubleshooting

### `ModuleNotFoundError: No module named 'numpy'`

Activate the virtual environment and install the dependencies:

```bash
python -m pip install numpy pandas jupyter
```

### The notebook does not show the expected values

Run all cells from the beginning in order. The notebook defines variables in
earlier cells, and each cell uses the DataFrames created before it.

### The notebook kernel is unavailable

Install Jupyter in the selected Python environment, then select that same
environment as the notebook kernel:

```bash
python -m pip install jupyter
```

### Results differ after editing the notebook

Do not remove or change the `np.random.seed(...)` calls if reproducible output
is required. Each seed controls the generated values for its task.

## Reproducibility

The notebook is self-contained and does not require network access, API keys,
or external data files. Run it in a fresh kernel from top to bottom to
reproduce the included examples and outputs.
