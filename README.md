# Netflix Data Cleaning & Analysis (SQL Server + Python)

An end-to-end ELT exercise on the public Netflix titles dataset: load raw data with Python, clean and model it in SQL Server, then answer business questions in SQL.

## Pipeline
1. **Load (Python)**: pandas + SQLAlchemy push `netflix_titles.csv` into SQL Server. Column lengths are profiled first so the target table uses tight `VARCHAR`/`NVARCHAR` sizes (NVARCHAR keeps non-English titles intact).
2. **De-duplicate**: titles repeated with the same type are removed with `ROW_NUMBER() OVER (PARTITION BY title, type)`.
3. **Normalise**: multi-value columns (director, cast, country, genre) are split into their own tables with `STRING_SPLIT` + `CROSS APPLY`.
4. **Fill gaps**: missing countries are filled from the same director's other titles, and missing durations that were shifted into `rating` are recovered.
5. **Type fixes**: `date_added` is cast to `DATE`. The clean result is saved as `netflix_f`.

## Questions answered
1. Directors who made both movies and TV shows, with counts of each
2. Country with the most comedy movies
3. For each year added, the director with the most movies
4. Average movie duration by genre
5. Directors who made both horror and comedy movies, with counts

## Tools
SQL Server (CTEs, window functions, `STRING_SPLIT`, `CROSS APPLY`, conditional aggregation) · Python (pandas, SQLAlchemy)

## Files
| File | What it is |
|---|---|
| `SQL Code.txt` | All cleaning and analysis queries |
| `Python Code.txt` | Load script and column profiling |
| `Netflix queries with output.pdf` | Queries with their results |
| `Netflix Data Analysis presentation.pptx` | Findings deck |
| `netflix dataset.csv` | Raw data |
