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
### 自訂需要的時間資訊
```SQL
SELECT DATE_FORMAT(NOW(), "%Y-%m-%d") -- YYYY-MM-DD
```
#### Tips
以 2023-04-15 13:59:20 為例：
- %Y（YYYY）：2023
- %y（YY）：23
- %M（english_month_name）：April
- %m（MM）：04
- %D（english_date）：15th
- %H（24 hours）：13
- %h（12 hours）：1
- %i（minute）：59
- %s（second）：20
### Reference
<ol>
    <li>https://www.w3schools.com/sql/func_mysql_month.asp</li>
    <li>https://www.fooish.com/sql/date.html</li>
    <li>https://www.w3school.com.cn/sql/sql_dates.asp</li>
    <li>https://stackoverflow.com/questions/9032047/how-to-select-only-date-from-a-datetime-field-in-mysql</li>
    <li>https://www.fooish.com/sql/mysql-date_format-function.html</li>
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
### Reference
<ol>
    <li>https://dev.mysql.com/doc/refman/8.0/en/date-and-time-functions.html#function_convert-tz</li>
    <li>http://tw.gitbook.net/mysql/mysql_function_convert_tz.html</li>
</ol>

## DISTINCT：
去除整行重複的資料。
### SELECT DISTINCT
查詢不重複的資料，只能放置於 SELECT 之後且括號不影響查詢結果。
```SQL
SELECT DISTINCT column1, column2 FROM table1;
SELECT DISTINCT (column1), column2 FROM table1; -- 查詢結果與上述 SQL 相同
SELECT DISTINCT (column1, column2) FROM table1; -- Error，DISTINCT 的括號內僅能放置一欄位
```
### 搭配聚合函數使用
可以不用放置於 SELECT 之後。
```SQL
SELECT COUNT(DISTINCT column1) FROM table1; -- 計算 column1 不重複值的數量
```
### Reference
<ol>
    <li>https://www.twle.cn/c/yufei/mysqlfav/mysqlfav-basic-distinct.html</li>
    <li>https://www.twle.cn/c/yufei/mysqlfav/mysqlfav-basic-distinct2.html</li>
    <li>https://www.yiibai.com/mysql/distinct.html</li>
    <li>https://www.w3schools.com/sql/sql_distinct.asp</li>
    <li>https://stackoverflow.com/questions/7250566/mysql-select-distinct</li>
    <li>https://stackoverflow.com/questions/1443069/mysql-error-when-trying-to-get-unique-values-using-distinct-together-with-left-j</li>
</ol>
