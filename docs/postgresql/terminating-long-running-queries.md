# Terminating Long-Running Queries

This runbook is to terminate long-running PostgreSQL queries.

## Procedure

### 1. Identify Long-Running Queries

First, find the queries that are running longer than desired. You can use the following SQL command:

```sql
SELECT pid, now() - pg_stat_activity.query_start AS duration, query 
FROM pg_stat_activity 
WHERE state = 'active' 
AND now() - pg_stat_activity.query_start > interval '{{INTERVAL}}';
```

Replace `{{INTERVEAL}}` with the desired time (e.g., `5 minutes`) to identify queries running longer than that time.

### 2. Terminate the Queries

If you find a query that needs to be terminated, use the PID from the above step to kill it:

```sql
SELECT pg_cancel_backend({{PID}});
```

Replace `{{PID}}` with the process ID of the query you want to terminate.

### 3. Verify Termination

Make sure that the query has been terminated by running the command from Step 1 again. If the query is still active, you can forcefully terminate it:

```sql
SELECT pg_terminate_backend({{PID}});
```

Replace `{{PID}}` with the process ID of the query you want to terminate.

### 4. Monitor Regularly

It's important to regularly monitor your database for long-running queries to ensure optimal performance. Implement logging and alerting, or consider using monitoring tools specific to PostgreSQL.

### 5. Document and Notify

Make a record of any terminated queries and notify the relevant team or individual, as killing a query may affect ongoing operations or processes within your application. Communication helps to avoid confusion and potential issues.

By following these steps, you'll have a process in place to identify and manage long-running queries in your PostgreSQL environment.

## Expected Result

All long-running queries are intended to be terminated.
