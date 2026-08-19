# เอกสารประกอบภาคปฏิบัติ (Lab Manual)
## Workshop: การพัฒนา Web Application ด้วย Google Antigravity
### กรณีศึกษา — Funding Hub: ระบบจัดการข้อมูลทุนวิจัย

# LAB 0 — เตรียมเครื่องมือ

## ขั้นตอน

### 0.1 ติดตั้ง Node.js
1. เข้า <https://nodejs.org> ดาวน์โหลดเวอร์ชัน **LTS**
2. ติดตั้งตามค่าเริ่มต้น (กด Next ตลอด)
3. เปิด Terminal / Command Prompt แล้วตรวจสอบ

```bash
node -v
npm -v
```

### 0.2 ติดตั้ง Git และสมัคร GitHub
1. ติดตั้ง Git จาก <https://git-scm.com>
2. สมัครบัญชีที่ <https://github.com> (ถ้ายังไม่มี)
3. ตั้งค่าชื่อและอีเมล

```bash
git config --global user.name "ชื่อของคุณ"
git config --global user.email "อีเมลของคุณ"
```

### 0.3 สมัคร Supabase
1. เข้า <https://supabase.com> → **Start your project**
2. เข้าสู่ระบบด้วยบัญชี GitHub (สะดวกที่สุด)
3. ยังไม่ต้องสร้างโปรเจกต์ — จะสร้างใน LAB 4

### 0.4 ดาวน์โหลด Google Antigravity
1. เข้า <https://antigravity.google/download>
2. เลือก **Antigravity IDE** (ไม่ใช่ Antigravity 2.0 desktop app)
   > เวิร์กช็อปนี้ต้องใช้ตัวแก้ไขโค้ด + Terminal + Browser ในหน้าต่างเดียว จึงใช้ IDE
3. ติดตั้งแล้วเปิดโปรแกรม ล็อกอินด้วยบัญชี Google


---

# LAB 1 — ติดตั้งและเปิดโปรเจกต์แรก

## ขั้นตอน

### 1.1 สร้างโฟลเดอร์โปรเจกต์

```bash
mkdir fundinghub
cd fundinghub
```

### 1.2 เปิดโฟลเดอร์ใน Antigravity
`File` → `Open Folder...` → เลือกโฟลเดอร์ `fundinghub`

### 1.3 สำรวจหน้าจอ 4 ส่วน

| ส่วน | หน้าที่ |
|---|---|
| **Editor** | แก้ไขไฟล์โดยตรง มี Tab autocomplete |
| **Agent / Agent Manager** | ช่องคุยกับ Agent และดูงานที่กำลังทำ |
| **Artifacts** | แผนงาน (Plan) รายการงาน และผลตรวจสอบที่ Agent สร้าง |
| **Browser** | เบราว์เซอร์ที่ Agent ควบคุมเองเพื่อทดสอบเว็บ |

### 1.4 วางไฟล์สเปก
คัดลอกไฟล์ `FundingHub.md` มาไว้ที่รากโฟลเดอร์ `fundinghub/`

### 1.5 Prompt แรก — ให้ Agent อ่านสเปก

> 📋 **คัดลอกทั้งกล่องนี้ไปวางในช่อง Agent**

```text
อ่านไฟล์ FundingHub.md ทั้งไฟล์
สรุปให้ฟังเป็นภาษาไทยว่า ระบบนี้มีกี่หน้า อะไรบ้าง เก็บข้อมูลกี่ฟิลด์ และมีอะไรบ้างที่ห้ามสร้าง
ยังไม่ต้องเขียนโค้ดใด ๆ
```

---

# LAB 2 — แกะโจทย์ให้เป็นสเปก

## 2.1 Prompt — ให้ Agent ตรวจสเปกที่เราเขียน

> 📋 **คัดลอกไปวางใน Agent**

