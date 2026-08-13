# Workshop 1 วัน — สร้างเว็บแอปด้วย Google Antigravity
## กรณีศึกษา: ระบบแจ้งซ่อมงานอาคารสถานที่ "FacilityCare"

> แนวคิดหลักของหลักสูตร: **"คิดให้จบก่อน แล้วค่อยให้ AI ลงมือ"**
> ผู้เรียนจะไม่พิมพ์คำสั่งลอย ๆ ให้ AI เดา แต่จะเปลี่ยนความคิดรวบยอด → Requirements → Flowchart → Spec → แล้วจึงให้ Agent พัฒนา ทดสอบ และ Deploy

---

## 1. ข้อมูลหลักสูตร

| หัวข้อ | รายละเอียด |
|---|---|
| ชื่อหลักสูตร | Agentic Web Development with Google Antigravity: ระบบแจ้งซ่อมอาคารสถานที่ |
| ระยะเวลา | 1 วัน (เนื้อหาและปฏิบัติประมาณ 6 ชั่วโมง 30 นาที รวมพัก 1 ชั่วโมง 30 นาที) |
| กลุ่มเป้าหมาย | บุคลากรสายสนับสนุน/IT, อาจารย์, นักศึกษาป.ตรี–ป.โท ที่มีพื้นฐานคอมพิวเตอร์ทั่วไป (ไม่จำเป็นต้องเขียนโค้ดเป็น) |
| จำนวนที่เหมาะสม | 20–30 คน + ผู้ช่วยวิทยากร 2 คน |
| รูปแบบ | บรรยาย 30% : ปฏิบัติ 70% (ทำงานเดี่ยวบนเครื่องตัวเอง, ปรึกษาเป็นกลุ่ม 4–5 คน) |
| ผลผลิตของผู้เรียน | เว็บแอปแจ้งซ่อมที่ deploy ขึ้น GitHub Pages ใช้งานได้จริง + repo บน GitHub + เอกสารออกแบบ (flowchart + ERD + spec) |

### ผลลัพธ์การเรียนรู้ (Learning Outcomes)

เมื่อจบการอบรม ผู้เรียนสามารถ

1. ติดตั้งและตั้งค่า Google Antigravity พร้อมเชื่อมต่อ GitHub ได้
2. แปลงปัญหาการทำงานจริงเป็น Requirements, User Story และ **Flowchart** ที่สื่อสารกับ AI ได้อย่างแม่นยำ
3. ใช้ AI ออกแบบโครงสร้างฐานข้อมูล PostgreSQL บน Supabase (ERD / schema) และตรวจทานความถูกต้องด้วยตนเอง
4. สั่งงาน Agent ให้สร้างฟอร์มแจ้งซ่อม, อัปโหลดรูป, Dashboard และระบบแจ้งเตือน
5. อ่านและวิจารณ์ **Artifacts** (Implementation Plan / Task List / Walkthrough) เพื่อควบคุมทิศทางของ Agent
6. ใช้ **Browser Agent** ทดสอบและตรวจรับงานหน้าเว็บโดยอัตโนมัติ
7. Deploy ระบบขึ้น GitHub Pages และส่งมอบงาน

---

## 2. สิ่งที่ต้องเตรียมก่อนวันอบรม

### ผู้เรียนเตรียมมาเอง (ส่ง checklist ล่วงหน้า 1 สัปดาห์)

- [ ] โน้ตบุ๊ก Windows / macOS / Linux — RAM ≥ 8 GB (แนะนำ 16 GB), พื้นที่ว่าง ≥ 10 GB
- [ ] **บัญชี Google ส่วนตัว (Gmail)** — บัญชีองค์กรบางแห่งถูกล็อกไม่ให้ล็อกอิน Antigravity
- [ ] **บัญชี GitHub** (สมัครฟรี) + ยืนยันอีเมลแล้ว
- [ ] ติดตั้ง **Google Chrome และตั้งเป็นเบราว์เซอร์เริ่มต้น** (จำเป็นสำหรับ Browser Agent)
- [ ] ติดตั้ง **Node.js LTS (v20 ขึ้นไป)** และ **Git**
- [ ] ติดตั้ง **Google Antigravity** จาก `https://antigravity.google/download` (ทั้ง Antigravity และ Antigravity IDE)
- [ ] ทดลองล็อกอิน Antigravity ให้ผ่านมาก่อนวันอบรม

### ทีมงานเตรียม

- อินเทอร์เน็ตเสถียร (Agent ทำงานผ่านคลาวด์ตลอดเวลา) — ประเมิน 5–10 Mbps/คน
- ปลั๊กไฟเพียงพอ, จอโปรเจกเตอร์ 2 จอถ้าเป็นไปได้ (จอหนึ่งค้างที่ flowchart)
- Slide + ไฟล์นี้แจกเป็น PDF, และ repo ตัวอย่างสำรอง (เผื่อผู้เรียนตามไม่ทัน ให้ `git clone` จุดเช็กพอยต์ได้)
- **แผน B**: เตรียมโปรเจกต์สำเร็จรูปของแต่ละ checkpoint ไว้ใน branch `checkpoint-1` … `checkpoint-6`

---

## 3. คู่มือทำตามทีละขั้นสำหรับผู้เข้าอบรม

> **เริ่มทำจากหัวข้อนี้ได้ทันที** ทุกกล่องที่มีป้าย **ก๊อบปี้ prompt นี้** ให้คัดลอกทั้งกล่องไปวางใน Antigravity ตามลำดับ ห้ามข้าม checkpoint เพราะ prompt ขั้นถัดไปอ้างอิงไฟล์จากขั้นก่อนหน้า

### ขั้นที่ 0 — เปิดเครื่องมือให้พร้อม

1. เปิด Google Antigravity และลงชื่อเข้าใช้ด้วยบัญชี Google
2. เปิด Chrome แล้วลงชื่อเข้าใช้ GitHub
3. เปิด Terminal แล้วพิมพ์ `node -v` และ `git --version` หากเห็นเลขเวอร์ชันทั้งคู่ ให้ทำขั้นที่ 1

> ✅ **ผ่านขั้นนี้เมื่อ**: เปิด Antigravity, Chrome และ Terminal ได้

### ขั้นที่ 1 — สร้างโฟลเดอร์และ GitHub repository

1. เปิด Terminal แล้วก๊อบปี้คำสั่งนี้

```bash
mkdir -p ~/antigravity-projects/facility-care
cd ~/antigravity-projects/facility-care
```

2. ใน Antigravity เลือก `Select Project → New Project → Add Folder` แล้วเลือกโฟลเดอร์ `facility-care`
3. ในช่องสนทนา Antigravity ให้ **ก๊อบปี้ prompt นี้ทั้งกล่อง**

```text
ในโฟลเดอร์นี้ ช่วยสร้าง Git repository และตั้งค่า .gitignore สำหรับ Vite/Node
ต้อง ignore node_modules, .env และ dist
สร้าง README.md ที่ระบุว่าโปรเจกต์นี้คือ FacilityCare ระบบแจ้งซ่อมอาคารสถานที่
commit งานแรกด้วยข้อความ "chore: initial project setup"
จากนั้นบอกขั้นตอนแบบสั้น ๆ ที่ฉันต้องทำเองเพื่อสร้าง repository แบบ Public บน GitHub และ push โค้ดขึ้นไป
ยังไม่ต้องสร้างเว็บหรือเขียนโค้ดแอป
```

4. ทำตามคำตอบของ Agent เพื่อสร้าง repository **Public** บน GitHub และ push branch `main`

> ✅ **ผ่านขั้นนี้เมื่อ**: หน้า GitHub มี repository ของตนเอง และมีไฟล์ `README.md` กับ `.gitignore`

### ขั้นที่ 2 — สร้าง Flowchart ก่อนเขียนโค้ด

1. สร้างไฟล์ว่างชื่อ `docs/flow.md` ในโฟลเดอร์โปรเจกต์
2. ใน Antigravity ให้ **ก๊อบปี้ prompt นี้ทั้งกล่อง**

