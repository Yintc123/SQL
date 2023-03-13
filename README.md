# SQL
## Error 1：
Error Code：1267. Illegal mix of collations (utf8mb4_unicode_ci,IMPLICIT) and (utf8mb4_general_ci,IMPLICIT) for operation '='
### Problem：
由於兩張表的編碼不同。JOIN 兩張表時，欄位的值無法使用 = 相互比對。
### Solution：
將欄位的值使用相同的編碼。
### Example：
```
SELECT table1.field2, table2.field2 FROM table1 JOIN table2 ON table1.field1 COLLATE utf8mb4_general_ci = table2.field1 COLLATE utf8mb4_general_ci;
```
### Reference：
1. https://stackoverflow.com/questions/44027987/illegal-mix-of-collations-utf8mb4-unicode-ci-implicit-and-utf8mb4-general-ci
2. https://dotblogs.com.tw/Eyelash/2021/05/07/192212