```text
ตรวจไฟล์ FundingHub.md ในฐานะ Reviewer
หาจุดที่กำกวม ขัดแย้งกันเอง หรือทดสอบไม่ได้ 
รายงานเป็นตารางภาษาไทย: หัวข้อ | ปัญหา | ข้อเสนอแนะ
ห้ามแก้ไขไฟล์ ให้รายงานอย่างเดียว
```

> 📋 **หากต้องการปรับแก้ คัดลอกไปวางใน Agent**

```text
ปรับแก้ ตามข้อเสนอแนะ เป็นไฟล์ FoundingHub2.md
```

---

# LAB 3 — กำหนด Design System ด้วยตัวเอง

## 3.1 เลือกสไตล์จาก UI Style Guide

🔗 <https://www.uistyleguide.com/>

เว็บนี้รวมสไตล์การออกแบบ UI ไว้ 67 แบบ พร้อมตัวอย่างที่กดเล่นได้จริง

**วิธีทำ**
1. เลื่อนดูสไตล์ทั้งหมด กดเข้าไปดูตัวอย่าง
2. เลือก **1 สไตล์** ที่เหมาะกับระบบข้อมูลทุนวิจัย

| สไตล์แนะนำ | เหมาะเพราะ |
|---|---|
| **Minimalism** | อ่านข้อมูลง่าย เหมาะกับงานราชการ/วิชาการ (ค่าเริ่มต้นของสเปก) |
| **Flat Design** | เรียบ ทำเร็ว รองรับ responsive ดี |
| **Soft UI / Neumorphism** | นุ่มนวล แต่ระวังปัญหาความคมชัดของตัวอักษร |
| **Glassmorphism** | สวยแต่ทำให้อ่านตัวเลข KPI ยาก — ไม่แนะนำสำหรับ dashboard |


## 3.2 เลือกจานสีจาก Color Hunt

🔗 <https://colorhunt.co/>

**วิธีทำ**
1. เลือกหมวด `Pastel`, `Vintage` หรือ `Popular`
2. เลือก 1 palette (4 สี) แล้วกดคัดลอกรหัส HEX ทั้งชุด
3. จับคู่สีเข้ากับ token ตามหลัก **60–30–10**

| Token | เอาสีไหนมาใส่ | สัดส่วน |
|---|---|---|
| `--color-bg` | สีอ่อนที่สุด | 60% |
| `--color-ink` | สีเข้มที่สุด | 30% |
| `--color-primary` | สีที่สดที่สุด | 10% (ปุ่มและจุดเน้นเท่านั้น) |
| `--color-surface` | ขาว `#FFFFFF` เสมอ | — |

4. ตรวจความคมชัดที่ <https://webaim.org/resources/contrastchecker/> — ตัวอักษรกับพื้นหลังต้องได้ **อัตราส่วนอย่างน้อย 4.5:1**

## 3.3 เลือกฟอนต์จาก Google Fonts

🔗 <https://fonts.google.com/?subset=thai>

**สำคัญ:** ต้องกรอง `Language = Thai` เท่านั้น ไม่งั้นภาษาไทยจะแสดงผลเพี้ยน

| ฟอนต์ | บุคลิก | เหมาะกับ |
|---|---|---|
| **Sarabun** | ทางการ อ่านง่าย ใกล้เคียง TH Sarabun New | เอกสารราชการ/วิชาการ ✅ ค่าเริ่มต้น |
| **IBM Plex Sans Thai** | สมัยใหม่ สะอาด | ระบบข้อมูล dashboard |
| **Noto Sans Thai** | กลาง ๆ ปลอดภัย | ใช้ได้ทุกงาน |
| **Prompt** | โมเดิร์น เรขาคณิต | เว็บองค์กร |
| **Kanit** | หนักแน่น เด่น | หัวข้อใหญ่ (ไม่เหมาะกับเนื้อหายาว) |

**กฎการใช้ฟอนต์ไทย 3 ข้อ**
1. โหลดแค่ 2–3 น้ำหนัก (400/600/700) — โหลดหมดทำให้เว็บช้า
2. ตั้ง `line-height` อย่างน้อย `1.6` — ภาษาไทยมีสระบนล่าง ถ้าบรรทัดชิดจะชนกัน
3. ห้ามใช้ `text-transform: uppercase` — ภาษาไทยไม่มีตัวพิมพ์ใหญ่

