Exercise : ตู้ยอดน้ำอัดลม
===

พัฒนาตู้ยอดน้ำอัดลม โดยเรียกใช้งาน API รายละเอียดของสินต้าจากที่มีให้  
โดยเงื่อนไขในการพัฒนาของตู้นี้มีดังนี้
- สินค้ามีอย่างไม่จำกัด
- เงินทอนมีอย่างไม่จำกัด
- เหรียญที่ใช้ได้คือ 1, 2, 5 และ 10 บาท เท่านั้น  

**ตัวอย่างการใช้งาน**  

|  | Story | เหรียญที่ยอดตามลำดับ | ยอดเงินทั้งหม | สินค้าที่เลือก | ได้รับสินค้า | เงินทอนที่ได้รับ|
|---|-------|------------------|------------|-----------|----------|------------|
| 1 |ผู้ใช้หยอดเหรียญ 10, 5 และเลือกสินค้า Pepsi Max|10, 5|15|Pepsi Max|true|-|
| 2 |ผู้ใช้หยอดเหรียญ 10, 5, 2, 1 และเลือกสินค้า Pepsi Max|10, 5, 2, 1|18|Pepsi Max|true|2, 1|
| 3 |ผู้ใช้หยอดเหรียญ 10, 2 และเลือกสินค้า Pepsi Max แต่เลือกไม่ได้เพราะยอดเงินไม่พอ|10, 2|12|Pepsi Max|false|-|
| 4 |ผู้ใช้หยอดเหรียญ 10, 2 และเลือกสินค้า Coke Vanilla (S) แต่เลือกไม่ได้เพราะสินค้าไม่มีในตู้|10, 2|12|Coke || 5 |Vanilla (S)|false|-|
| 6 |ผู้ใช้หยอดเหรียญ 10, 10, 2 แต่เปลี่ยนใจขอเงินคืน|10, 10, 2|22|-|false|10, 10, 2|


ข้อมูลน้ำอัดลม
---

| API | Endpoint | Method |
|-----|----------|--------|
|Drinking list|http://www.mocky.io/v2/5af10fc5310000580096c7d4|GET|

ข้อตกลงการตรวจรับ
---
1. ทำการ Fork github project นี้ไปยังของตนเอง
2. นำ Source code ที่ทำเรียบร้อยใส่ไว้ในโฟลเดอร์ `exercise` เท่านั้น

ข้อสงสัยอื่น ๆ 
---
ทำการเปิด Issue เพื่อสอบถามหรือแนะนำเพิ่มเติมเกี่ยวกับโจทย์นี้ได้ที่ลิงค์ด้านล่าง  
https://github.com/nitipatl/problem-vending-machine/issues
