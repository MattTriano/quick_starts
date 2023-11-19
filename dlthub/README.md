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

# Quickest start

Following along the [Getting Started](https://dlthub.com/docs/getting-started) walkthrough, copy the first python codeblock into a file `quick_start_pipeline.py`, run the script, and then use start up a streamlit app to inspect the schema (in a browser).

```bash
python quick_start_pipeline.py
dlt pipeline quick_start show
``` 

## Loading more realistic data

The walkthrough provides code snippets to load data from JSON, from CSV (or anything that can be read into a `pandas` DataFrame), from a REST API, or from a database. I'll try the CSV and API modes.

### API example

I copied the API sample code into a file `from_api_pipeline.py` and ran

```bash
python from_api_pipeline.py
dbt pipeline from_api show
```

Looking at the streamlit app, I see two main views: **Explore data** and **Load info**

#### Explore data view
Includes column info (`name`, `data_type`, and `nullable`) on all tables in the one schema (`from_api`).

There is also a **SHOW DATA** button with every table that reveals rows of raw data. It's not clear if this will show all rows or just a sample. Looking at the data, I see that `dlt` adds on columns `_dlt_load_id` and `_dlt_id`.

From this (and a check of their [glossary](https://dlthub.com/docs/general-usage/glossary#schema)), I infer they use **schema** to mean the structure of the data model in the database.

#### Load data view
**Pipeline metadata**
* pipeline name (`from_api`)
* destination location (the path to the duckdb database file, I'm not sure what it would look like in other situations)
* dataset name (`github_data`)
* default schema name (`from_api`)
* all schema names (only `from_api` here)

**Last load info**
* last load time (with `load_id` and number of loads)
Also provides an interface where you can select a `load_id` and see:
* the number of rows loaded
* the datetime of that load

**Schema updates**
Shows "100 recent schema updates"
This includes the schema name, insertion time, schema version, and version_hash.

I'm not sure where that version info came from (it's currently showing `version` 3 for the only schema ingestion, so I assume that's a field that was in the API response)

### CSV/Pandas example

I followed the same pattern, copied the sample code into `from_csv_pipeline.py` and ran

```bash
python from_csv_pipeline.py
dbt pipeline from_csv show
```

and explored.

## Subsequent Runs

Rerunning either of those scripts will append data onto the respective tables, but we have two other kinds of update modes we can select via the `write_disposition` kwarg of the  `pipeline.run()` call. Valid mode labels:
* `"append"` (default; appends all records to the table)
* `"replace"` (full load)
* `"merge"` (incremental updates)