## 3.4 เขียนกลับลงสเปก

เปิด `FundingHub.md` แก้ให้เป็นของตัวเอง

---

# LAB 4 — สร้างฐานข้อมูลด้วย Supabase

> 🎞️ **ตรงกับสไลด์ที่ 31** · ⏱️ 20 นาที · 📖 อ้างอิง `SPEC §5`

## เป้าหมาย
มีฐานข้อมูลจริงบนคลาวด์ พร้อมข้อมูลตัวอย่าง 3 รายการ

## 4.1 สร้างโปรเจกต์

1. <https://supabase.com/dashboard> → **New project**
2. กรอกตามนี้

| ช่อง | ค่า |
|---|---|
| Name | `fundinghub` |
| Database Password | **ตั้งเอง** แล้วเก็บไว้ในที่ปลอดภัย |
| Region | `Southeast Asia (Singapore)` |

3. รอประมาณ 2 นาที

> 🔐 รหัสผ่านฐานข้อมูล **ห้ามพิมพ์ลงในไฟล์สเปกหรือไฟล์โค้ดใด ๆ** และห้ามส่งให้ AI
> (สังเกตว่าในโจทย์ต้นฉบับมีบรรทัด `password: xxx` — นี่คือตัวอย่างของสิ่งที่ **ไม่ควร** เขียนไว้ในเอกสารที่แชร์กัน)

## 4.2 คัดลอกกุญแจเชื่อมต่อ

`Project Settings` → `API Keys`

| ต้องคัดลอก | ห้ามแตะ |
|---|---|
| ✅ `Project URL` | ❌ `service_role` key |
| ✅ `anon` / `publishable` key | |

## 4.3 สร้างไฟล์ `.env.local`

สร้างที่โปรเจกต์ `fundinghub/.env.local`

```
VITE_SUPABASE_URL=<วาง Project URL ที่นี่>
VITE_SUPABASE_ANON_KEY=<วาง anon key ที่นี่>
```

ตัวอย่าง:

```
VITE_SUPABASE_URL=https://abcde12345.supabase.co
VITE_SUPABASE_ANON_KEY=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6ImFiY2RlMTIzNDUiLCJyb2xlIjoiYW5vbiIsImlhdCI6MTY4NzQ5MjAwMCwiZXhwIjoxOTkzMDQ4MDAwfQ.abcdef1234567890abcdef1234567890abcdef12
```

แล้วสร้าง `.gitignore` ให้มีบรรทัด

```
.env.local
node_modules
dist
```

---

# LAB 5 — สร้างแอปพลิเคชันด้วย Antigravity


```text
สร้างโปรเจกต์ตาม FundingHub.md 
```

---

# LAB 6 — ทดสอบและนำขึ้นระบบ

## 6.1 ขึ้น GitHub

```bash
git init
git add .
git commit -m "Funding Hub: ระบบจัดการข้อมูลทุนวิจัย"
git branch -M main
git remote add origin https://github.com/<username>/fundinghub.git
git push -u origin main
```

> 🔍 ก่อน push ให้รัน `git status` แล้วยืนยันว่า **ไม่มี `.env.local`** อยู่ในรายการ

## 6.2 Deploy ขึ้น GitHub Pages

### ขั้นที่ 1 — ให้ Agent แก้โค้ดให้

> 📋 **คัดลอกทั้งกล่องนี้ไปวางในช่อง Agent**