```text
คุณคือ Business Analyst สำหรับระบบแจ้งซ่อมอาคารสถานที่ชื่อ FacilityCare

ช่วยสร้างเอกสาร Flowchart ด้วย Mermaid แล้วบันทึกลงไฟล์ docs/flow.md

บริบทระบบ:
- ผู้แจ้งกรอกหัวข้อ ประเภท รายละเอียด อาคาร ชั้น ห้อง และแนบรูปได้ 1–3 รูป
- ธุรการตรวจสอบเรื่อง แล้วขอข้อมูลเพิ่ม, ปฏิเสธ, หรือมอบหมายช่างได้
- ช่างเริ่มงาน, พักงานเมื่อรออะไหล่, ซ่อมเสร็จ และบันทึกผลได้
- ผู้แจ้งดูสถานะและยืนยันผลการซ่อมได้
- หัวหน้างานดู Dashboard ได้

สถานะที่อนุญาต:
NEW, NEED_INFO, REJECTED, ASSIGNED, IN_PROGRESS, ON_HOLD, DONE, CLOSED

ใน docs/flow.md ให้สร้างตามลำดับนี้:
1. Process Flow ด้วย Mermaid: ตั้งแต่พบจุดชำรุดจนปิดงาน
2. State Diagram ด้วย Mermaid: ทุก state และทุกเส้นทางเปลี่ยนสถานะ
3. Swimlane แบบตาราง: ผู้แจ้ง, ธุรการ, ช่าง, หัวหน้างาน ทำอะไรได้บ้าง
4. Screen Flow ด้วย Mermaid: หน้ารายการแจ้งซ่อม, ฟอร์มแจ้งซ่อม, รายละเอียด, อัปเดตสถานะ, Dashboard, การแจ้งเตือน
5. หัวข้อ "คำถามที่ต้องตัดสินใจ" สำหรับกฎธุรกิจที่ยังไม่ชัดเจน

ใช้ภาษาไทยในข้อความที่ผู้ใช้เห็น
Mermaid ต้อง render ได้
ห้ามใส่ระบบ login หรือแผนที่
ยังไม่ต้องเขียนโค้ดแอป, SQL หรือสร้างฐานข้อมูล
```

3. เปิดไฟล์ `docs/flow.md` และดูว่า Mermaid ครบ 3 แผนภาพกับ 1 ตารางหรือไม่

> ✅ **ผ่านขั้นนี้เมื่อ**: มี `docs/flow.md`, มี Process Flow/State Diagram/Screen Flow/Swimlane ครบ และไม่มี Login หรือแผนที่

### ขั้นที่ 3 — สร้างแบบฐานข้อมูลและ SPEC

1. ใน Antigravity ให้ **ก๊อบปี้ prompt นี้ทั้งกล่อง**

```text
อ่าน @docs/flow.md ก่อน แล้วออกแบบฐานข้อมูล PostgreSQL สำหรับ Supabase

สร้างไฟล์ docs/data-model.md ที่มี:
- ตาราง buildings, tickets, attachments, ticket_updates, notifications
- ทุก field พร้อมชนิดข้อมูล, primary key, foreign key, enum และ index ที่จำเป็น
- ERD ด้วย Mermaid erDiagram
- วิธีสร้าง ticket_no รูปแบบ FC-YYYY-0001 โดยไม่ชนกัน
- ข้อเสนอ Row Level Security (RLS) สำหรับเดโม และคำเตือนสำหรับระบบจริง
- รายการข้อมูลส่วนบุคคลที่ต้องระวังตาม PDPA

จากนั้นสร้าง SPEC.md โดยสรุป flow, หน้าจอ, user story, data model และเทคโนโลยีต่อไปนี้:
- Vite + React + JavaScript + Tailwind CSS
- Supabase PostgreSQL, Data API, Storage และ Realtime
- GitHub Pages ผ่าน GitHub Actions
- UI ภาษาไทยและรองรับมือถือ

ยังไม่ต้องสร้างเว็บหรือรัน SQL
```

2. ตรวจว่ามีไฟล์ `docs/data-model.md` และ `SPEC.md`

> ✅ **ผ่านขั้นนี้เมื่อ**: Flow, Data Model และ SPEC มีอยู่ครบ 3 ไฟล์

### ขั้นที่ 4 — สร้าง Supabase project และฐานข้อมูล

