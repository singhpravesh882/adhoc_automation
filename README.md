
# Import Libraries #
import pandas as pd

import os

pip install pandas openpyxl


# CONFIGURATION #

## Path to input Excel file containing IDs
INPUT_EXCEL = "input_ids.xlsx"

## Column name in the input file that contains IDs
INPUT_COLUMN = "Customer_Number"

## Number of IDs per SQL IN clause
CHUNK_SIZE = 500

## Path to save final combined output
OUTPUT_FILE = "query_output.xlsx"

# LOAD INPUT #

df_ids = pd.read_excel(INPUT_EXCEL)

id_list = (
    df_ids[INPUT_COLUMN]
    .dropna()
    .astype(str)
    .str.strip()
    .unique()
    .tolist()
)

if not id_list:
    raise ValueError("No valid values found in input Excel")

print(f"Total unique IDs found: {len(id_list)}")


# HELPER FUNCTIONS #

def chunk_list(lst, size):
    """Yield successive chunks from list."""
    for i in range(0, len(lst), size):
        yield lst[i:i + size]


def format_in_values(values):
    """Format values for SQL IN clause: 'A','B','C' """
    return ", ".join(f"'{v}'" for v in values)


def run_query(query: str) -> pd.DataFrame:
    """
    Replace this function with your own database connection logic.

    Example:
        - Use cx_Oracle / oracledb
        - Use pymysql / sqlalchemy
        - Use internal data access libraries
    """
    raise NotImplementedError("Add your database query execution logic here.")


# BASE QUERY TEMPLATE #

BASE_QUERY = """
SELECT column1, column2, column3
FROM your_table
WHERE customer_number IN ({})
"""


# MAIN EXECUTION #

final_df = pd.DataFrame()

for idx, chunk in enumerate(chunk_list(id_list, CHUNK_SIZE), start=1):
    in_clause = format_in_values(chunk)
    query = BASE_QUERY.format(in_clause)

    print(f"Running chunk {idx} | Records in chunk: {len(chunk)}")

    temp_df = run_query(query)
    final_df = pd.concat([final_df, temp_df], ignore_index=True)

print("All chunks executed successfully")

final_df.to_excel(OUTPUT_FILE, index=False)

print(f"Total input IDs  : {len(id_list)}")
print(f"Total rows fetched: {len(final_df)}")
print(f"Output saved to  : {os.path.abspath(OUTPUT_FILE)}")

