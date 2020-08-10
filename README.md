----------------------------------
All columns (from both tables and views) that I have access to:
```sql
SELECT * FROM ALL_TAB_COLUMNS
```
-----------------------------------------
All the tables that I have access to:
```sql
SELECT owner, table_name, num_rows
FROM all_tables
```
---------------------------------------
All the tables in the db, if I have privileges for it:
```sql
SELECT owner, table_name
FROM dba_tables
```
----------------------------------------------
All the views that I have access to:
```sql
SELECT owner, view_name 
FROM all_views
```
------------------------------------------------------
Relations į nurodytą lentelę:
```sql
--CASE SENSITIVE
SELECT   PARENT.TABLE_NAME  "PARENT TABLE_NAME"
,        PARENT.CONSTRAINT_NAME  "PARENT PK CONSTRAINT"
,       '->' " "
,        CHILD.TABLE_NAME  "CHILD TABLE_NAME"
,        CHILD.COLUMN_NAME  "CHILD COLUMN_NAME"
,        CHILD.CONSTRAINT_NAME  "CHILD CONSTRAINT_NAME"
FROM     ALL_CONS_COLUMNS   CHILD
,        ALL_CONSTRAINTS   CT
,        ALL_CONSTRAINTS   PARENT
WHERE    CHILD.OWNER  =  CT.OWNER
AND      CT.CONSTRAINT_TYPE  = 'R'
AND      CHILD.CONSTRAINT_NAME  =  CT.CONSTRAINT_NAME 
AND      CT.R_OWNER  =  PARENT.OWNER
AND      CT.R_CONSTRAINT_NAME  =  PARENT.CONSTRAINT_NAME 
AND      CHILD.TABLE_NAME  = :tabl -- table name variable
AND      CT.OWNER  = :owner; -- schema variable
```
----------------------------------------------------------
