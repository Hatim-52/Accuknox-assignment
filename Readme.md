# AccuKnox Assignment 1 - Python + SQLite tasks

| File | Task |
|------|------|
| `q1books.py` | Fetch books from the Open Library REST API, store in SQLite, print them |
| `q2scores.py` | Load student scores (API or JSON file), compute the average, save a bar chart |
| `q3csvimport.py` | Import `name,email` rows from a CSV into SQLite |

## Run
```
pip install requests matplotlib
python q1_books.py --query "python programming" --limit 20
python q2_scores.py --url <scores-api-url>        # or --file sample_scores.json
python q3_csv_import.py sample_users.csv
```

## Assumptions
- Q1: Open Library (`openlibrary.org/search.json`) is the books API. It returns `title`, `author_name` and `first_publish_year`; "publication year" is taken as the first publish year. Missing authors are stored as "Unknown"; records without a title are skipped.
- Q1: `(title, author)` is UNIQUE, so re-running the script does not create duplicates.
- Q2: No specific scores API was given. The script expects JSON like `[{"name": "Asha", "score": 82}]` from any URL (or a local file with `--file`). Malformed records are skipped and reported.
- Q3: CSV has a header row with `name` and `email`. Emails are lower-cased and checked with a simple regex; duplicate emails and invalid rows are skipped, not fatal.
- All SQL uses parameterised queries. Network calls use a timeout and exit with a clear error on failure.