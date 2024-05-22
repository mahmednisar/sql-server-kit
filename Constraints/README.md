### Default Constraints:
```sql
SELECT OBJECT_NAME(parent_object_id) AS TableName
	,cl.name AS ColumnName
	,type.name AS Type
	,ct.DEFINITION
FROM sys.default_constraints ct
JOIN sys.columns cl ON ct.parent_column_id = cl.column_id
	AND ct.parent_object_id = cl.object_id
JOIN sys.types type ON cl.user_type_id = type.user_type_id
ORDER BY TableName
OPTION (RECOMPILE);
```

### Key Constraints:
```sql
SELECT K.TABLE_NAME AS TableName
	,K.COLUMN_NAME AS ColumnName
	,K.CONSTRAINT_NAME AS ConstaintName
FROM INFORMATION_SCHEMA.TABLE_CONSTRAINTS AS C
JOIN INFORMATION_SCHEMA.KEY_COLUMN_USAGE AS K ON C.TABLE_NAME = K.TABLE_NAME
	AND C.CONSTRAINT_CATALOG = K.CONSTRAINT_CATALOG
	AND C.CONSTRAINT_SCHEMA = K.CONSTRAINT_SCHEMA
	AND C.CONSTRAINT_NAME = K.CONSTRAINT_NAME
WHERE C.CONSTRAINT_TYPE = 'PRIMARY KEY'
OPTION (RECOMPILE);
```
