# Dashboard Builder

เปลี่ยนโจทย์และข้อมูลของคุณให้เป็น Dashboard ที่มีนิยามตัวเลขชัดเจน ใช้ filter ได้จริง และมีหลักฐานการตรวจงาน

ใช้ **Codex** ช่วยเก็บความต้องการ เตรียมโปรเจกต์ เขียนโค้ด และตรวจผล ผ่านสกิลเดียวชื่อ **`dashboard-builder`** เริ่มได้ทั้งโปรเจกต์ใหม่และ Dashboard ที่มีอยู่แล้ว พร้อมบันทึกการตัดสินใจไว้กลับมาทำต่อ

[เริ่มใช้งาน](#เริ่มใช้งาน) · [ขั้นตอนการทำงาน](#จากโจทย์สู่-dashboard) · [ตัวอย่างคำสั่ง](#ตัวอย่างคำสั่งที่ใช้บ่อย) · [โครงสร้างไฟล์](#โครงสร้างไฟล์) · [การตรวจคุณภาพ](#การตรวจคุณภาพ)

## ปัญหาที่สกิลนี้ช่วยแก้

การสั่ง AI ว่า “ทำ Dashboard ให้หน่อย” อาจได้หน้าจอที่ดูเรียบร้อย แต่ยังไม่ตอบคำถามที่ต้องใช้ตัดสินใจ ตัวเลขแต่ละส่วนอาจใช้เงื่อนไขต่างกัน หรือ filter เปลี่ยนกราฟแต่ไม่เปลี่ยนการ์ดสรุป

สกิลนี้เริ่มจากผู้ใช้งาน คำถาม และแหล่งข้อมูล แล้วระบุสูตร KPI กับพฤติกรรมของแต่ละส่วนก่อนลงมือทำ เมื่อสร้างเสร็จจึงตรวจทั้งข้อมูล การใช้งาน และข้อกำหนดของโปรเจกต์

Repo นี้เก็บ **คำแนะนำสำหรับ agent และ template** ส่วนโค้ด Dashboard จะถูกสร้างในโปรเจกต์ที่คุณเลือก ยังไม่มีแอป Dashboard สำเร็จรูปให้เปิดจาก repo นี้

## สิ่งที่คุณจะได้

- **Onboarding** — ช่วยระบุว่าใครใช้ Dashboard ต้องการตอบคำถามอะไร และมีข้อมูลอะไรอยู่แล้ว
- **Project setup** — เตรียมโปรเจกต์ใหม่ หรือใช้ framework และเครื่องมือของโปรเจกต์เดิม
- **Dashboard contract** — ระบุความหมาย สูตร หน่วย ช่วงเวลา และเงื่อนไขของ KPI กับ filter
- **Working dashboard** — สร้างทีละส่วนที่ใช้งานได้ ตั้งแต่ข้อมูลถึงการแสดงผลและการโต้ตอบ
- **Verification record** — บันทึกสิ่งที่ตรวจผ่าน ตรวจไม่ผ่าน และยังไม่ได้ตรวจ
- **Project memory** — เก็บโจทย์ การตัดสินใจ และงานค้างไว้สำหรับ session ถัดไป

ผลลัพธ์ขึ้นกับขอบเขตที่ขอและการเข้าถึงข้อมูล หากขอเฉพาะ setup งานจะจบที่โปรเจกต์ตั้งต้น หากข้อมูลจริงยังเชื่อมต่อไม่ได้ สกิลต้องระบุข้อจำกัดนั้นอย่างชัดเจน

## จากโจทย์สู่ Dashboard

**Onboarding → Setup → Specification → Build → Verify**

| ขั้นตอน | Agent ทำอะไร | สิ่งที่ควรเห็นเมื่อจบขั้น |
|---|---|---|
| Onboarding | อ่านไฟล์เดิม แล้วถามเฉพาะข้อมูลสำคัญที่ยังขาด | เป้าหมาย ผู้ใช้ แหล่งข้อมูล และขอบเขตที่เข้าใจตรงกัน |
| Setup | เลือกหรือใช้ stack เดิม เตรียม dependencies และ configuration | เปิดโปรเจกต์ในเครื่องได้ หรือมีรายการสิ่งที่ยังติดขัดชัดเจน |
| Specification | กำหนดสูตร KPI, filter, สถานะหน้าจอ และตัวอย่างผลที่ถูกต้อง | ข้อกำหนดที่ใช้ตรวจงานได้ |
| Build | ทำข้อมูล → metric → view → filter ให้ครบหนึ่งส่วน ก่อนขยายต่อ | ส่วนที่ทำงานจริงและเชื่อมโยงกัน |
| Verify | เทียบตัวเลขกับข้อมูล ทดลองใช้งาน และรัน checks ที่เกี่ยวข้อง | ผลตรวจพร้อมหลักฐานและข้อจำกัด |

Prototype ใช้เมื่อยังต้องตอบคำถามเรื่องหน้าตาหรือ interaction ส่วนโปรเจกต์ที่มีแบบชัดเจนแล้วสามารถเดินหน้าลงมือทำตามขอบเขตได้

## เริ่มใช้งาน

ต้องมี **Codex ที่พร้อมใช้งาน** และ **Git** สำหรับวิธี clone ด้านล่าง หรือเลือก **Code → Download ZIP** บน GitHub แล้วแตกไฟล์แทนได้ เครื่องมือสำหรับรัน Dashboard เช่น Node.js จะเลือกและตรวจในขั้น setup ตามโปรเจกต์จริง

### 1. ดาวน์โหลดสกิล

```bash
git clone https://github.com/nutdnuy/dashboard-builder.git
cd dashboard-builder
```

### 2. ติดตั้งใน Codex

คัดลอกโฟลเดอร์ `skills/dashboard-builder` ไปไว้ในโฟลเดอร์ skills ของ Codex โดยต้องได้โครงสร้าง `dashboard-builder/SKILL.md` พร้อมไฟล์ประกอบทั้งหมด

**macOS / Linux** — รันจากโฟลเดอร์ repo:

```bash
dashboard_skills_dir="${CODEX_HOME:-$HOME/.codex}/skills"
mkdir -p "$dashboard_skills_dir"
if [ -e "$dashboard_skills_dir/dashboard-builder" ] || [ -L "$dashboard_skills_dir/dashboard-builder" ]; then
  echo "dashboard-builder already exists. Review the existing installation before updating."
else
  cp -R skills/dashboard-builder "$dashboard_skills_dir/dashboard-builder"
fi
```

คำสั่งนี้คงสกิลที่ติดตั้งไว้แล้ว รวมถึง symlink เดิม หากต้องการอัปเดต ให้ตรวจต้นฉบับที่การติดตั้งนั้นใช้อยู่ก่อน เพื่อรักษาการปรับแต่งของคุณ

<details>
<summary>ติดตั้งด้วยการคัดลอกโฟลเดอร์ หรือใช้ Windows</summary>

1. เปิดโฟลเดอร์ที่ clone หรือแตก ZIP ไว้
2. คัดลอกโฟลเดอร์ `dashboard-builder` ที่อยู่ภายใน `skills/`
3. วางไว้ใน `skills` ใต้ตำแหน่ง `CODEX_HOME` ของคุณ ถ้าไม่ได้ตั้งค่านี้ ค่าเริ่มต้นคือ `.codex/skills` ในโฟลเดอร์ผู้ใช้
4. ตรวจว่าไฟล์ `SKILL.md`, `references/`, `assets/` และ `agents/` อยู่ครบ
5. หากมีโฟลเดอร์หรือ symlink ชื่อเดียวกันอยู่แล้ว ให้ตรวจการติดตั้งเดิมก่อนแทนที่

</details>

ไม่ต้องติดตั้งชุด Matt Pocock เพิ่ม สกิลนี้รวมขั้นตอนที่ปรับใช้แล้วไว้ในตัว

### 3. เปิดโปรเจกต์ที่จะทำ Dashboard

เปิดโฟลเดอร์โปรเจกต์เป้าหมายใน Codex แล้วเริ่มแชตสำหรับงานนั้น ถ้ายังไม่มีโปรเจกต์ ให้เลือก workspace ที่จะสร้างงานใหม่ พร้อมระบุชื่อหรือโฟลเดอร์ปลายทางในคำขอ

เตรียมข้อมูลเท่าที่มี เช่น CSV, ตัวอย่าง schema, เอกสาร API หรือโค้ด Dashboard เดิม ไม่ต้องเลือกทุก library ล่วงหน้า

### 4. เริ่ม onboarding และ setup

พิมพ์ในบทสนทนา Codex:

```text
Use $dashboard-builder to build a dashboard for my sales team.
Start with onboarding and setup. My data is in sales.csv.
```

แทน `sales.csv` ด้วยไฟล์จริงที่ agent เข้าถึงได้ หรือบอกแหล่งข้อมูลของคุณ สกิลจะอ่านบริบทที่มี แล้วถามเฉพาะสิ่งที่ยังจำเป็นต่อการทำงาน

ถ้าต้องการเตรียมโปรเจกต์ก่อน โดยยังไม่สร้าง Dashboard:

```text
Use $dashboard-builder for onboarding and setup only.
```

**สิ่งที่ควรตรวจหลัง setup:** เปิดโปรเจกต์ได้ตามคำสั่งที่บันทึกไว้ รู้ว่าใช้ข้อมูลจริงหรือข้อมูลตัวอย่าง และทราบว่ายังต้องเตรียมข้อมูลหรือสิทธิ์เข้าถึงอะไรเพิ่มเติม

## ตัวอย่างคำสั่งที่ใช้บ่อย

ทั้งหมดเป็น prompt สำหรับสกิลเดียว ใช้ในบทสนทนา Codex ไม่ใช่คำสั่ง shell หรือ slash command แยกหลายตัว

| ต้องการทำอะไร | Prompt ตัวอย่าง |
|---|---|
| สร้าง Dashboard ใหม่ | `Use $dashboard-builder to build a dashboard from this CSV. Start with onboarding and setup.` |
| ทำเฉพาะ onboarding และ setup | `Use $dashboard-builder for onboarding and setup only.` |
| เพิ่ม filter ในงานเดิม | `Use $dashboard-builder to add date and category filters to this dashboard.` |
| เชื่อมแหล่งข้อมูลจริง | `Use $dashboard-builder to connect this dashboard to the API described in these docs.` |
| ตรวจตัวเลขกับพฤติกรรม | `Use $dashboard-builder to review this dashboard against its metric definitions and requirements.` |
| ทำงานต่อจากครั้งก่อน | `Use $dashboard-builder to resume this project from its project record and remaining tasks.` |

ตัวอย่างโจทย์ที่ให้บริบทได้ดี:

```text
Use $dashboard-builder to build a sales dashboard from sales.csv.
Audience: the sales manager.
Main question: which regions and products explain the change in sales?
Required controls: date range, region, and product category.
Start with onboarding and setup, and clarify any missing metric definitions.
```

## Onboarding จะเก็บข้อมูลอะไร

| เรื่อง | ตัวอย่าง |
|---|---|
| ผู้ใช้และการตัดสินใจ | ผู้จัดการฝ่ายขายต้องหาสาเหตุที่รายได้ลดลง |
| ข้อมูล | ไฟล์ CSV, API, database หรือแหล่งข้อมูลเดิมในโปรเจกต์ |
| Metric | Revenue หมายถึงยอดก่อนหรือหลังส่วนลด รวมรายการคืนสินค้าหรือไม่ |
| เวลาและความสด | ใช้เขตเวลาอะไร อัปเดตรายวันหรือเมื่อกด refresh |
| การใช้งาน | ดูบน desktop หรือมือถือ ต้องกรองและเปรียบเทียบอะไร |
| ขอบเขตส่งมอบ | setup อย่างเดียว, Dashboard ในเครื่อง หรือ deploy ตามที่ร้องขอ |

ถ้ามีคำตอบอยู่ในโปรเจกต์หรือบทสนทนาแล้ว สกิลจะใช้ข้อมูลนั้น โปรเจกต์ใหม่ใช้ `docs/dashboard/project.md` เป็นบันทึกตั้งต้น ส่วนโปรเจกต์เดิมให้ใช้โครงสร้างเอกสารที่มีอยู่

## ปรับให้เข้ากับงานของคุณ

| อยากปรับอะไร | เริ่มที่ไหน |
|---|---|
| เป้าหมาย, KPI, filter และงานค้าง | Project record ในโปรเจกต์ Dashboard |
| พฤติกรรมการ onboarding และ setup | [onboarding-setup.md](skills/dashboard-builder/references/onboarding-setup.md) |
| กติกาข้อมูลและการตรวจงาน | [data-and-verification.md](skills/dashboard-builder/references/data-and-verification.md) |
| แบบบันทึกโปรเจกต์ | [project-brief.md](skills/dashboard-builder/assets/project-brief.md) |
| ขั้นตอนหลักของสกิล | [SKILL.md](skills/dashboard-builder/SKILL.md) |

โปรเจกต์เดิมใช้ framework, package manager และ design system เดิมเป็นหลัก สำหรับเว็บ Dashboard ใหม่ที่ไม่มีข้อกำหนดด้าน server สกิลเสนอ React + TypeScript + Vite เป็นจุดเริ่มต้น และตรวจข้อกำหนดปัจจุบันเมื่อ setup หากคุณระบุ stack อื่นให้ใช้ตามนั้น

## โครงสร้างไฟล์

```text
dashboard-builder/
├── README.md
├── Read.md
├── LICENSE
└── skills/
    └── dashboard-builder/
        ├── SKILL.md
        ├── SOURCE.md
        ├── LICENSE.txt
        ├── agents/
        │   └── openai.yaml
        ├── assets/
        │   └── project-brief.md
        └── references/
            ├── onboarding-setup.md
            └── data-and-verification.md
```

`agents/openai.yaml` เป็น metadata สำหรับแสดงสกิลใน Codex ส่วน `assets/project-brief.md` เป็น template สำหรับบันทึกโปรเจกต์ ไม่ใช่ข้อมูล Dashboard ตัวอย่าง

## การตรวจคุณภาพ

**ตรวจตัวเลขกับข้อมูลต้นทาง** — กำหนดสูตร หน่วย ขอบเขต filter และตัวอย่างผลที่คำนวณแยกไว้ก่อน ตรวจเรื่อง null, duplicate, denominator และช่วงเวลาตามความเสี่ยงของ metric

**ตรวจสิ่งที่ผู้ใช้ทำได้จริง** — เปลี่ยน filter แล้วตรวจส่วนที่ได้รับผล ทดลอง reset และสถานะข้อมูลว่างหรือผิดพลาด รวมถึงดูหน้าจอและการใช้งานด้วย keyboard ตามขอบเขต

**แยกผลตรวจสองด้าน** — Requirements ตรวจว่าตรงโจทย์และตัวเลขถูกต้อง ส่วน Engineering ตรวจมาตรฐานโค้ดและความสามารถในการดูแลต่อ

**รายงานตามหลักฐาน** — การ build ผ่านยังไม่ยืนยันว่าตัวเลขถูกหรือหน้าเว็บใช้งานได้ หากไม่มี browser ให้ตรวจ ต้องระบุว่าการตรวจหน้าจอและ interaction ยังไม่เกิดขึ้น

สถานะของสกิลชุดนี้: ผ่านการตรวจโครงสร้าง YAML, ลิงก์ไฟล์ และการติดตั้ง Codex ในเครื่องผู้พัฒนา พร้อมทบทวน workflow ด้วยการอ่านคำสั่ง แต่ **ยังไม่ได้ทดลองใช้สร้าง Dashboard จริงครบกระบวนการ** จึงยังไม่มีผลทดสอบ end-to-end ให้ใช้อ้างอิง

## ข้อมูลส่วนตัวและการเผยแพร่

เก็บ credential ในฝั่ง server หรือ secret store ที่เหมาะสม หลีกเลี่ยงการใส่ key ลงใน frontend, fixture หรือเอกสารที่เผยแพร่ ระบุให้ชัดเมื่อใช้ข้อมูลตัวอย่างแทนข้อมูลจริง

สกิลรองรับการทำงานในเครื่อง การสร้าง repository, ส่งข้อมูลขึ้น tracker, ตั้งงาน refresh อัตโนมัติ หรือ deploy เป็นงานเพิ่มเติมตามขอบเขตที่ผู้ใช้ร้องขอ

## ที่มาและเครดิต

ปรับใช้แนวทางจาก [mattpocock/skills](https://github.com/mattpocock/skills):

| แนวทางต้นทาง | นำมาใช้กับ Dashboard อย่างไร |
|---|---|
| `setup-matt-pocock-skills` | สำรวจโปรเจกต์ก่อนตั้งค่า และเก็บบริบทสำหรับใช้งานต่อ |
| `grilling` | ถามเพื่อคลี่คลายการตัดสินใจที่ยังขาด |
| `to-spec` | สรุปโจทย์เป็นข้อกำหนดที่ตรวจได้ |
| `prototype` | ทดลองเพื่อตอบคำถามเรื่องหน้าตาหรือ interaction |
| `tdd` | ทำทีละส่วนและทดสอบพฤติกรรมด้วยผลคาดหวังที่คำนวณแยก |
| `code-review` | แยกการตรวจความตรงโจทย์ออกจากคุณภาพทางวิศวกรรม |

มีแนวคิดประกอบจาก `wizard` และ `writing-for-agents` รายละเอียด commit ต้นทางและสิ่งที่ปรับเปลี่ยนอยู่ใน [SOURCE.md](skills/dashboard-builder/SOURCE.md) สกิลนี้เป็นงานดัดแปลง ไม่ใช่ release ทางการหรือการรับรองจาก Matt Pocock

โครงสร้างการนำเสนอ README ได้แรงบันดาลใจจาก [llm-wiki-starter ของ Migchw](https://github.com/Migchw/llm-wiki-starter/blob/master/README.md) โดยเขียนเนื้อหาสำหรับ Dashboard Builder ขึ้นใหม่

เผยแพร่ภายใต้ [MIT License](LICENSE) และคงประกาศลิขสิทธิ์ต้นทางไว้

## ร่วมพัฒนา

แจ้งปัญหาที่ [Issues](https://github.com/nutdnuy/dashboard-builder/issues) พร้อม prompt ที่ใช้ ผลที่คาดหวัง สิ่งที่เกิดขึ้น และตัวอย่างข้อมูลที่แบ่งปันได้ หรือส่ง PR ที่ปรับปรุงปัญหาหนึ่งเรื่องต่อครั้ง

ผลทดลองใช้สกิลสร้าง Dashboard จริงจะช่วยให้พัฒนาคำสั่งจากพฤติกรรมที่สังเกตได้ กรุณาแยกข้อผิดพลาดของสกิลออกจากปัญหา dependencies, สิทธิ์เข้าถึงข้อมูล และการตั้งค่าโปรเจกต์
