# COVID-19 ETL Pipeline

A simple end-to-end ETL (Extract → Transform → Load) pipeline that downloads public COVID-19 data, cleans and processes it, and loads it into a SQLite database.  
You can clone this repo, run the scripts, and instantly reproduce the entire workflow.

---

## 🔍 Project Structure

```txt
covid19_ETL_pipeline/
├── .gitignore
├── README.md
├── scripts/
│   ├── covid_rawdata_fetching.ipynb   # Extract step
│   ├── Data_Cleaning.ipynb            # Transform step
│   └── data_loading.ipynb             # Load step
├── data/
│   ├── raw/       → Downloaded CSV (ignored by Git)
│   └── processed/ → Cleaned CSV (ignored by Git)
├── database/
│   └── covid19.db  → SQLite database (ignored by Git)
└── requirements.txt
```

---

## 🚀 Quickstart

1. **Clone this repository**  
   ```bash
   git clone https://github.com/akunuru03/covid19_ETL_pipeline.git
   cd covid19_ETL_pipeline
   ```

2. **Install dependencies**  
   ```bash
   pip install -r requirements.txt
   ```

3. **Run the ETL pipeline**  
   **In Jupyter**, open and execute each notebook in order:  
   - **Extract** data  
     `scripts/covid_rawdata_fetching.ipynb`  
   - **Transform** data  
     `scripts/Data_Cleaning.ipynb`  
   - **Load** into SQLite  
     `scripts/data_loading.ipynb`  

   **Or**, convert notebooks to Python scripts and run from the command line:  
   ```bash
   # Extract
   jupyter nbconvert --to script scripts/covid_rawdata_fetching.ipynb
   python scripts/covid_rawdata_fetching.py

   # Transform
   jupyter nbconvert --to script scripts/Data_Cleaning.ipynb
   python scripts/Data_Cleaning.py

   # Load
   jupyter nbconvert --to script scripts/data_loading.ipynb
   python scripts/data_loading.py
   ```

4. **Verify the database**  
   ```python
   import sqlite3, pandas as pd

   conn = sqlite3.connect("database/covid19.db")
   df = pd.read_sql(
       "SELECT location, date, total_cases, new_cases, total_deaths, active_cases FROM covid_data LIMIT 5;",
       conn
   )
   print(df)
   conn.close()
   ```

---

## 📦 What’s Inside

- **Extract**  
  - Downloads the latest COVID-19 CSV from Our World in Data  
  - Saves raw CSV to `data/raw/owid-covid-data.csv`

- **Transform**  
  - Reads raw CSV  
  - Filters to key columns: `location`, `date`, `total_cases`, `new_cases`, `total_deaths`  
  - Fills missing values, computes `active_cases`  
  - Writes cleaned CSV to `data/processed/cleaned_covid_data.csv`

- **Load**  
  - Creates `database/` folder  
  - Loads cleaned CSV into a SQLite table `covid_data` in `covid19.db`

- **.gitignore**  
  - Excludes `data/raw/`, `data/processed/`, `database/` and large `.csv`/`.db` files so your repo stays lean

---

## ⚙️ Requirements

Listed in `requirements.txt`:

```
pandas
requests
```

*(sqlite3 is part of Python’s standard library; no install needed)*

Install via:

```bash
pip install -r requirements.txt
```

---

## 🙋‍♂️ Author

**Aravind Kunuru**  
Data Analyst → Data Engineer  
[https://github.com/akunuru03](https://github.com/akunuru03)

