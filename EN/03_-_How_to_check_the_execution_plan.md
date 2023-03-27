To check the execution plan of a SQL query in an Oracle database, you can use the Explain Plan feature, as it provides an estimated execution plan for your query. Here's how to check the execution plan using different methods:

Using the EXPLAIN PLAN FOR statement:
```
EXPLAIN PLAN FOR
SELECT * FROM employees WHERE department_id = 10;
```
After running the EXPLAIN PLAN FOR statement, you can view the execution plan by querying the PLAN_TABLE:

```
SELECT * FROM TABLE(DBMS_XPLAN.DISPLAY('PLAN_TABLE', NULL, 'TYPICAL'));
```
Using the DBMS_XPLAN package with the SQL_ID:
First, find the SQL_ID for your query by looking into the V$SQL view:

```
SELECT sql_id, sql_text
FROM v$sql
WHERE sql_text LIKE 'SELECT%FROM employees%';
```
Next, use the SQL_ID to display the execution plan using the DBMS_XPLAN package:

```
SELECT * FROM table(DBMS_XPLAN.DISPLAY_CURSOR('<SQL_ID>', NULL, 'TYPICAL'));
```
Using the SQL*Plus AUTOTRACE feature:
In SQL*Plus, enable the AUTOTRACE feature to display the execution plan and statistics after running the query:

```
SET AUTOTRACE ON
SELECT * FROM employees WHERE department_id = 10;
```
To turn off AUTOTRACE, use the following command:

```
SET AUTOTRACE OFF
```
Keep in mind that the Explain Plan provides an estimated execution plan, and the actual execution might differ slightly due to runtime factors. To capture the actual execution plan, you can use tools like SQL Trace (with TKPROF utility) or Oracle Enterprise Manager to analyze the performance and gather more accurate information about the execution plan.
