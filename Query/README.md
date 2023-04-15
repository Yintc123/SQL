# QUERY
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

## 查詢時間資訊：
### 僅顯示需要的時間資訊
- SECOND()：僅顯示秒的時間資訊（SS）。
```SQL
SELECT SECOND(NOW());
```
- MINUTE()：僅顯示分鐘的時間資訊（mm）。
```SQL
SELECT MINUTE(NOW());
```
- HOUR()：僅顯示小時的時間資訊（HH）。
```SQL
SELECT HOUR(NOW());
```
- DATE()：僅顯示 DATE 型別的時間資訊（YYYY-MM-DD）。
```SQL
SELECT DATE(NOW());
```
- MONTH()：僅顯示月份的時間資訊（MM）。
```SQL
SELECT MONTH(NOW());
```
- YEAR()：僅顯示年份的時間資訊（YYYY）。
```SQL
SELECT YEAR(NOW());
```
#### Reference
<ol>
    <li>https://www.w3schools.com/sql/func_mysql_month.asp</li>
    <li>https://www.fooish.com/sql/date.html</li>
    <li>https://www.w3school.com.cn/sql/sql_dates.asp</li>
</ol>

### 轉換時區
資料庫通常為 UTC 時區，有時須因需求轉換資料的時區，以下以轉換至台灣時區（UTC+8）為例。
#### Method_1（Better）：
CONVERT_TZ(datetime, from_tz, to_tz)：將時間資訊轉換至指定時區的時間。
```SQL
SELECT CONVERT_TZ(NOW(), 'system', '+8:00'); -- system 為資料庫的時區
```
#### Method_2
DATE_ADD(datetime, interval 8 HOUR)：將時間資訊加上 8 小時。
```SQL
SELECT DATE_ADD(NOW(), INTERVAL 8 HOUR);
```
#### Reference
<ol>
    <li>https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_convert-tz</li>
    <li>http://tw.gitbook.net/mysql/mysql_function_convert_tz.html</li>
</ol>