1. เข้า [Supabase](https://supabase.com) → `Sign in with GitHub` → `New project`
2. ตั้งชื่อ `facility-care-ชื่อของคุณ` → ตั้ง Database Password → เลือก region ที่ใกล้ที่สุด → `Create new project`
3. เมื่อสถานะพร้อม ให้เปิด `SQL Editor` → `New query`
4. ใน Antigravity ให้ **ก๊อบปี้ prompt นี้ทั้งกล่อง**

```text
อ่าน @docs/data-model.md และ @SPEC.md
สร้างไฟล์ SQL migration ที่รันได้จริงชื่อ supabase/migrations/001_initial_schema.sql
ให้สร้างตาราง buildings, tickets, attachments, ticket_updates และ notifications
ใส่ primary key, foreign key, constraint, index และข้อมูลตัวอย่างอาคารอย่างน้อย 3 แห่ง
สร้าง RLS policy สำหรับ "เดโมในห้องอบรม" ที่อนุญาตเฉพาะการอ่านและบันทึกข้อมูลที่จำเป็น
ใส่ SQL comment ชัดเจนว่า policy เดโมนี้ห้ามใช้กับข้อมูลจริง
ยังไม่ต้องสร้าง React
```

5. เปิดไฟล์ `supabase/migrations/001_initial_schema.sql` → ก๊อบปี้ SQL ทั้งหมด → วางใน Supabase SQL Editor → กด `Run`
6. ใน Supabase ไปที่ `Storage → New bucket` ตั้งชื่อ `ticket-images` แล้วสร้าง bucket
7. ไปที่ `Connect` แล้วคัดลอก **Project URL** และ **Publishable key** เก็บไว้ชั่วคราว ห้ามคัดลอก `service_role` key

> ✅ **ผ่านขั้นนี้เมื่อ**: Table Editor เห็น 5 ตาราง และ Storage เห็น bucket `ticket-images`

### ขั้นที่ 5 — สร้างเว็บและเชื่อม Supabase

1. ใน Antigravity ให้ **ก๊อบปี้ prompt นี้ทั้งกล่อง**

```text
อ่าน @SPEC.md, @docs/flow.md และ @docs/data-model.md ให้ครบก่อน

สร้างเว็บ Vite + React + JavaScript + Tailwind CSS สำหรับ FacilityCare
- ติดตั้ง @supabase/supabase-js, react-router-dom, recharts, date-fns และ lucide-react
- ใช้ HashRouter เพื่อให้ GitHub Pages เปิดทุกหน้าได้
- สร้าง src/services/supabase.js โดยอ่าน VITE_SUPABASE_URL และ VITE_SUPABASE_PUBLISHABLE_KEY จาก .env
- สร้าง .env.example และเพิ่ม .env ใน .gitignore
- ทำหน้ารายการแจ้งซ่อม, ฟอร์มแจ้งซ่อม, รายละเอียดใบแจ้ง, อัปเดตสถานะ, Dashboard และการแจ้งเตือน
- ห้ามใส่ login หรือแผนที่
- รันเว็บในเครื่องและบอก URL สำหรับเปิดทดสอบ

เริ่มจากโครงหน้าและ routing ก่อน ยังไม่ต้องทำฟอร์มบันทึกข้อมูลจริง
```

2. สร้างไฟล์ `.env` โดยคัดลอกชื่อ field จาก `.env.example` แล้ววาง Project URL และ Publishable key ที่ได้จาก Supabase
3. เปิด URL ที่ Agent บอก เช่น `http://localhost:5173`

> ✅ **ผ่านขั้นนี้เมื่อ**: เว็บเปิดได้ใน Chrome และมีหน้าตาม Screen Flow

### ขั้นที่ 6 — ทำฟอร์มแจ้งซ่อมและอัปโหลดรูป

1. ใน Antigravity ให้ **ก๊อบปี้ prompt นี้ทั้งกล่อง**

```text
อ่าน @SPEC.md และแก้เว็บ FacilityCare ให้ฟอร์ม /tickets/new บันทึกข้อมูลจริงลง Supabase

ฟอร์มต้องมี: หัวข้อ, ประเภทงาน, ความเร่งด่วน, รายละเอียด, อาคาร, ชั้น, ห้อง และรูป 1–3 รูป
- ดึงรายชื่ออาคารจากตาราง buildings
- สร้าง row ใน tickets ก่อน แล้วอัปโหลดรูปไป bucket ticket-images ที่ path tickets/{ticketId}/{timestamp}_{index}.jpg
- บันทึกข้อมูลรูปลงตาราง attachments
- แสดง preview, progress และ error ภาษาไทย
- สร้าง ticket_no, status = NEW และ due_at ตามความเร่งด่วน
- หลังบันทึกให้กลับไปหน้ารายการและเห็นใบแจ้งใหม่ทันที
- ห้ามเปลี่ยนไปใช้ login หรือแผนที่

หลังแก้ไข ให้รันเว็บและบอกขั้นตอนทดสอบ 4 ข้อ
```

2. เปิดเว็บ → สร้างใบแจ้งซ่อม 1 รายการ → แนบรูป 1 รูป → กดบันทึก
3. กลับไปที่ Supabase Table Editor และ Storage เพื่อตรวจข้อมูล

> ✅ **ผ่านขั้นนี้เมื่อ**: เห็นข้อมูลใน `tickets`, `attachments` และไฟล์ใน `ticket-images`

### ขั้นที่ 7 — เพิ่ม Dashboard แล้วทดสอบ

1. ใน Antigravity ให้ **ก๊อบปี้ prompt นี้ทั้งกล่อง**

```text
อ่าน @SPEC.md แล้วทำ Dashboard และการแจ้งเตือนของ FacilityCare ให้ใช้ข้อมูลจริงจาก Supabase
- Dashboard แสดงจำนวนเรื่องทั้งหมด, ค้างดำเนินการ, เสร็จเดือนนี้, เกิน SLA และเวลาเฉลี่ยปิดงาน
- ใช้ Recharts แสดงจำนวนเรื่องตามประเภท, สัดส่วนตามสถานะ และแนวโน้ม 30 วัน
- เมื่อสถานะเปลี่ยน ให้บันทึก ticket_updates และ notifications
- ใช้ Supabase Realtime อัปเดตรายการแจ้งเตือน
- เพิ่มปุ่ม Export CSV
- ห้ามเพิ่ม login หรือแผนที่

รันเว็บ แล้วใช้ Browser Agent ทดสอบการสร้างใบแจ้งและเปลี่ยนสถานะ
รายงานผล พร้อม screenshot และรายการปัญหาที่พบ แต่ยังไม่ต้องแก้อัตโนมัติ
```

2. อ่านรายงาน Browser Agent แล้วคัดลอกปัญหาไม่เกิน 3 ข้อที่สำคัญที่สุดกลับไปให้ Agent แก้

> ✅ **ผ่านขั้นนี้เมื่อ**: Dashboard มีข้อมูลจริง และมีรายงานทดสอบอย่างน้อย 1 ชุด

### ขั้นที่ 8 — Deploy ขึ้น GitHub Pages

1. ใน Antigravity ให้ **ก๊อบปี้ prompt นี้ทั้งกล่อง**

```text
เตรียมโปรเจกต์นี้สำหรับ GitHub Pages
- สร้าง .github/workflows/deploy.yml เพื่อ build Vite และ deploy โฟลเดอร์ dist ทุกครั้งที่ push branch main
- ตั้งค่า base ใน vite.config.js ให้ใช้ชื่อ repository นี้
- ตรวจว่าใช้ HashRouter
- ให้ workflow อ่าน VITE_SUPABASE_URL และ VITE_SUPABASE_PUBLISHABLE_KEY จาก GitHub Actions secrets
- รัน npm run build และแก้เฉพาะ error หรือ warning ที่เกิดขึ้น
- สรุปเป็นรายการสิ่งที่ฉันต้องกดใน GitHub แบบทีละคลิก
```

2. บน GitHub repository ไปที่ `Settings → Secrets and variables → Actions → New repository secret`
3. เพิ่ม secret 2 ตัว: `VITE_SUPABASE_URL` และ `VITE_SUPABASE_PUBLISHABLE_KEY`
4. ไปที่ `Settings → Pages → Source` แล้วเลือก `GitHub Actions`
5. commit และ push ไป branch `main` → เปิดแท็บ `Actions` → รอ workflow `Deploy to GitHub Pages` เป็นสีเขียว
6. เปิด URL `https://ชื่อผู้ใช้.github.io/ชื่อ-repository/` แล้วทดลองบันทึกใบแจ้ง 1 รายการ

> ✅ **ผ่านขั้นนี้เมื่อ**: เปิด URL บนมือถือได้ และข้อมูลใบแจ้งปรากฏใน Supabase

---

## 4. ตารางเวลา

| เวลาที่ใช้ | Session | หัวข้อ | ผลผลิต |
|---|---|---|---|
| 30 นาที | — | ลงทะเบียน / ตรวจความพร้อมเครื่อง | เครื่องพร้อม |
| 30 นาที | **S0** | Agentic Development คืออะไร + โจทย์ FacilityCare | เข้าใจภาพรวม |
| 45 นาที | **S1** | ติดตั้ง & ตั้งค่า Antigravity + เชื่อม GitHub | Project + repo ว่าง |
| 15 นาที | ☕ | พักเบรก | |
| 50 นาที | **S2** | **คิดก่อนโค้ด: Requirements → User Story → Flowchart** | `docs/flow.md` |
| 40 นาที | **S3** | AI ออกแบบฐานข้อมูล + เขียน `SPEC.md` | ERD + spec |
| 60 นาที | 🍽 | พักกลางวัน | |
| 50 นาที | **S4** | Scaffold โปรเจกต์ | โครงแอปพร้อม |
| 50 นาที | **S5** | ฟอร์มแจ้งซ่อม + อัปโหลดรูป | แจ้งซ่อมได้ |
| 15 นาที | ☕ | พักเบรก | |
| 40 นาที | **S6** | Dashboard + ระบบแจ้งเตือน | Dashboard ใช้งานได้ |
| 35 นาที | **S7** | Browser Agent ตรวจงาน + Deploy | URL จริง |
| 20 นาที | **S8** | นำเสนอ 60 วินาที / ถอดบทเรียน / ต่อยอด | ใบประกาศ |

---

## 5. รายละเอียดแต่ละ Session

---

### S0 — Agentic Development และโจทย์ (30 นาที)

**บรรยาย (15 นาที)**

- ยุคของเครื่องมือ: Autocomplete → Chat assistant → **Agent ที่วางแผน ลงมือ และตรวจสอบงานเองได้**
- Antigravity คืออะไร: แพลตฟอร์มพัฒนาแบบ agent-first ของ Google ใช้ได้ฟรีในช่วง preview บน Mac/Windows/Linux รองรับหลายโมเดล (Gemini 3 Pro/Flash, Claude, GPT-OSS)
- องค์ประกอบ 4 ส่วน:
  | ส่วน | ใช้ทำอะไร | ใช้ในเวิร์กช็อปนี้ |
  |---|---|---|
  | **Antigravity** (แอปหลัก) | ศูนย์บัญชาการ สั่ง Agent หลายตัวขนาน ตั้ง Scheduled Task | ✅ ใช้เป็นหลัก |
  | **Antigravity IDE** | IDE เต็มรูปแบบ (fork ของ VS Code) + Agent panel | ✅ ใช้ดู/แก้โค้ด |
  | **Antigravity CLI** | สั่ง Agent จาก terminal | ⛔️ ไม่ครอบคลุม |
  | **Antigravity SDK** | เขียน Python สร้าง agent เอง | ⛔️ ไม่ครอบคลุม |
- แนวคิดสำคัญ 5 คำ: **Project · Conversation · Artifact · Browser Agent · Skill**

**เปิดโจทย์ (10 นาที)** — เล่าให้เห็นภาพจริง

> งานอาคารสถานที่ของหน่วยงานรับแจ้งซ่อมผ่าน LINE กลุ่มและกระดาษ
> ปัญหา: หาเรื่องเก่าไม่เจอ, ไม่รู้ว่าเรื่องไหนค้าง, ไม่รู้ว่าจุดชำรุดอยู่ตรงไหนกันแน่ ("ห้องน้ำชั้น 3 ตึกไหน?"),
> ไม่มีรูปประกอบ, ผู้แจ้งไม่รู้สถานะ, สิ้นปีสรุปสถิติไม่ได้

**เป้าหมายของวันนี้** — สร้าง **FacilityCare**: ระบบแจ้งซ่อมที่มี
1. แจ้งเรื่องพร้อมรูปและระบุอาคาร ชั้น ห้อง
2. เจ้าหน้าที่รับเรื่อง มอบหมายช่าง อัปเดตสถานะ
3. ผู้แจ้งติดตามสถานะและได้รับแจ้งเตือน
4. Dashboard สรุปภาพรวมสำหรับผู้บริหาร

**กติกาสำคัญของวัน (เขียนติดผนัง)**
> 🚫 ห้ามสั่ง Agent ว่า "สร้างระบบแจ้งซ่อมให้หน่อย"
> ✅ ต้องมี flowchart และ spec ก่อนเสมอ — AI เก่งเรื่อง "ทำอย่างไร" แต่ **เราต้องเป็นคนตอบว่า "ทำอะไร และทำไม"**

---

### S1 — ติดตั้ง ตั้งค่า และเชื่อม GitHub (45 นาที)

#### 1.1 ติดตั้งและล็อกอิน (10 นาที)
- ดาวน์โหลดจาก `antigravity.google/download` → ติดตั้ง → ล็อกอินด้วย Google → ยอมรับ Security & Data Use → เลือกธีม → เลือก plugin (ข้ามได้)
- ติดตั้ง **Antigravity IDE** เพิ่ม (ไอคอนพื้นดำ) — จะเห็น 2 ไอคอนใน dock

#### 1.2 สร้าง Project (10 นาที)

Project ใน Antigravity = **ชุดโฟลเดอร์ + สิทธิ์ + เครื่องมือ** ที่กำหนดขอบเขตให้ Agent (ไม่ใช่แค่โฟลเดอร์เดียว จะรวม frontend + backend repo ก็ได้)

```bash
mkdir -p ~/antigravity-projects/facility-care
```

`Select Project → New Project → Add Folder` → เลือกโฟลเดอร์ → ตั้งชื่อ `facility-care` → Create

#### 1.3 ตั้งค่า Project Settings (10 นาที) — **สอนให้เข้าใจ ไม่ใช่กด Next ผ่าน**

| ค่า | ความหมาย | แนะนำในห้องอบรม |
|---|---|---|
| Security Preset | Agent ต้องขออนุญาตก่อนรันคำสั่ง terminal / แก้ไฟล์หรือไม่ | **ให้รีวิวก่อน** ในช่วงเช้า (เพื่อให้เห็นว่า Agent ทำอะไร) แล้วค่อยผ่อนช่วงบ่าย |
| Agent Behaviour | ให้ Agent ลงมือตาม plan เลย หรือรอเรารีวิวก่อน | **รอรีวิว** — หัวใจของวันนี้คือการอ่าน Implementation Plan |
| Local Permissions | path / URL ที่อนุญาตหรือบล็อก | ปล่อย default |
| MCP Tools | เลือกว่า MCP server ไหนใช้ได้ในโปรเจกต์นี้ | เปิดเฉพาะที่ใช้ |

> 💡 **จุดสอนสำคัญ**: ความปลอดภัยคือการ "ให้สิทธิ์เท่าที่จำเป็น" — โปรเจกต์งานจริงที่มีข้อมูลส่วนบุคคลต้องตั้งค่าให้เข้ม

#### 1.4 เชื่อมต่อ GitHub (15 นาที)

**วิธีที่ 1 — ให้ Agent ทำให้ (แนะนำ)**

Prompt:
```
สร้าง Git repository ในโฟลเดอร์นี้ ตั้งค่า .gitignore สำหรับโปรเจกต์ Node/Vite
(ต้องมี node_modules, .env, dist)
สร้าง README.md อธิบายว่าโปรเจกต์นี้คือระบบแจ้งซ่อมอาคารสถานที่
แล้ว commit แรกด้วยข้อความ "chore: initial project setup"
จากนั้นบอกขั้นตอนที่ฉันต้องทำเองเพื่อ push ขึ้น GitHub
```

**วิธีที่ 2 — ทำเอง (สำรอง)**
```bash
gh auth login              # หรือสร้าง repo ผ่านเว็บ
gh repo create facility-care --public --source=. --push
```

**ตั้งค่า GitHub MCP (ถ้าเวลาเหลือ / สาธิตหน้าห้อง)**
`Settings → Customizations → Add MCP +` → เลือก GitHub → ใส่ token
เมื่อเชื่อมแล้วสั่งได้เช่น *"เปิด issue ใน repo facility-care สำหรับงานที่ยังไม่เสร็จทั้งหมด"*

> ✅ **Checkpoint 1**: มี Project ใน Antigravity + repo บน GitHub ที่มี commit แรก

---

### S2 — คิดก่อนโค้ด: Requirements → User Story → Flowchart (50 นาที) ⭐ **หัวใจของหลักสูตร**

> ช่วงนี้ **ปิดหน้าจอ Agent** 20 นาทีแรก ใช้กระดาษ/ไวท์บอร์ดก่อน

#### 2.1 ขั้นที่ 1 — ตีโจทย์ด้วย 5W1H (10 นาที, ทำเป็นกลุ่ม)

| คำถาม | คำตอบของ FacilityCare |
|---|---|
| **Who** ใครใช้ | ผู้แจ้ง (บุคลากร/นักศึกษา), ธุรการอาคาร, ช่างเทคนิค, หัวหน้างาน/ผู้บริหาร |
| **What** ทำอะไร | แจ้ง–รับเรื่อง–มอบหมาย–ซ่อม–ปิดงาน–สรุปผล |
| **When** เมื่อไร | ทันทีที่พบปัญหา, ติดตามได้ตลอดเวลา, สรุปรายเดือน |
| **Where** ที่ไหน | มือถือเป็นหลัก (ผู้แจ้งยืนอยู่หน้าจุดชำรุด) → **ต้อง responsive** |
| **Why** ทำไม | ลดเรื่องตกหล่น, ระบุจุดชำรุดชัดเจน, มีหลักฐานภาพ, วัดผลได้ |
| **How** อย่างไร | เว็บแอป + Supabase |

#### 2.2 ขั้นที่ 2 — Actor & User Story (10 นาที)

รูปแบบ: **ในฐานะ \<ใคร\> ฉันต้องการ \<ทำอะไร\> เพื่อ \<ได้ประโยชน์อะไร\>**

| # | Actor | User Story | Priority |
|---|---|---|---|
| US-01 | ผู้แจ้ง | แจ้งจุดชำรุดพร้อมรูปและข้อมูลอาคาร ชั้น ห้อง | Must |
| US-02 | ผู้แจ้ง | ดูสถานะเรื่องที่ตนแจ้งไว้ | Must |
| US-03 | ธุรการ | เห็นเรื่องใหม่ทั้งหมดและมอบหมายช่าง | Must |
| US-04 | ช่าง | ดูงานที่ได้รับมอบหมาย + อัปเดตสถานะพร้อมรูปหลังซ่อม | Must |
| US-05 | ทุกคน | ได้รับแจ้งเตือนเมื่อสถานะเปลี่ยน | Should |
| US-06 | หัวหน้างาน | Dashboard สรุปจำนวน/ประเภท/เวลาเฉลี่ยของงานซ่อม | Should |
| US-07 | ผู้ดูแล | จัดการผู้ใช้ อาคาร และประเภทงาน | Could |
| US-08 | ผู้แจ้ง | ให้คะแนนความพึงพอใจหลังปิดงาน | Won't (เฟสถัดไป) |

> 💡 **สอน MoSCoW**: ในเวิร์กช็อป 1 วัน เราทำ **Must ทั้งหมด + Should เท่าที่ทัน** — การกล้าตัด scope คือทักษะที่สำคัญกว่าการเขียนโค้ด

#### 2.3 ขั้นที่ 3 — เขียน Flowchart 4 ระดับ (20 นาที)

**สอนให้เห็นว่า flowchart ไม่ได้มีแบบเดียว** แต่ละแบบตอบคำถามคนละอย่าง

#### 2.3.1 ผู้เรียนต้องก๊อบปี้อะไร

ให้กลับไปที่ **คู่มือทำตามทีละขั้น → ขั้นที่ 2 — สร้าง Flowchart ก่อนเขียนโค้ด** แล้วก๊อบปี้ prompt เพียงกล่องเดียวในหัวข้อนั้นไปวางใน Antigravity

> ✅ **ตรวจเองก่อนผ่านขั้นนี้**: Mermaid ทั้ง 4 ส่วนแสดงผลได้, ไม่มี Login/แผนที่, และทุกสถานะใน State Diagram มีเส้นทางเข้า–ออกที่สมเหตุสมผล

**(ก) Process Flow — ภาพรวมกระบวนการ (ตอบว่า "งานเดินอย่างไร")**

```mermaid
flowchart TD
    A([พบจุดชำรุด]) --> B[/กรอกฟอร์มแจ้งซ่อม<br/>หัวข้อ ประเภท รายละเอียด/]
    B --> C[/ถ่ายรูป 1-3 ภาพ/]
    C --> D[/เลือกอาคาร ชั้น ห้อง/]
    D --> E[(บันทึกเรื่อง<br/>status = NEW)]
    E --> F[แจ้งเตือนธุรการอาคาร]
    F --> G{ธุรการตรวจสอบ<br/>เรื่องสมบูรณ์?}
    G -- ไม่ --> H[ตีกลับ ขอข้อมูลเพิ่ม<br/>status = NEED_INFO]
    H --> B
    G -- ไม่ใช่งานเรา --> I[ปฏิเสธพร้อมเหตุผล<br/>status = REJECTED]
    G -- ใช่ --> J[มอบหมายช่าง + กำหนดความเร่งด่วน<br/>status = ASSIGNED]
    J --> K[ช่างรับงาน<br/>status = IN_PROGRESS]
    K --> L{ซ่อมได้ทันที?}
    L -- ไม่ ต้องรออะไหล่/จ้างเหมา --> M[status = ON_HOLD<br/>บันทึกเหตุผล]
    M --> K
    L -- ได้ --> N[/อัปโหลดรูปหลังซ่อม + บันทึกผล/]
    N --> O[status = DONE]
    O --> P[แจ้งเตือนผู้แจ้ง]
    P --> Q{ผู้แจ้งยืนยัน<br/>เรียบร้อย?}
    Q -- ไม่ --> K
    Q -- ใช่ / ครบ 7 วันไม่ตอบ --> R([status = CLOSED])
    I --> P
```

**(ข) State Diagram — วงจรชีวิตของใบแจ้งซ่อม (ตอบว่า "สถานะมีอะไรบ้าง เปลี่ยนไปไหนได้")**

> นี่คือสิ่งที่ AI ต้องการมากที่สุด เพราะมันแปลตรงเป็น enum + logic การอนุญาต

```mermaid
stateDiagram-v2
    [*] --> NEW: ผู้แจ้งส่งเรื่อง
    NEW --> NEED_INFO: ธุรการขอข้อมูลเพิ่ม
    NEED_INFO --> NEW: ผู้แจ้งแก้ไข
    NEW --> REJECTED: ไม่อยู่ในขอบเขต
    NEW --> ASSIGNED: มอบหมายช่าง
    ASSIGNED --> IN_PROGRESS: ช่างเริ่มงาน
    IN_PROGRESS --> ON_HOLD: รออะไหล่/งบประมาณ
    ON_HOLD --> IN_PROGRESS: พร้อมทำต่อ
    IN_PROGRESS --> DONE: ซ่อมเสร็จ
    DONE --> IN_PROGRESS: ผู้แจ้งไม่ยอมรับ
    DONE --> CLOSED: ยืนยัน/auto 7 วัน
    REJECTED --> [*]
    CLOSED --> [*]
```

**(ค) Swimlane — ใครทำอะไร (ตอบว่า "สิทธิ์ของแต่ละ role คืออะไร")**

| ขั้นตอน | ผู้แจ้ง | ธุรการ | ช่าง | หัวหน้างาน |
|---|:---:|:---:|:---:|:---:|
| สร้างใบแจ้ง | ✅ | ✅ | ✅ | ✅ |
| ดูใบแจ้งทั้งหมด | เฉพาะของตน | ✅ | ที่ได้รับมอบหมาย | ✅ |
| มอบหมายช่าง | ⛔️ | ✅ | ⛔️ | ✅ |
| เปลี่ยนสถานะเป็น IN_PROGRESS/DONE | ⛔️ | ⛔️ | ✅ | ✅ |
| ปิดงาน (CLOSED) | ✅ (ของตน) | ✅ | ⛔️ | ✅ |
| ดู Dashboard | ⛔️ | ✅ | ⛔️ | ✅ |
| จัดการผู้ใช้/อาคาร | ⛔️ | ⛔️ | ⛔️ | ✅ (admin) |

**(ง) Screen Flow — ผังหน้าจอ (ตอบว่า "แอปมีกี่หน้า ไปกันอย่างไร")**

```mermaid
flowchart LR
    H[หน้าหลัก: รายการแจ้งซ่อม]
    H --> NEW[ฟอร์มแจ้งซ่อม]
    NEW --> DET[รายละเอียดใบแจ้ง]
    H --> DET
    H --> DASH[Dashboard]
    DASH --> DET
    DET --> UPD[อัปเดตสถานะ]
    ALL[ทุกหน้า] --> NOTI[กระดิ่งแจ้งเตือน]
```

#### 2.4 ขั้นที่ 4 — ให้ AI ช่วยหาช่องโหว่ของ Flowchart (10 นาที)

**ตอนนี้จึงเปิด Antigravity** และใช้ AI เป็น "ผู้ตรวจ" ไม่ใช่ "ผู้คิดแทน"

Prompt:
```
ฉันออกแบบกระบวนการของระบบแจ้งซ่อมอาคารสถานที่ไว้ตาม flowchart ด้านล่าง
บทบาทของคุณคือ Business Analyst ที่ช่างสงสัย

[วาง mermaid flowchart + state diagram + ตาราง swimlane]

ช่วยทำ 3 อย่าง:
1. หา edge case ที่ฉันยังไม่ได้ครอบคลุม (เช่น เรื่องซ้ำ, ผู้แจ้งลาออก, ช่างลาป่วย, เรื่องเร่งด่วนกลางคืน)
2. ชี้จุดที่ business rule ยังกำกวมและตั้งคำถามกลับมาให้ฉันตัดสินใจ อย่าเดาแทนฉัน
3. ตรวจว่า state transition ครบถ้วนหรือไม่ มี state ไหนที่เข้าไปแล้วออกไม่ได้

ยังไม่ต้องเขียนโค้ดใด ๆ
```

**กิจกรรม**: ผู้เรียนตอบคำถามที่ AI ถามกลับ แล้วปรับ flowchart → บันทึกเป็น `docs/flow.md`

> ✅ **Checkpoint 2**: ไฟล์ `docs/flow.md` มี flowchart 4 ระดับที่ผ่านการตรวจแล้ว
> 💡 **จุดสอน**: สังเกตว่าเราใช้ AI 2 แบบต่างกัน — *"ช่วยคิด"* กับ *"ช่วยตรวจ"* แบบหลังปลอดภัยกว่ามาก

---

### S3 — AI ออกแบบฐานข้อมูล และเขียน SPEC.md (40 นาที)

#### 3.1 สอนหลักการก่อน (5 นาที)

- Entity = คำนามในโจทย์ (ใบแจ้ง, ผู้ใช้, อาคาร, ประเภทงาน, ประวัติการอัปเดต)
- Relationship = ความสัมพันธ์ (ผู้ใช้ 1 คน → แจ้งได้หลายใบ)
- **PostgreSQL**: เริ่มจากตารางที่ไม่ซ้ำซ้อน (normalization) และเชื่อมด้วย foreign key; ค่อยเพิ่ม view หรือข้อมูลซ้ำเฉพาะกรณีที่มีเหตุผลด้านประสิทธิภาพ

#### 3.2 Prompt ออกแบบฐานข้อมูล (15 นาที)

```
จาก flowchart และ user story ใน @docs/flow.md
ช่วยออกแบบโครงสร้างข้อมูล PostgreSQL บน Supabase

ข้อกำหนด:
- ระบุตาราง, field, ชนิดข้อมูล, ค่าที่เป็นไปได้ (enum), primary key, foreign key และ field ที่ต้องมี index
- อธิบายความสัมพันธ์ระหว่างตารางและเหตุผลของ index โดยอ้างอิงจากหน้าจอที่ต้องใช้
- เขียน ERD เป็น mermaid erDiagram
- ระบุรูปแบบเลขที่ใบแจ้ง เช่น FC-2569-0001 และวิธีสร้างให้ไม่ชนกัน
- เสนอ Supabase Row Level Security (RLS) เบื้องต้น และแยกให้ชัดเจนระหว่าง policy สำหรับเดโมกับระบบจริง
- เตือนฉันด้วยถ้ามี field ไหนเป็นข้อมูลส่วนบุคคลที่ควรระวังตาม PDPA

ผลลัพธ์ให้เขียนลงไฟล์ docs/data-model.md ยังไม่ต้องเขียนโค้ดแอป
```

**โครงสร้างเป้าหมาย (วิทยากรเตรียมไว้เทียบ)** — ให้ Agent สร้างเป็น SQL migration ใน `supabase/migrations/`

```
buildings
  id (uuid), code, name, floors

tickets
  id (uuid), ticket_no, title, description
  category, priority, status
  building_id (FK → buildings.id), floor, room
  reporter_name, reporter_phone, assignee_name
  created_at, updated_at, assigned_at, done_at, closed_at, due_at

attachments
  id (uuid), ticket_id (FK → tickets.id), storage_path, public_url, uploaded_at

ticket_updates
  id (uuid), ticket_id (FK → tickets.id), from_status, to_status, note, by_name, created_at

notifications
  id (uuid), ticket_id (FK → tickets.id), recipient_name, type, message, is_read, created_at
```

**Index ที่ต้องมี** (ให้ผู้เรียนสังเกตว่า AI บอกครบหรือไม่)
`tickets(reporter_name, created_at desc)` · `tickets(status, created_at desc)` · `tickets(assignee_name, status)`

#### 3.3 รวมทุกอย่างเป็น SPEC.md (15 นาที) ⭐

**นี่คือเอกสารที่จะกลายเป็น "สัญญา" ระหว่างเรากับ Agent ตลอดช่วงบ่าย**

```
อ่าน @docs/flow.md และ @docs/data-model.md
แล้วสรุปเป็นไฟล์ SPEC.md ฉบับเดียวที่ใช้เป็นแหล่งอ้างอิงหลักของโปรเจกต์ ประกอบด้วย

1. ภาพรวมระบบและวัตถุประสงค์
2. Actor และสิทธิ์ (ตาราง)
3. รายการ User Story พร้อม acceptance criteria แบบ Given-When-Then
4. โครงสร้างข้อมูล
5. รายการหน้าจอ และสิ่งที่ต้องมีในแต่ละหน้า
6. Tech stack ที่กำหนด:
   - Vite + React 18 + JavaScript + Tailwind CSS
   - Supabase: PostgreSQL, Data API, Storage และ Realtime
   - Deploy: GitHub Pages ผ่าน GitHub Actions
   - กราฟ: Recharts
   - รองรับมือถือเป็นหลัก (mobile-first)
   - UI ภาษาไทย, วันที่แบบไทย
7. สิ่งที่ "ไม่ทำ" ในเวอร์ชันนี้ (out of scope)

เขียนให้กระชับ ใช้ bullet และตาราง อย่าใส่โค้ด
```

> ✅ **Checkpoint 3**: มี `docs/flow.md`, `docs/data-model.md`, `SPEC.md` — commit ขึ้น GitHub
> 💡 **จุดสอน**: ตอนนี้ผู้เรียน "เขียนโปรแกรม" ไปแล้ว 40% ทั้งที่ยังไม่มีโค้ดสักบรรทัด

---

### S4 — Scaffold โปรเจกต์ (50 นาที)

#### 4.1 เตรียม Supabase (15 นาที) — ทำคู่ขนาน วิทยากรฉายจอ

1. เข้า `https://supabase.com` → Sign in with GitHub → New project → ชื่อ `facility-care-<ชื่อคุณ>` → ตั้งรหัสผ่านฐานข้อมูลและเลือก region ที่ใกล้ที่สุด
2. รอโปรเจกต์พร้อม แล้วเปิด **SQL Editor** → วางและรัน migration ที่ Agent สร้างจาก data model
3. ไปที่ **Storage** → สร้าง bucket ชื่อ `ticket-images` สำหรับรูปแจ้งซ่อม
4. กด **Connect** → คัดลอก Project URL และ Publishable key

> ⚠️ **จุดสอนเรื่องความปลอดภัย**: Project URL และ Publishable key ใช้บนหน้าเว็บได้ แต่ห้ามนำ `service_role` หรือ secret key ไปใส่ใน React, GitHub repository หรือ GitHub Pages เด็ดขาด; การป้องกันข้อมูลต้องทำด้วย RLS และ policy

#### 4.2 Scaffold ด้วย Agent (15 นาที)

```
อ่าน @SPEC.md ให้ครบก่อน

งานที่ 1: สร้างโครงโปรเจกต์
- Vite + React + JavaScript + Tailwind CSS
- ติดตั้ง @supabase/supabase-js, react-router-dom, recharts, date-fns, lucide-react
- โครงสร้างโฟลเดอร์: src/pages, src/components, src/services, src/hooks, src/utils
- ใส่ฟอนต์ไทยที่อ่านง่าย (Noto Sans Thai หรือ IBM Plex Sans Thai)
- สร้าง src/services/supabase.js ที่อ่านค่าจาก .env (`VITE_SUPABASE_URL`, `VITE_SUPABASE_PUBLISHABLE_KEY`)
- สร้างไฟล์ .env.example และเพิ่ม .env ใน .gitignore
- ทำหน้า placeholder ทุกหน้าตามผัง screen flow พร้อม HashRouter (รองรับ GitHub Pages ที่ไม่มี SPA fallback)

อย่าเพิ่งทำ business logic ทำแค่โครงและ routing ให้รันได้ก่อน
เสร็จแล้วรัน dev server และบอกฉันว่าต้องใส่อะไรใน .env
```

**ระหว่างรอ — สอนอ่าน Artifacts (นี่คือช่วงที่ต้องหยุดสาธิตจริงจัง)**

| Artifact | คืออะไร | ต้องดูอะไร |
|---|---|---|
| **Implementation Plan** | แผนสถาปัตยกรรม/การแก้ไข ก่อนลงมือ | **อ่านให้ละเอียดที่สุด** ถ้าแผนผิด โค้ดผิดหมด — comment แก้ได้ก่อนกด Proceed |
| **Task List** | รายการงานย่อยที่ tick ทีละข้อ | ใช้ติดตามความคืบหน้า |
| **Walkthrough** | สรุปสิ่งที่ทำและวิธีทดสอบ | ใช้ตรวจรับงานและเขียน commit message |
| **Screenshots** | ภาพหน้าจอก่อน/หลัง | หลักฐานว่า UI เปลี่ยนจริง |
| **Code diffs** | ความต่างของโค้ด | รีวิวแบบ PR |

เปิดดูผ่าน **Auxiliary Pane** (มุมขวาบน)

> 💡 **จุดสอน**: Artifact แก้ปัญหา "trust gap" — เมื่อก่อน AI บอกว่า "แก้ให้แล้ว" เราต้องไปไล่โค้ดเอง ตอนนี้มันต้องแสดงหลักฐาน
> **แบบฝึกหัดสั้น**: ให้ผู้เรียนพิมพ์ comment ลงใน Implementation Plan อย่างน้อย 1 ข้อ เช่น *"ขอให้ใช้ react-router v6 แบบ createBrowserRouter"* แล้วดูว่า Agent ปรับตาม

> ✅ **Checkpoint 4**: โครงแอป รันได้ และมีหน้า placeholder ตาม screen flow

---

### S5 — ฟอร์มแจ้งซ่อม + อัปโหลดรูป (50 นาที)

#### 5.1 ฟอร์มแจ้งซ่อมและอัปโหลดรูป (25 นาที)

```
งานที่ 3: หน้าแจ้งซ่อม /tickets/new ตาม US-01

ฟอร์ม:
- หัวข้อ (บังคับ, 5-100 ตัวอักษร)
- ประเภทงาน (dropdown ตาม enum ใน SPEC พร้อมไอคอน)
- ความเร่งด่วน (low/normal/high/urgent) อธิบายสั้น ๆ ว่าแต่ละระดับหมายถึงอะไร
- รายละเอียด (textarea, บังคับ)
- อาคาร (dropdown จากตาราง buildings), ชั้น, ห้อง

อัปโหลดรูป:
- เลือกได้ 1-3 รูป, รองรับถ่ายจากกล้องมือถือ (capture="environment")
- แสดง preview thumbnail และลบทีละรูปได้
- **ย่อรูปฝั่ง client ก่อนอัปโหลด**: ด้านยาวสุดไม่เกิน 1600px, JPEG quality 0.8
  (สำคัญมาก เพราะรูปจากมือถือใหญ่ 5-8 MB)
- อัปโหลดขึ้น Supabase Storage bucket `ticket-images` ที่ path: tickets/{ticketId}/{timestamp}_{index}.jpg
- แสดง progress bar ระหว่างอัปโหลด และปุ่มยกเลิก
- ถ้าอัปโหลดล้มเหลว ต้องไม่ทำให้ข้อมูลใบแจ้งหาย

เมื่อบันทึก: สร้าง ticket ตาม data model, สร้าง ticketNo อัตโนมัติ, status = NEW
คำนวณ dueAt จาก priority (urgent 4 ชม., high 1 วัน, normal 3 วัน, low 7 วัน)
```

> ⚠️ **จุดที่ Agent มักพลาด — ให้ผู้เรียนตรวจเอง**: อัปโหลดรูปก่อนหรือหลังสร้าง ticket? ถ้าอัปโหลดก่อนแล้วผู้ใช้ปิดหน้าไป จะเกิด "ไฟล์กำพร้า" ใน Storage — ลองถาม Agent ว่าจัดการเรื่องนี้อย่างไร

> ✅ **Checkpoint 5**: แจ้งซ่อมได้จริงพร้อมรูป — ตรวจใน Supabase Table Editor และ Storage ว่าข้อมูลเข้าครบ

---

### S6 — Dashboard และระบบแจ้งเตือน (40 นาที)

#### 6.1 รายการงาน + อัปเดตสถานะ (15 นาที)

```
งานที่ 5: หน้ารายการงานและรายละเอียด

/tickets — รายการ:
- Filter: สถานะ, ประเภท, อาคาร, ความเร่งด่วน, ช่วงวันที่, ค้นหาข้อความ
- แสดงรายการทั้งหมดพร้อมตัวกรองเพื่อใช้ติดตามงาน
- Card แสดง: เลขที่, หัวข้อ, badge สถานะ (สีตามระดับ), ความเร่งด่วน, อาคาร-ชั้น, เวลา, รูปแรก
- ไฮไลต์ใบที่เลย dueAt ด้วยสีแดงและป้าย "เกินกำหนด"

/tickets/:id — รายละเอียด:
- ข้อมูลครบ + แกลเลอรีรูป (คลิกขยาย)
- Timeline ประวัติจากตาราง ticket_updates
- ปุ่มเปลี่ยนสถานะ **แสดงเฉพาะ transition ที่อนุญาตตาม state diagram ใน SPEC และตาม role เท่านั้น**
- ทุกครั้งที่เปลี่ยนสถานะ ต้องบันทึกลง updates และอัปเดต timestamp ที่เกี่ยวข้อง
- ธุรการ/หัวหน้างานมอบหมายช่างได้ (dropdown จากรายชื่อช่างที่กำหนดไว้สำหรับเดโม)
```

#### 6.2 ระบบแจ้งเตือน (10 นาที)

```
งานที่ 6: ระบบแจ้งเตือนภายในแอป

- เมื่อสถานะใบแจ้งเปลี่ยน ให้สร้าง row ในตาราง notifications
  ส่งถึง: ผู้แจ้ง (ทุกครั้ง) และช่างที่รับผิดชอบ (เมื่อถูกมอบหมาย)
- ไอคอนกระดิ่งบน navbar พร้อมตัวเลขจำนวนที่ยังไม่อ่าน
  ใช้ Supabase Realtime (Postgres Changes) เพื่อให้อัปเดตแบบ real-time
- Dropdown แสดง 10 รายการล่าสุด คลิกแล้วไปหน้าใบแจ้งและ mark เป็นอ่านแล้ว
- หน้า /notifications แสดงทั้งหมด พร้อมปุ่ม "อ่านทั้งหมด"
```

**สอนต่อยอด (พูดอย่างเดียว ไม่ต้องทำ)**
- **อีเมล**: ใช้ Supabase Edge Function เรียกบริการส่งอีเมล เช่น Resend
- **Web Push**: service worker ร่วมกับผู้ให้บริการ push notification
- **LINE**: ใช้ LINE Messaging API โดยให้ Supabase Edge Function เป็นตัวกลาง
- ⚠️ **ข้อควรระวัง**: การเขียน notification จาก client ทำได้ในเวิร์กช็อป แต่ระบบจริงควรย้ายไป Supabase Edge Function หรือ database trigger เพื่อไม่ให้ client ปลอมแปลงการแจ้งเตือนได้

#### 6.3 Dashboard (15 นาที)

```
งานที่ 7: หน้า /dashboard สำหรับ supervisor/admin

การ์ดตัวเลข: เรื่องทั้งหมด, ค้างดำเนินการ, เสร็จเดือนนี้, เกินกำหนด SLA,
เวลาเฉลี่ยตั้งแต่รับแจ้งจนปิดงาน (ชั่วโมง)

กราฟด้วย Recharts:
- Bar: จำนวนเรื่องแยกตามประเภทงาน
- Pie/Donut: สัดส่วนตามสถานะ
- Line: แนวโน้มรายวันย้อนหลัง 30 วัน
- Horizontal bar: 5 อาคารที่แจ้งซ่อมมากที่สุด

ปุ่ม Export CSV ตาม filter ปัจจุบัน (ให้ encoding รองรับภาษาไทยใน Excel)
ทุกส่วนต้องแสดงผลได้ดีบนจอมือถือ
```

> ✅ **Checkpoint 6**: Dashboard แสดงข้อมูลจริงจาก Supabase

---

### S7 — Browser Agent ตรวจงาน + Deploy (35 นาที)

#### 7.1 Browser Agent (15 นาที) ⭐ **ไฮไลต์ที่คนตื่นเต้นที่สุด**

Browser Agent เปิด Chrome จริง คลิกจริง กรอกฟอร์มจริง แล้วรายงานผลกลับพร้อมภาพ/วิดีโอ
(ต้องตั้ง Chrome เป็นเบราว์เซอร์เริ่มต้น)

**สาธิต 1 — ทดสอบ end-to-end**
```
/browser เปิด http://localhost:5173 แล้วทดสอบ flow การแจ้งซ่อมทั้งหมด:
1. แจ้งซ่อมเรื่องใหม่: หัวข้อ "หลอดไฟชั้น 3 ดับ" ประเภทไฟฟ้า ความเร่งด่วน high
2. เลือกอาคาร ชั้น และห้อง แล้วแนบรูปประกอบ
3. บันทึก แล้วตรวจว่าไปโผล่ในรายการจริง
4. เปิดหน้ารายละเอียดและตรวจว่าข้อมูลครบถ้วน

รายงานผลเป็น artifact พร้อม screenshot ทุกขั้นตอน
ถ้าเจอ error ให้บอกว่าเกิดที่ไหนและสาเหตุน่าจะคืออะไร แต่ยังไม่ต้องแก้
```

**สาธิต 2 — ตรวจ responsive และ accessibility**
```
/browser ทดสอบเว็บที่ localhost:5173 ที่ความกว้าง 390px (iPhone) และ 1440px
ตรวจว่ามีเนื้อหาล้นขอบ ปุ่มเล็กเกินกด หรือข้อความทับกันหรือไม่
ตรวจ contrast ของสีตัวอักษรกับพื้นหลังตามเกณฑ์ WCAG AA
สรุปเป็นรายการปัญหาเรียงตามความรุนแรง พร้อม screenshot ประกอบ
```

จากนั้นสั่ง `แก้ปัญหา 3 ข้อแรกที่พบ แล้วทดสอบซ้ำด้วย browser เพื่อยืนยันว่าแก้ได้จริง`
→ **นี่คือลูป plan → execute → verify ที่เป็นหัวใจของ agentic development**

#### 7.2 RLS และ Deploy (20 นาที)

```
งานที่ 8: เตรียมขึ้นระบบจริง

1. เขียน SQL migration สำหรับตาราง, constraint และ index ตาม @SPEC.md
2. เปิด Row Level Security (RLS) ทุกตารางและ bucket `ticket-images`
   - เขียน policy เดโมที่อนุญาตเฉพาะสิ่งจำเป็นต่อการสร้าง/อ่าน/แก้ไขใบแจ้งในห้องอบรม
   - เพิ่ม comment เตือนว่าการอนุญาต `anon` แบบกว้างใช้ได้เฉพาะเดโม และห้ามใช้กับข้อมูลจริง
   - จำกัดไฟล์ให้เป็น `image/*` และขนาดไม่เกิน 5 MB
3. เขียน `.github/workflows/deploy.yml` เพื่อ build Vite และ deploy `dist` ไป GitHub Pages เมื่อ push branch `main`
   - อ่าน `VITE_SUPABASE_URL` และ `VITE_SUPABASE_PUBLISHABLE_KEY` จาก GitHub Actions secrets ตอน build
4. ตั้งค่า `base` ใน `vite.config.js` ให้ตรงกับชื่อ repository และอธิบายว่าทำไมจึงต้องตั้งค่า
5. รัน build และแก้ warning ที่เกิดขึ้น
6. อธิบายให้ฉันฟังทีละบรรทัดว่า RLS policy และ GitHub Actions workflow ป้องกันหรือทำอะไร
```

**ขั้นตอนบน GitHub**: ไปที่ `Settings → Secrets and variables → Actions` เพิ่ม `VITE_SUPABASE_URL` และ `VITE_SUPABASE_PUBLISHABLE_KEY`; จากนั้นไปที่ `Settings → Pages` เลือก **Source: GitHub Actions** แล้ว push ไปที่ `main` และรอ workflow `Deploy to GitHub Pages` สำเร็จ

**ทดสอบของจริง**: ให้ทุกคนเปิด URL ที่ได้ (`https://<username>.github.io/<repository>/`) **บนมือถือตัวเอง** แล้วลองแจ้งซ่อมจริงในห้องอบรม (เช่น "ปลั๊กไฟห้องประชุมหลวม") → เห็นข้อมูลขึ้น Dashboard บนจอโปรเจกเตอร์ทันที 🎉

**ปิดท้าย — push ขึ้น GitHub**
```
commit งานทั้งหมดด้วยข้อความที่สื่อความหมาย แยกเป็นหลาย commit ตามฟีเจอร์
อัปเดต README.md ให้มี: ภาพหน้าจอ, วิธีติดตั้ง, ตัวแปร .env ที่ต้องใช้, URL ที่ deploy แล้ว
แล้ว push ขึ้น GitHub
```

> ✅ **Checkpoint 7**: URL ใช้งานได้จริง + repo สมบูรณ์

---

### S8 — นำเสนอและถอดบทเรียน (20 นาที)

- **Lightning demo 60 วินาที/คน** (สุ่ม 5–6 คน) เปิด URL จริงบนจอ
- **ถอดบทเรียนร่วมกัน** — คำถามชวนคุย:
  1. ตอนไหนที่ Agent เข้าใจผิด? ย้อนดูสิว่าเป็นเพราะ spec เราไม่ชัดหรือเปล่า
  2. flowchart ที่วาดตอนเช้า ช่วยประหยัดเวลาตอนบ่ายอย่างไรบ้าง
  3. ถ้าไม่มี Artifact ให้อ่าน เราจะรู้ได้อย่างไรว่า Agent ทำถูก
- **สิ่งที่ยังขาดก่อนใช้งานจริง** (สำคัญมาก อย่าให้ผู้เรียนกลับไปด้วยความเข้าใจผิด):
  - PDPA: ข้อตกลงการใช้ข้อมูล, การลบข้อมูล, การเก็บรูปที่อาจติดใบหน้าคน
  - ย้าย business logic สำคัญไป Supabase Edge Functions หรือ database trigger
  - ระบบสำรองข้อมูล, การทดสอบอัตโนมัติ, การเชื่อมกับระบบบุคลากรขององค์กร
  - การประเมินต้นทุน Supabase เมื่อผู้ใช้มาก
- **ต่อยอด**: Skills, Scheduled Tasks (เช่น สรุปเรื่องค้างส่งทุกเช้า 8 โมง), MCP servers, Antigravity CLI

---

## 6. ภาคผนวก

### ก. Prompt Pattern ที่สอนในหลักสูตรนี้

| Pattern | รูปแบบ | ใช้เมื่อ |
|---|---|---|
| **Role + Task + Constraint + Output** | "คุณคือ BA / ช่วยหา edge case / อย่าเดาแทนฉัน / ตอบเป็นตาราง" | ทุกครั้ง |
| **อ้างอิงไฟล์ด้วย @** | `อ่าน @SPEC.md แล้ว…` | ให้ Agent ยึด spec ไม่หลุดบริบท |
| **Stop point** | "ยังไม่ต้องเขียนโค้ด" / "ทำแค่โครงก่อน" | กัน Agent วิ่งเลยธง |
| **Verify loop** | "แก้แล้วทดสอบด้วย browser เพื่อยืนยัน" | ตรวจรับงาน |
| **Explain back** | "อธิบายทีละบรรทัดว่า rule นี้ป้องกันอะไร" | เรียนรู้จากโค้ดที่ AI เขียน |
| **Ask me back** | "ถ้ามีจุดกำกวม ให้ถามกลับ อย่าเดา" | ลดการสมมติผิด |

### ข. Rubric ประเมินผลงาน (100 คะแนน)

| เกณฑ์ | คะแนน |
|---|---|
| เอกสารออกแบบ: flowchart 4 ระดับ + ERD + SPEC ครบและสอดคล้องกัน | 25 |
| ระบบใช้งานได้: แจ้งซ่อม, รูป, สถานะ | 30 |
| Dashboard และการแจ้งเตือน | 15 |
| Deploy สำเร็จ + repo มี README ที่คนอื่นทำตามได้ | 15 |
| คุณภาพการควบคุม Agent (มีการ comment ใน Implementation Plan, มีผลทดสอบจาก Browser Agent) | 15 |

### ค. Troubleshooting ที่เจอบ่อย

| อาการ | สาเหตุ/วิธีแก้ |
|---|---|
| `/browser` ไม่ทำงาน | Chrome ไม่ใช่เบราว์เซอร์เริ่มต้น |
| ล็อกอิน Antigravity ไม่ผ่าน | ใช้บัญชี Google ขององค์กรที่ถูกจำกัด → ใช้ Gmail ส่วนตัว |
| อัปโหลดรูปค้าง | bucket ยังไม่สร้าง, policy ของ Storage บล็อก, หรือไฟล์เกินกำหนด |
| `permission denied` จาก Supabase | RLS policy หรือสิทธิ์ Data API ยังไม่อนุญาต query นั้น |
| เว็บบน GitHub Pages เปิดแล้วว่าง | ค่า `base` ใน Vite ไม่ตรงกับชื่อ repository หรือ workflow build ไม่สำเร็จ |
| Agent วนแก้ไม่จบ | หยุด แล้วเริ่ม conversation ใหม่ อ้างอิง `@SPEC.md` และระบุปัญหาให้แคบลง |
| แอปช้าเมื่อข้อมูลเยอะ | ไม่ได้ใส่ `limit()` ใน query → เพิ่ม pagination |

### ง. ลิงก์อ้างอิง

- Google Antigravity — https://antigravity.google/
- เอกสาร — https://antigravity.google/docs/home
- Codelab เริ่มต้น — https://codelabs.developers.google.com/getting-started-google-antigravity
- Supabase — https://supabase.com
- Supabase Docs — https://supabase.com/docs
- GitHub Pages — https://docs.github.com/pages

---

## 7. หมายเหตุสำหรับวิทยากร

1. **อย่ารีบข้าม S2** — ถ้าเวลาไม่พอ ให้ตัดฟีเจอร์ในช่วงบ่าย (เช่น ตัดระบบแจ้งเตือน) แต่ห้ามตัดช่วงออกแบบ flowchart เพราะเป็นสาระสำคัญของหลักสูตร
2. **เตรียม branch สำรองทุก checkpoint** — คนที่ตกขบวนให้ `git clone` มาต่อได้ ไม่ให้ใครนั่งดูเฉย ๆ
3. **เน้นย้ำตลอดวันว่า Agent ผิดพลาดได้** ผู้เรียนต้องกล้าอ่าน กล้าแย้ง กล้าสั่งให้ทำใหม่
4. **ปรับกรณีศึกษาได้ตามผู้เรียน** — โครงสร้างเดียวกันนี้ใช้กับ ระบบยืม-คืนครุภัณฑ์, ระบบจองห้องประชุม, ระบบรับเรื่องร้องเรียน หรือระบบสำรวจภาคสนาม ได้ทันที เพียงเปลี่ยน entity และ state diagram
