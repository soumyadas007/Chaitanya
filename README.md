Certainly! Here's a Python function that takes a list of dictionaries, where each dictionary contains keys for `table_name`, `column_names`, and `where`. It generates SQL queries based on these values and returns a list of queries that can be used with other variables when required:

```python
def generate_sql_queries(table_data):
    queries = []

    for data in table_data:
        table_name = data.get("table_name")
        column_names = data.get("column_names", [])
        where_conditions = data.get("where", {})

        query = f"SELECT {', '.join(column_names) if column_names else '*'} FROM {table_name}"

        if where_conditions:
            where_clause = " AND ".join([f"{key} = '{value}'" for key, value in where_conditions.items()])
            query += f" WHERE {where_clause}"

        queries.append(query)

    return queries

# Example usage:
tables = [
    {"table_name": "customers", "column_names": ["first_name", "last_name"], "where": {"age": 25, "city": "New York"}},
    {"table_name": "orders", "where": {"status": "shipped"}},
    {"table_name": "products"}
]

queries = generate_sql_queries(tables)

# Use the generated queries with other variables when required
for query in queries:
    print(query)
```

You can call the `generate_sql_queries` function with your list of dictionaries containing `table_name`, `column_names`, and `where` information to generate SQL queries. The resulting list of queries can be used with other variables or functions as needed.

# Chaitanya
