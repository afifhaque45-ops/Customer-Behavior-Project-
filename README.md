# Customer Shopping Behavior Analysis

📊 **Overview**

This repository contains a Jupyter notebook and dataset for analyzing customer shopping behavior. The intent is to clean the data, explore purchase patterns, and export the processed dataset to a SQL Server for reporting or downstream analytics.

---

## Files in this repository

- `CustomerBehaviorAnalysis.ipynb` — Jupyter notebook containing the data-cleaning, transformations, and SQL export steps.
- `customer_shopping_behavior.csv` — Source dataset with shopping behavior and customer attributes.
- `customer_behavior.sql` — (Optional) SQL file for schema or query examples used in analysis and reporting.

---

## Key Notebook Steps

The notebook performs the following high-level tasks:

- Import the dataset and standard Python libraries (pandas, numpy, SQLAlchemy).
- Inspect data with `df.info()` and `df.head()`.
- Fill missing review ratings using the median by `Category`.
- Normalize and rename column names (lowercase, underscores).
- Create derived features (e.g., `age_group`, `purchase_frequency_days`).
- Remove redundant columns when applicable (e.g., drop `promo_code_used` if identical to `discount_applied`).
- Configure a SQL Server connection using SQLAlchemy and write the DataFrame to a SQL table.

---

## Setup & Dependencies ✅

This project assumes you have Python installed (recommended: Python 3.9+). To set up a Python virtual environment and install dependencies (Windows PowerShell):

```powershell
cd "<Folder_Path>"
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
pip install -r requirements.txt
```

Alternatively, if you prefer conda:

```powershell
conda create -n cb_analysis python=3.9 -y
conda activate cb_analysis
pip install -r requirements.txt
```

---

## Running the Notebook 🧪

1. Start Jupyter and open the notebook:

```powershell
jupyter notebook
```

2. Click on `CustomerBehaviorAnalysis.ipynb` and run each cell in order. This will load `customer_shopping_behavior.csv` (which should be kept in the same folder), run cleaning steps, and optionally export the final DataFrame to a SQL Server.

---

## Database Export (Azure SQL / SQL Server) 🔌

The notebook contains a section that shows how to set up a SQL Server connection and write to a table. It uses SQLAlchemy with a PyODBC connection string.

Important:

- Replace the placeholders in the notebook's connection block with your actual server, database, username, and password. Do not commit secrets to the repository.
- Ensure the correct ODBC driver is installed. The notebook references `ODBC Driver 17 for SQL Server` by default.

A recommended best practice is to use environment variables rather than hardcoding credentials. Example (PowerShell):

```powershell
$env:DB_SERVER = "tcp:your_server.database.windows.net,1433"
$env:DB_NAME = "your_database"
$env:DB_USER = "your_user"
$env:DB_PWD = "your_password"
```

Then update the notebook's connection-building code to read from `os.environ`.

---

## Scripts & Automation

If you'd rather run the data pipeline as a script (outside of Jupyter), convert the notebook to a Python script or write a short runner that:

- Loads the CSV
- Performs the same cleaning steps
- Writes the output to SQL

Example to convert and run:

```powershell
jupyter nbconvert --to script CustomerBehaviorAnalysis.ipynb
python CustomerBehaviorAnalysis.py
```

---

## Notes & Caveats ⚠️

- The notebook contains a database export step: ensure that you have access to the target database and the network/credentials required.
- The CSV provided in the repository contains all the sample data required to reproduce the notebook's analysis.
- The code uses `median()` to impute missing review ratings by `Category`. Consider other methods if the distribution is skewed or if you want to preserve variance.

---

## Contributing & Improvements 🙌

If you'd like to improve this repo:

- Add more robust EDA (visualizations, correlation heatmaps).
- Implement unit tests for data-cleaning functions.
- Add more descriptive SQL queries or sample schema in `customer_behavior.sql`.
- Provide a script and wrapper for safer database writes (e.g., use transactions, upsert safeguards).

---

## License

This repo doesn't include a license file. If you plan to share, add a `LICENSE` (e.g., MIT) to make usage terms explicit.

---


