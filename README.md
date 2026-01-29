# Euro 2024 Goal Timing Analysis (SQL + Python)

This project analyzes when goals occur during Euro 2024 matches using a combination of Python (Pandas) and SQL (SQLite). Starting from raw event‑level match data, the workflow demonstrates how to profile a dataset, engineer time‑based features, and use SQL to uncover patterns in scoring behavior across different phases of a match.

The project was inspired by a DataCamp DataLab walkthrough and extended to run locally with SQLite while adding additional feature engineering and analysis logic.

---

## Project Objectives

* Load and profile raw soccer event data from CSV files
* Engineer match‑time features such as formatted minutes, stoppage time labels, and time buckets
* Use SQL aggregations to analyze goal frequency across different game periods
* Demonstrate practical SQL skills including CTEs, CASE statements, grouping, and sorting
* Showcase how Python and SQL can be combined in a modern analytics workflow

---

## Tech Stack

* Python
* Pandas
* SQLite
* Jupyter Notebook
* ipython‑sql

---

## Dataset

The dataset contains event‑level records from Euro 2024 matches. Each row represents an in‑game event (pass, foul, goal, substitution, etc.) with attributes such as:

* match / fixture identifiers
* team and player information
* event type
* minute and extra minute
* additional metadata depending on event type

Only events where `event_type = 'Goal'` are used for the main analysis.

---

## Workflow Overview

### 1. Data Profiling (Python)

The dataset is first explored using Pandas to understand:

* column types
* missing values
* basic summary statistics
* data ranges and distributions

This step ensures the data is clean and logically consistent before SQL analysis.

---

### 2. Load Data into SQLite

The cleaned DataFrame is written into a local SQLite database using `to_sql`, creating a table called `game_events`.

---

### 3. Feature Engineering in SQL

A new table called `goals` is created using a Common Table Expression (CTE). Additional columns are engineered directly in SQL:

* **minute_str_sortable** – space‑padded minute value for clean sorting and display
* **game_minute** – formatted match time (e.g., `45 + 2`)
* **game_period_bucket** – 5‑minute buckets (e.g., `05`, `10`, `15`, …), stoppage‑time buckets, and extra‑time labels

This allows temporal analysis without modifying the original dataset.

---

### 4. Analytical Queries

Key SQL queries include:

* Goals per minute
* Goals by event type
* Goals by 5‑minute time bucket
* Late‑game vs stoppage‑time scoring frequency

Example aggregation:

* Count of goals per `game_period_bucket`
* Sorting by frequency or chronological order

---

## Example SQL Logic Used

* Common Table Expressions (CTEs)
* CASE statements
* Aggregations (`COUNT`)
* String formatting with `printf`
* Conditional time bucketing
* Table creation from query results

---

## Key Insights

* Goal frequency increases in the later stages of matches
* Stoppage time contributes a meaningful share of total goals
* Time bucketing makes match‑flow trends easier to visualize and analyze

These patterns align with known match dynamics such as fatigue, tactical risk‑taking, and increased pressure late in games.

---

## How to Run Locally

1. Install dependencies:

```bash
pip install pandas sqlalchemy ipython-sql
```

2. Open the notebook:

```bash
jupyter notebook EUROS-2024.ipynb
```

3. Run all cells in order:

* Load CSV files
* Profile with Pandas
* Write to SQLite
* Execute SQL analysis

---

## Project Structure

```
EUROS-2024.ipynb
README.md
/game_events.csv
/goals.csv (optional export)
```

---

## Conclusion

This project demonstrates how SQL can be used to transform raw event‑level soccer data into structured analytical insights. By combining Pandas for data profiling with SQLite for feature engineering and aggregation, the analysis highlights how scoring behavior changes across different phases of a match.

Beyond soccer analytics, the techniques used here generalize to many real‑world data problems involving timestamped events, categorical grouping, and feature engineering directly in SQL. The project showcases practical skills in writing clean analytical queries, designing derived tables, and building reproducible data workflows.

---

## Acknowledgments

Project inspiration:

DataCamp DataLab – Euro 2024 event analysis walkthrough

---

## Author

Justin Starks
Finance + Data Science | Analytics & Engineering Portfolio

---

If you have questions or suggestions, feel free to reach out or open an issue.
