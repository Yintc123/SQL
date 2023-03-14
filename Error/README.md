# SQL
## Error Code：1093
Error Code: 1093. You can't specify target table 'tableName' for update in FROM clause
### Problem：
於 MSQL 更新表的資料時，（WHERE 等）條件運算式的子查詢所查詢的表不得與更新資料的表相同。
```SQL
UPDATE table1 SET field1=value1, field2=value2 WHERE field_pk IN (SELECT field_pk FROM table1 WHERE field3=value3);
```
### Solution_1：
於 MSQL 更新表 table1 的資料時，將最內層子查詢 table1 的結果作為暫時的表並讓外層的子查詢查詢該表。
### Example_1：
```SQL
UPDATE table1 SET field1=value1, field2=value2 
WHERE field_pk IN (
    SELECT field_pk FROM (
        SELECT field_pk FROM table1 WHERE field3=value3
        ) as tempTable
    );
```
### Solution_2：
於 MSQL 更新表 table1 的資料時，table1 內部連結（INNER JOIN）自己並將其中一張表使用 AS 另外命名，此做法可以使 MySQL 將此二表示為不同的表。
### Example_2：
```SQL
UPDATE table1
INNER JOIN table1 AS tempTable ON table1.field_pk=tempTable.field_pk
SET table1.field1=value1, table1.field2=value2 
WHERE tempTable.field3=value3;
```
### Reference：
<ol>
    <li>https://blog.csdn.net/u010657094/article/details/64439486</li>
    <li>https://stackoverflow.com/questions/45494/mysql-error-1093-cant-specify-target-table-for-update-in-from-clause</li>
</ol>

## Error Code：1267
Illegal mix of collations (utf8mb4_unicode_ci,IMPLICIT) and (utf8mb4_general_ci,IMPLICIT) for operation '='
### Problem：
由於兩張表的編碼不同。JOIN 兩張表時，欄位的值無法使用 = 相互比對。
### Solution：
將欄位的值設置相同的 Collation。
### Example：
```SQL
SELECT table1.field2, table2.field2 FROM table1 
JOIN table2 ON table1.field1 COLLATE utf8mb4_general_ci = table2.field1 COLLATE utf8mb4_general_ci;
```
### Note
* Collate：設定 expression-level 的 Collation 為 utf8mb4_general_ci。
* utf8mb4_general_ci：utf8mb4 的 Collation。較簡易也較快（與 utf8mb4_unicode_ci 對比）的 Collation。
* utf8mb4_unicode_ci：utf8mb4 的 Collation。基於標準的 unicode 排序及比較，能夠於各種語言間精準的排序。
* utf8mb4_0900_ai_ci：utf8mb4 的 Collation，為 MySQL 預設 utf8mb4 的 collation。基於標準的 unicode 排序及比較，能夠於各種語言間精準的排序，並且較 utf8mb4_general_ci 更為優化的 collation。
* utf8mb4：對 Unicode 的編碼。於 MySQL 中，utf8mb4 為正式的 utf8 編碼，使用四個位元組儲存。（於 MySQL 中，utf8 實為 utf8mb3 使用三個位元組儲存）
* Collation：定序。資料庫預先定義處理字元集（Character set）的一套規則，包含描述字元、排序字元及比較字元。
```SQL
SHOW COLLATION; -- 查詢 Collation 的 SQL 語法
```
* Character set：字元集。一組包含（多個）字元符號及其對應的編碼。
```SQL
SHOW CHARACTER SET; -- 查詢 Character set 的 SQL 語法
```
* Collation 與 Character set 的對應關係：一個定序僅對應一個字元集；一個字元集可以有多個定序，且至少有一個定序。
### Reference：
<ol>
    <li>https://stackoverflow.com/questions/44027987/illegal-mix-of-collations-utf8mb4-unicode-ci-implicit-and-utf8mb4-general-ci</li>
    <li>https://dotblogs.com.tw/Eyelash/2021/05/07/192212</li>
    <li>https://dev.mysql.com/doc/refman/8.0/en/charset-collate.html (COLLATE)</li>
    <li>https://cloud.tencent.com/developer/article/1366841 (COLLATE)</li>
    <li>https://www.cadch.com/modules/news/article.php?storyid=198 (utf8mb4 Collation)</li>
    <li>https://www.cnblogs.com/amyzhu/p/9595665.html (utf8mb4 Collation)</li>
    <li>https://khiav223577.github.io/blog/2019/06/30/MySQL-%E7%B7%A8%E7%A2%BC%E6%8C%91%E9%81%B8%E8%88%87%E5%B7%AE%E7%95%B0%E6%AF%94%E8%BC%83/ (utf8mb4)</li>
    <li>https://dotblogs.com.tw/jimmyyu/2009/08/30/10320 (Collation)</li>
    <li>https://developer.aliyun.com/article/347339 (Collation)</li>
    <li>https://www.geeksforgeeks.org/what-is-collation-and-character-set-in-mysql/ (the relationship between Collation and Character set)</li>
    <li>https://dev.mysql.com/doc/refman/8.0/en/charset-general.html (the relationship between Collation and Character set)</li>
    <li>https://dev.mysql.com/doc/refman/8.0/en/charset-mysql.html (the relationship between Collation and Character set)</li>
    <li>https://dev.mysql.com/doc/refman/8.0/en/adding-collation.html (Weight_string)</li>
</ol>