```text
เตรียมโปรเจกต์นี้ให้ deploy ขึ้น GitHub Pages ที่ https://<username>.github.io/fundinghub/

1. แก้ vite.config.js ให้ base เป็น '/fundinghub/'
2. ตรวจ src/main.jsx หรือ src/App.jsx ถ้าใช้ BrowserRouter ให้เปลี่ยนเป็น HashRouter
3. สร้างไฟล์ .github/workflows/deploy.yml ให้ build ด้วย Node 24 แล้ว deploy ด้วย actions/deploy-pages (ใช้ action เวอร์ชันล่าสุด)
   โดยรับ VITE_SUPABASE_URL และ VITE_SUPABASE_ANON_KEY จาก GitHub Actions Secrets
4. ห้ามเขียนค่า URL หรือ key จริงลงในไฟล์ใด ๆ ที่จะถูก commit

เสร็จแล้วสรุปเป็นภาษาไทยว่าผมต้องไปตั้งค่าอะไรบ้างในหน้าเว็บ GitHub
```

### ขั้นที่ 2 — ใส่ Secrets บน GitHub

ไปที่หน้า repo ของตัวเองบนเว็บ GitHub

`Settings` → เมนูซ้าย `Secrets and variables` → `Actions` → ปุ่ม **New repository secret**

ทำ **2 รอบ** ตามตารางนี้ (ค่าคัดลอกมาจากไฟล์ `.env.local` ของ LAB 4)

| Name (พิมพ์ให้ตรงตัวพิมพ์ใหญ่เป๊ะ) | Secret |
|---|---|
| `VITE_SUPABASE_URL` | `https://abcde12345.supabase.co` |
| `VITE_SUPABASE_ANON_KEY` | `eyJhbGciOi...` (คีย์ยาว ๆ) |


---

### ขั้นที่ 3 — เปิดใช้งาน GitHub Pages

`Settings` → เมนูซ้าย `Pages` → หัวข้อ **Build and deployment** → ช่อง `Source`

เลือกเป็น **GitHub Actions** (ไม่ใช่ `Deploy from a branch`)

> ถ้าเลือก `Deploy from a branch` มันจะไปหยิบโค้ดดิบที่ยังไม่ build มาเสิร์ฟ → หน้าขาวแน่นอน

---

### ขั้นที่ 4 — push แล้วดูผล

```bash
git status                       # ยืนยันอีกครั้งว่าไม่มี .env.local
git add .
git commit -m "เพิ่ม workflow deploy ขึ้น GitHub Pages"
git push
```

เปิดแท็บ **Actions** บนหน้า repo จะเห็นงานชื่อ `Deploy to GitHub Pages` กำลังรัน

| ไอคอน | ความหมาย | ทำอะไรต่อ |
|---|---|---|
| 🟡 จุดเหลืองหมุน | กำลัง build (ปกติ 1–3 นาที) | รอ |
| ✅ ติ๊กเขียว | สำเร็จ | เปิดเว็บได้เลย |
| ❌ กากบาทแดง | ล้มเหลว | กดเข้าไปอ่าน log ดูว่า step ไหนแดง |

เสร็จแล้วเปิด

```
https://<username>.github.io/fundinghub/
```

---


# 📎 ภาคผนวก

## ก. คำสั่งที่ใช้บ่อย

```bash
npm install          # ติดตั้ง dependency
npm run dev          # รันเซิร์ฟเวอร์พัฒนา
npm run build        # สร้างไฟล์สำหรับขึ้นระบบ
npm run preview      # ดูผลลัพธ์ของ build
git status           # ดูว่ามีไฟล์อะไรจะถูก commit บ้าง
```

## ข. แหล่งอ้างอิง

| เรื่อง | ลิงก์ |
|---|---|
| Google Antigravity | <https://antigravity.google> |
| เอกสาร Antigravity | <https://antigravity.google/docs/getting-started> |
| Supabase Docs | <https://supabase.com/docs> |
| UI Style Guide (67 สไตล์) | <https://www.uistyleguide.com/> |
| Color Hunt | <https://colorhunt.co/> |
| Google Fonts (ไทย) | <https://fonts.google.com/?subset=thai> |
| Contrast Checker | <https://webaim.org/resources/contrastchecker/> |
| Vite | <https://vite.dev> |
| React | <https://react.dev> |
| Tailwind CSS | <https://tailwindcss.com> |

---

*เอกสารประกอบการอบรม — Funding Hub × Google Antigravity*
