## LOCK_TIMEOUT

```sql
-- SET LOCK_TIMEOUT
-- 180,000 milliseconds, which is equivalent to 3 minutes
-- 90,000 milliseconds, which is equivalent to 90 sec

SET LOCK_TIMEOUT 90000;
GO

--  SET DEFAULT 

SET LOCK_TIMEOUT -1;  
GO

-- GET SETTING

SELECT @@LOCK_TIMEOUT;
GO
```



ปกติแล้วในการทำงานแบบ multi-user ที่มีการใช้ข้อมูลพร้อมๆ กันหลายๆ คนนั้น มักจะมีการแก้ไขข้อมูลพร้อมๆ กันด้วย ซึ่งแน่นอนครับ คนที่เข้ามาแก้ไขข้อมูลก่อนก็จะทำการ lock table หรือ record ที่กำลังแก้ไขอยู่ ผลก็คือทำให้ user คนที่เข้ามาทีหลังไม่สามารถที่จะแก้ไขข้อมูลเดียวกันกับที่ user คนแรกเข้ามาแก้ไขอยู่ได้ จะต้องรอ รอจนกว่า user คนแรกทำการแก้ไขเสร็จแล้วปลด lock table หรือ record นั้นก่อน ซึ่งในบางครั้งก็อาจจะรอนานเป็น ชม.หรือเป็นวันก็ได้ครับ ถ้าเป็นการ lock table
คำสั่งต่อไปนี้เป็นวิธีการกำหนด lock timeout ไม่ใช่ query timeout นะครับ โดยตัวเลข 3000 คือเวลาที่เรากำหนด หน่วยเป็น milli-second ซึ่งก็หมายความว่าถ้าเรารอจนถึงเวลา time out แล้ว ทาง user คนแรกยังแก้ไขไม่เสร็จหรือไม่ยอมปลด lock เราก็จะตัดสินใจ kill ตัวเองทันที หลังจากนั้นก็หาเวลา รัน stored procedure ที่เราต้องการใหม่อีกครั้งครับ

