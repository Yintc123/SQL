# SQL
## Error 1：
### Error Code：1267
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
* utf8mb4：對 Unicode 的編碼。於 MySQL 中，utf8mb4 為正式的 utf8 編碼，使用四個位元組儲存。（於 MySQL 中，utf8 實為 utf8mb3 使用三個位元組儲存）
* Collation：定序。資料庫預先定義處理字元集（Character set）的一套規則，包含描述字元、字元的排序及字元的比較。
* Character set：字元集。
* Collation 與 Character set 的對應關係：一個定序僅對應一個字元集；一個字元集可以有多個定序。
### Reference：
<ol>
    <li>https://stackoverflow.com/questions/44027987/illegal-mix-of-collations-utf8mb4-unicode-ci-implicit-and-utf8mb4-general-ci</li>
    <li>https://dotblogs.com.tw/Eyelash/2021/05/07/192212</li>
    <li>https://dev.mysql.com/doc/refman/8.0/en/charset-collate.html (COLLATE)</li>
    <li>https://cloud.tencent.com/developer/article/1366841 (COLLATE)</li>
    <li>https://www.cadch.com/modules/news/article.php?storyid=198 (utf8mb4 Collation)</li>
    <li>https://www.cnblogs.com/amyzhu/p/9595665.html (utf8mb4 Collation)</li>
    <li>https://khiav223577.github.io/blog/2019/06/30/MySQL-%E7%B7%A8%E7%A2%BC%E6%8C%91%E9%81%B8%E8%88%87%E5%B7%AE%E7%95%B0%E6%AF%94%E8%BC%83/ (utf8mb4)</li>
    <li>https://ithelp.ithome.com.tw/articles/10222814 (Collation and Character set)</li>
    <li>https://dotblogs.com.tw/jimmyyu/2009/08/30/10320 (Collation)</li>
    <li>https://developer.aliyun.com/article/347339 (Collation)</li>
    <li>https://www.geeksforgeeks.org/what-is-collation-and-character-set-in-mysql/ (the relationship between Collation and Character set)</li>
</ol>