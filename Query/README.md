# SQL
## 查詢 collation：
查詢特定欄位的 <a href="https://github.com/Yintc123/SQL/tree/main/Error#note">Collation</a>。
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

## 查詢時間欄位：
### 僅顯示需要的時間資訊
- SECOND()：僅顯示秒的時間資訊（SS）
```SQL
SELECT SECOND(datetime_column) FROM table1;
```
- MINUTE()：僅顯示分鐘的時間資訊（mm）
```SQL
SELECT MINUTE(datetime_column) FROM table1;
```
- HOUR()：僅顯示小時的時間資訊（HH）
```SQL
SELECT HOUR(datetime_column) FROM table1;
```
- DATE()：僅顯示 DATE 型別的時間資訊（YYYY-MM-DD）
```SQL
SELECT DATE(datetime_column) FROM table1;
```
- MONTH()：僅顯示月份的時間資訊（MM）
```SQL
SELECT MONTH(datetime_column) FROM table1;
```
- YEAR()：僅顯示年份的時間資訊（YYYY）
```SQL
SELECT YEAR(datetime_column) FROM table1;
```
