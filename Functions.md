## 取出4的位置
```
SELECT CHARINDEX('4','123456789')
```
output
```
4
```
## 字串長度
```
SELECT LEN('1234567')
```
output
```
7
```
## CASE條件

```
SELECT
CASE '1'
WHEN '1' THEN 'OK'
WHEN '2' THEN 'ON'
ELSE '3' 
END
```
output
```
OK
```
## REPLACE
```
SELECT REPLACE('ABCDEFG','BCDE','EDCB')
```
output
```
AEDCBFG
```
## UPDATE 用組合TABLE
```
UPDATE Table1
SET Column1 = t1.C1 
FROM TABLE1 t1 JOIN TABLE2 t2 ON t1.C1 = t2.C1 
```
## UPDATE 塞資料
```
UPDATE QuotationVersion
SET QuotationVersion.Number = CONCAT(q.Number,'-',qv.Version)
FROM Quotation q join QuotationVersion qv on q.ID = qv.QuotationID


UPDATE InquaryVersion
SET InquaryVersion.Number = CONCAT(i.Number,'-',iv.Version)
FROM Inquary i join InquaryVersion iv on i.ID = iv.InquaryID
```
### 站存
```
                //找該詢價編號所屬的CPQ編號
                var cpqIds = _conn.Query<int>(@"
                        SELECT c.ID
                        FROM CPQ c 
                        JOIN Quotation q on c.ID = q.CPQID 
                        JOIN QuotationVersion qv on q.ID = qv.QuotationID
                        WHERE qv.Number LIKE CONCAT('%,', @Number,',%') ",
                    new { Number = model.InquaryNumber }).ToList();
```