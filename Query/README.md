# SQL
## 查詢 collation：
查詢特定欄位的 Collation。
### Method_1（better）
```SQL
SHOW FULL COLUMNS FROM tableName;
```
### Method_2
```SQL
SELECT COLLATION_NAME FROM information_schema.columns
WHERE TABLE_SCHEMA = 'databaseName' 
AND TABLE_NAME = 'tableName'
AND COLUMN_NAME = 'fieldName';
```
### Reference：
<ol>
    <li>https://stackoverflow.com/questions/7617412/discover-collation-of-a-mysql-column</li>
</ol>