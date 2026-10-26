# Thesis Skills

สกิลสำหรับเขียน **วิทยานิพนธ์ รายงานสหกิจศึกษา และเล่มวิจัย** ภาษาไทย — ตั้งแต่จัดรูปแบบ `.docx` ให้ตรงแม่แบบของหน่วยงาน ไปจนถึงปรับถ้อยคำให้อ่านเหมือนคนเขียน

รวม 2 สกิล

| สกิล | ทำอะไร |
|---|---|
| [`thesis-report-writer`](thesis-report-writer/SKILL.md) | เขียน/ขยาย/จัดรูปแบบ/ตรวจเล่มวิทยานิพนธ์และรายงานสหกิจศึกษา (`.docx`) ตาม house style ของหน่วยงาน — ขนาดกระดาษ ขอบ ฟอนต์ หัวข้อ ระยะย่อหน้า โครงบท ตาราง/รูปพร้อมคำบรรยาย เลขหน้า สารบัญ พร้อมตัวตรวจ compliance ที่รันซ้ำได้ |
| [`humanizer-th`](humanizer-th/SKILL.md) | แก้ข้อความภาษาไทยที่ดูเหมือน AI เขียน ให้อ่านเหมือนคนเขียน โดยไม่เปลี่ยนสาระและไม่เพิ่มข้อมูลที่ไม่มีในต้นฉบับ — 36 รูปแบบที่ต้องจับ (26 สากล + 10 เฉพาะไทย) พร้อมคู่มือภาษาไทยรายชนิดเอกสาร |

## ติดตั้ง

### Skills CLI (แนะนำ)

```bash
npx skills add <owner>/thesis-skills --global --agent '*'
```

### Claude Code plugin marketplace

```bash
/plugin marketplace add <owner>/thesis-skills
/plugin install thesis-report-writer@thesis-skills
/plugin install humanizer-th@thesis-skills
```

### คัดลอกโฟลเดอร์ด้วยมือ

คัดลอก `thesis-report-writer/` และ/หรือ `humanizer-th/` ไปไว้ในโฟลเดอร์สกิลของเอเจนต์ที่ใช้ เช่น `~/.agents/skills` หรือ `~/.claude/skills`

## การใช้งาน

### เขียนเล่ม / จัดรูปแบบ

```
ช่วยร่างบทที่ 3 ของวิทยานิพนธ์ตามแม่แบบของคณะ แล้วตรวจว่าไฟล์ผ่านกฎการจัดรูปแบบทั้งหมด
```

```
จัดรูปแบบรายงานสหกิจเล่มนี้ใหม่ให้ตรง template.docx แล้วรัน compliance check
```

สกิลจะหา house style ตามลำดับ: ไฟล์กฎที่เขียนไว้ → ไฟล์แม่แบบ `.docx` → โปรไฟล์ปริยายที่แถมมา (สไตล์วิทยานิพนธ์ไทย) แล้วสร้างเอกสารด้วยสคริปต์และตรวจด้วย `check_report.py` จนผ่านทุกข้อ

### ปรับภาษาไทย

```
แก้ข้อความนี้ให้เป็นธรรมชาติ ไม่ต้องเปลี่ยนสาระ
```

```
นี่คืออีเมลถึงลูกค้า ช่วยปรับให้สุภาพแต่ตรงประเด็น
```

## ความต้องการของระบบ

- **thesis-report-writer:** Python 3.9+ และไลบรารีใน [`requirements.txt`](requirements.txt)

  ```bash
  pip install -r requirements.txt
  ```

  ถ้าเครื่องมี Microsoft Word ใช้ Word MCP backend ได้ จะได้ fidelity สูงสุดและ refresh field สารบัญได้ในตัว ถ้าไม่มีก็ใช้ Python builder แล้ว refresh field ใน Word ทีหลัง

- **humanizer-th:** ไม่ต้องติดตั้งอะไรเพิ่ม เป็นสกิลเชิงข้อความล้วน

## โครงสร้าง

```
thesis-skills/
├── .claude-plugin/
│   └── marketplace.json
├── thesis-report-writer/
│   ├── .claude-plugin/plugin.json
│   ├── SKILL.md
│   ├── assets/          # โปรไฟล์สไตล์เริ่มต้น + Word master
│   ├── evals/           # กรณีทดสอบ
│   ├── references/      # โครงเล่ม, spec DSL, ตาราง/รูป, Word backend
│   └── scripts/         # build / check / inspect / make_master
├── humanizer-th/
│   ├── .claude-plugin/plugin.json
│   ├── SKILL.md
│   ├── CHANGELOG.md
│   ├── evals/
│   └── references/      # ชนิดเอกสาร, คลังคำ, อักขรวิธี
├── requirements.txt
└── README.md
```

## หมายเหตุ

- โปรไฟล์ที่แถมมากับ `thesis-report-writer` เป็นสไตล์วิทยานิพนธ์ไทย (KMITL คณะวิทยาศาสตร์) ใช้เป็นจุดเริ่มต้นได้ แต่สไตล์ของหน่วยงานอื่นให้แก้โปรไฟล์หรือสกัดจากไฟล์แม่แบบด้วย `inspect_docx.py` — กลไกทั้งหมดไม่ผูกกับสถาบันใดสถาบันหนึ่ง
- `humanizer-th` เผยแพร่ภายใต้สัญญาอนุญาต MIT ตามที่ระบุใน `SKILL.md` และ `plugin.json`
