# dlt

`dlt` (short for [**data load tool**](https://dlthub.com/)) is a python library that is focused on the data integration layer of a data warehousing system (ie collecting data from some source in the world and getting it into a database so ETL | ELT can happen).

I'm currently interested in finding better tooling for connecting different data sources to my data warehouse, so I'll work through the walkthrough and see how easy it would be to use.

## Env setup

```bash
mkdir dlthub && cd dlthub
python -m venv .venv
source .venv/bin/activate
python -m pip install dlt
python -m pip install dlt[duckdb]
python -m pip install streamlit
```

## Quickest start

Following along the [Getting Started](https://dlthub.com/docs/getting-started) walkthrough, copy the first python codeblock into a file `quick_start_pipeline.py`, run the script, and then use start up a streamlit app to inspect the schema (in a browser).

```bash
python quick_start_pipeline.py
dlt pipeline quick_start show
``` 

### Loading more realistic data

The walkthrough provides code snippets to load data from JSON, from CSV (or anything that can be read into a `pandas` DataFrame), from a REST API, or from a database. I'll try the CSV and API modes.

