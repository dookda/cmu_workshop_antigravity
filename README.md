# คู่มือการใช้งาน Google Antigravity สำหรับการพัฒนาเว็บแอปพลิเคชัน

## ชื่อหลักสูตร

การพัฒนาเว็บแอปพลิเคชันระบบแจ้งซ่อมอาคารสถานที่ด้วย Google Antigravity (1 วัน)

## วัตถุประสงค์

-   วิเคราะห์ปัญหา
-   ออกแบบความต้องการ
-   สร้าง Flowchart
-   ออกแบบฐานข้อมูล
-   เขียน Prompt สำหรับ AI
-   พัฒนา ทดสอบ และเผยแพร่แอปพลิเคชัน

## กรณีศึกษา

ระบบแจ้งซ่อมอาคารสถานที่ (Facility Repair Management System)

## กำหนดการ

  เวลา          หัวข้อ
  ------------- --------------------------
  09:00-09:30   Problem and Requirement
  09:30-10:15   User Story และ Flowchart
  10:15-10:45   Data Model
  11:00-11:30   AI Specification
  12:30-13:00   แนะนำ Google Antigravity
  13:00-14:00   พัฒนา MVP
  14:00-15:00   UX/UI และ Testing
  15:00-16:30   Debugging และ Deployment

## ขั้นตอนการพัฒนา

### 1. วิเคราะห์ปัญหา

คำถามหลัก

-   ใครคือผู้ใช้งาน
-   ปัญหาคืออะไร
-   ต้องการข้อมูลอะไร
-   ผลลัพธ์ที่คาดหวังคืออะไร

### 2. User Story

ตัวอย่าง

> As a staff member, I want to report a damaged facility with a photo so
> that the maintenance team can repair it.

### 3. Flowchart

``` mermaid
flowchart TD
A[พบจุดชำรุด] --> B[เข้าสู่ระบบ]
B --> C[กรอกข้อมูล]
C --> D[แนบรูปภาพ]
D --> E[ส่งคำขอ]
E --> F[เจ้าหน้าที่รับเรื่อง]
F --> G[มอบหมายช่าง]
G --> H[ซ่อมแซม]
H --> I[ปิดงาน]
```

### 4. Data Model

ตารางหลัก

-   User
-   Building
-   Room
-   RepairRequest
-   Technician
-   Attachment

ตัวอย่างโครงสร้าง

``` sql
RepairRequest(
 id,
 ticket_no,
 building_id,
 room_id,
 description,
 status,
 created_at
)
```

## ตัวอย่าง Prompt

### Prompt 1: วิเคราะห์ความต้องการ

``` text
You are a system analyst.

Analyze the requirements for a Facility Repair Management System.

Identify:
- stakeholders
- user roles
- required features
- missing requirements

Do not generate code.
```

### Prompt 2: สร้างสถาปัตยกรรมระบบ

``` text
You are a software architect.

Design the application architecture.

Include:
- frontend
- backend
- database
- authentication
- file storage

Do not write code.
```

### Prompt 3: สร้างฐานข้อมูล

``` text
Design a normalized database schema.

Generate:
- entities
- relationships
- primary keys
- foreign keys
```

### Prompt 4: พัฒนาแอปพลิเคชัน

``` text
Build an MVP web application.

Features:
- login
- create repair request
- upload photos
- status tracking
- dashboard

Verify the application after implementation.
```

### Prompt 5: ตรวจสอบ UX

``` text
Act as a UX designer.

Review the repair request form.

Identify:
- usability issues
- accessibility problems
- mobile responsiveness

Do not modify the code.
```

### Prompt 6: ทดสอบระบบ

``` text
Act as a QA engineer.

Test:
- login
- create request
- upload image
- assign technician
- close request

Generate a test report.
```

### Prompt 7: แก้ไขข้อผิดพลาด

``` text
Identify the root cause.

Explain:
- why the error occurred
- affected components
- recommended fix

Wait for approval before changing code.
```

## Deployment

``` text
Local
 ↓
GitHub
 ↓
Build
 ↓
Hosting
 ↓
Public URL
```

## ผลลัพธ์ที่คาดหวัง

-   Flowchart
-   Data model
-   Prompt specification
-   Web application
-   Test report
-   Public URL
