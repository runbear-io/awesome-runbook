# Checking Query History

This runbook is to check PostgreSQL query history.

## Procedure

Checking PostgreSQL query history can be done through various means, depending on your setup.

### Using Log Files

PostgreSQL can log queries into log files.
Check your PostgreSQL configuration file (usually `postgresql.conf`) for the proper settings.
Look for parameters like `log_statement`, `log_directory`, and `log_filename`.

### Using `pg_stat_statements` Module:

This is an extension that provides query statistics. Run the below query to enable it.

```sql
CREATE EXTENSION pg_stat_statements;
```

Query the `pg_stat_statements` view to see the query history.

```sql
SELECT * FROM pg_stat_statements;
```

### Using Command Line History

If you're using psql, the command-line tool, you can press the Up Arrow key to scroll through previous queries. History might be stored in the `.psql_history` file in your home directory.

## Expected Result

Recent queries are intended to be displayed.
