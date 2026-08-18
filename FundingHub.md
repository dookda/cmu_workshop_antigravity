
```text
สร้าง Web Application ภาษาไทยชื่อ Funding Hub – ระบบจัดการข้อมูลทุนวิจัย

เป็นระบบขนาดเล็กสำหรับฝึกพัฒนา Web Application

มีเพียง 4 หน้า:

1. Dashboard
    แสดง KPI 4 ช่อง:
* ทุนที่เปิดรับ
* ทุนใกล้หมดเขต
* ทุนปิดรับแล้ว
* ทุนทั้งหมด

2. รายการทุน
    แสดงข้อมูลเป็น Card หรือ Table:
* ชื่อทุน
* แหล่งทุน
* Theme
* Deadline
* สถานะ
มี Search และ Filter ตามสถานะ

3. เพิ่ม / แก้ไขทุน
    สร้าง Form:
* ชื่อทุน
* แหล่งทุน
* Theme
* Deadline
* URL
* หมายเหตุ
* สถานะ

สถานะ:
* เปิดรับ
* ใกล้หมดเขต
* ปิดรับแล้ว

มีปุ่ม บันทึก / ยกเลิก

4. Admin
    สามารถ:
* เพิ่มข้อมูล
* แก้ไข
* ลบ

สร้าง Database และ CRUD
ใช้ Supabase
project name: fundinghub

สร้าง Demo Data 3 รายการ:

TREE Fund
Deadline: 1 กันยายน 2569
Status: ใกล้หมดเขต

Belmont Forum CRA
Deadline: 30 กันยายน 2569
Status: เปิดรับ

ASEA-UNINET
Deadline: 15 พฤศจิกายน 2569
Status: เปิดรับ


UI design:
ภาษาไทย
Minimal
Clean
Responsive
ใช้งานง่าย
 
Palette สี: `#222831` · `#393E46` · `#00ADB5` · `#EEEEEE`
ฟอนต์: `IBM Plex Sans Thai`, `Noto Sans Thai`, `sans-serif`

เมนูมีเพียง:
Dashboard | ทุนวิจัย | เพิ่มทุน | Admin

ไม่ต้องสร้าง AI, LINE, Proposal, Project Tracking หรือระบบซับซ้อนอื่น


