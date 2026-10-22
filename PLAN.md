# My Life API — خطة المشروع

برنامج بالبايثون بيسجل يومك كله في مكان واحد (المذاكرة والجامعة والنوم والحركة والامتحانات) وبيعرضه في موقع.
تقدر تسجل فيه بصوتك من أليكسا بالعربي، والآيفون بيبعتله النوم والخطوات لوحده.

> الكود كله هتكتبه بنفسك. الملف ده هو الخريطة، وبتعلّم على كل خطوة لما تخلصها `[]`.

---

## الفكرة في صورة واحدة

```
أليكسا (صوت عربي) ─────┐
Shortcuts (نوم وخطوات) ─┼──►  موقعك (Flask + SQLite)  ──►  داشبورد
Focus Mode (مذاكرة) ────┘
```

| الجزء | الأداة | التكلفة |
|---|---|---|
| لغة البرمجة | Python 3 | مجاني |
| الموقع والـ API | Flask | مجاني |
| قاعدة البيانات | SQLite (ملف واحد جوه المشروع) | مجاني |
| الرسومات | Chart.js | مجاني |
| الاستضافة | PythonAnywhere (الخطة المجانية) | مجاني |
| أليكسا | Alexa Skills Kit + مكتبة `flask-ask-sdk` | مجاني |
| الآيفون | تطبيق Shortcuts | مجاني |
| ساعة هواوي | Huawei Health ← Apple Health | مجاني |
| حفظ الكود | Git + GitHub | مجاني |

---

## شكل المشروع في الآخر

```
my-life-api/
├── app.py            ← الموقع والـ API (نقطة البداية)
├── database.py       ← كل التعامل مع قاعدة البيانات
├── alexa_skill.py    ← الكود اللي بيرد على أليكسا
├── templates/        ← صفحات HTML
│   └── index.html
├── static/           ← CSS وجافاسكريبت
├── requirements.txt  ← المكتبات اللي المشروع محتاجها
├── .env              ← الأسرار (API Key)، ومش بيترفع على GitHub
├── .gitignore        ← الملفات اللي Git يتجاهلها
├── README.md         ← تعريف المشروع على GitHub (بالإنجليزي)
└── PLAN.md           ← الملف ده
```

### قاعدة البيانات (٣ جداول)

**activities**: أي نشاط ليه بداية ونهاية
| العمود | مثال |
|---|---|
| id | 1 |
| type | study / university / gym ... |
| subject | فيزيا (اختياري) |
| start_time | 2026-10-22 15:00 |
| end_time | 2026-10-22 17:00 |
| source | alexa / iphone / web |
| notes | (اختياري) |

**exams**
| العمود | مثال |
|---|---|
| id | 1 |
| subject | رياضة ٢ |
| exam_date | 2026-12-15 |
| notes | الفصول ١ لـ ٥ |

**health_daily**: يوم واحد في كل صف
| العمود | مثال |
|---|---|
| date | 2026-10-21 |
| sleep_minutes | 420 |
| steps | 8500 |

---

## المراحل

قاعدة مهمة: **كل خطوة تخلصها اعملها commit**. كده GitHub يبان عليه شغل حقيقي ومتدرج، وده اللي بيفرق في الـ CV.

### المرحلة ٠: تجهيز الجهاز
هتتعلم: تجهيز بيئة شغل حقيقية.
- [x] Python 3.11 (متسطب عندك)
- [x] VS Code (متسطب عندك). اتأكد إن الـ Python extension موجود
- [x] Git (متسطب عندك)
- [x] عمل حساب على GitHub (بحساب جوجل)
- [x] الاسم في Git: `Ammar`
- [x] الإيميل في Git: نفس إيميل حساب GitHub

### المرحلة ١: هيكل المشروع وGitHub
هتتعلم: virtual environment، وpip، وأساسيات Git.
- [ ] فتح فولدر `my-life-api` في VS Code
- [ ] عمل virtual environment: `python -m venv venv`
- [ ] تشغيله: `venv\Scripts\activate`
- [ ] تسطيب Flask: `pip install flask`
- [ ] عمل `.gitignore` (يتجاهل: `venv/` و`.env` و`*.db` و`__pycache__/`)
- [ ] `git init` وأول commit
- [ ] عمل repo على GitHub ورفع المشروع (`git remote add` و`git push`)

### المرحلة ٢: أول موقع بـ Flask
هتتعلم: يعني إيه سيرفر، وroute، وrequest وresponse.
- [ ] `app.py` يعرض "أهلًا" على `http://localhost:5000`
- [ ] route تاني بيرجع JSON
- [ ] commit: `Add basic Flask app`

### المرحلة ٣: قاعدة البيانات
هتتعلم: SQL، وsqlite3 في بايثون، وتقسيم الكود على ملفات.
- [ ] `database.py` فيه دالة بتعمل الجداول التلاتة لو مش موجودة
- [ ] دالة `add_activity(...)` ودالة `get_activities(date)`
- [ ] دالة `add_exam(...)` ودالة `get_upcoming_exams()`
- [ ] دالة `save_health_day(...)` (لو اليوم موجود تحدّثه بدل ما تكرره)
- [ ] تجربة الدوال من ملف تجارب صغير
- [ ] commit: `Add SQLite database layer`

### المرحلة ٤: الـ API
هتتعلم: REST API، وJSON، والتحقق من البيانات، والأمان بـ API Key.
- [ ] `POST /api/activities`: يسجل نشاط
- [ ] `GET  /api/activities?date=2026-10-22`: نشاطات يوم معين
- [ ] `POST /api/exams` و`GET /api/exams`
- [ ] `POST /api/health`: النوم والخطوات (ده اللي الآيفون هيكلمه)
- [ ] رفض أي طلب مالوش هيدر `X-API-Key` صح (والمفتاح متخزن في `.env`)
- [ ] تجربة كل endpoint (من Thunder Client في VS Code أو `curl`)
- [ ] `pip freeze > requirements.txt`
- [ ] commit: `Add REST API with API key auth`

### المرحلة ٥: الداشبورد
هتتعلم: HTML templates (Jinja)، وChart.js، وتجميع البيانات.
- [ ] صفحة النهاردة: كل النشاطات ومجموع ساعات كل نوع
- [ ] رسم ساعات المذاكرة في آخر ٧ أيام
- [ ] رسم النوم والخطوات في آخر ٧ أيام
- [ ] عد تنازلي للامتحانات الجاية
- [ ] فورم صغير تضيف منه امتحان أو نشاط بإيدك (احتياطي)
- [ ] حماية الصفحة بكلمة سر بسيطة
- [ ] commit: `Add dashboard`

### المرحلة ٦: رفع الموقع على النت (PythonAnywhere)
هتتعلم: deployment، وWSGI، ومتغيرات البيئة على السيرفر.
- [ ] حساب مجاني على pythonanywhere.com
- [ ] `git clone` للمشروع من GitHub جوه PythonAnywhere
- [ ] عمل virtualenv وتسطيب `requirements.txt`
- [ ] إعداد Web app من نوع Flask وتظبيط ملف WSGI
- [ ] الموقع يفتح على `https://USERNAME.pythonanywhere.com`
- [ ] تحط في الكالندر تذكير كل ٣ شهور تدوس "Extend" عشان الموقع مايقفش
- [ ] من هنا ورايح أي تعديل: تعمل `git push` من جهازك وبعدين `git pull` على PythonAnywhere

### المرحلة ٧: Skill أليكسا بالعربي (قلب المشروع)
هتتعلم: voice interfaces، وintents وslots، والتعامل مع API خارجي.
- [ ] حساب على developer.amazon.com (بنفس إيميل أليكسا اللي عندك)
- [ ] Custom Skill جديدة، واللغة Arabic (SA)، ونوع الـ backend: **Provision your own**
- [ ] اسم الاستدعاء، مثلًا: **يومياتي**
- [ ] Intents:
  - `LogActivityIntent`: "سجلي إني {activity} {subject} من {start_time} لـ {end_time}"
  - `TodaySummaryIntent`: "ذاكرت كام ساعة النهاردة"
  - `NextExamIntent`: "امتحاني الجاي إمتى"
  - `AddExamIntent`: "عندي امتحان {subject} يوم {date}"
- [ ] Slot type مخصص `ActivityType` (مذاكرة، جامعة، جيم، شغل، خروج...) مع كلمات تانية بنفس المعنى
- [ ] لكل intent تكتب صيغ كتير للجملة، مصري وخليجي
- [ ] `alexa_skill.py`: handlers بـ `ask-sdk-core` و`flask-ask-sdk`، وتربطها بـ route اسمه `/alexa` في `app.py`
- [ ] الـ Endpoint في Alexa Console: `https://USERNAME.pythonanywhere.com/alexa`
- [ ] تجربة في تبويب Test في الكونسول، وبعدين على جهاز أليكسا بتاعك
- [ ] commit: `Add Arabic Alexa skill`

### المرحلة ٨: الآيفون (Shortcuts)
هتتعلم: automation، وإزاي جهاز يكلم API بتاعك.
- [ ] في Huawei Health: فعّل المزامنة مع Apple Health، واتأكد بعد يوم إن النوم والخطوات بيوصلوا
- [ ] Shortcut اسمه "Sync Health": يجيب نوم امبارح وخطواته ويبعتهم `POST /api/health`
- [ ] Automation يومي الساعة ١٠ الصبح يشغّل "Sync Health"، ومعاه "Run Immediately"
- [ ] Focus Mode اسمه "مذاكرة": لما يشتغل يحفظ الوقت، ولما يقفل يبعت النشاط للـ API
- [ ] commit: تحط الشرح والسكرين شوتس في الـ README

### المرحلة ٩: إضافات (بعد ما كل حاجة تشتغل)
- [ ] وقت استخدام التلفون (Screen Time): إدخال يومي سريع أو قراءة سكرين شوت بالـ OCR
- [ ] تقرير أسبوعي في الداشبورد
- [ ] أليكسا تفكّرك بالامتحانات
- [ ] README احترافي بالإنجليزي فيه صور وGIF للمشروع وهو شغال

---

## نصايح GitHub

- **عمرك ما ترفع** `.env` ولا أي API Key ولا الداتابيز (`*.db`) فيها بياناتك. الـ `.gitignore` هو اللي بيحميك.
- رسالة الـ commit تبقى بالإنجليزي وتوصف اللي اتعمل: `Add exams endpoint` بدل `update`.
- اعمل commits صغيرة وكتير، أحسن من commit واحد ضخم.
- الـ README (بالإنجليزي) هو أول حاجة أي حد بيشوفها. فيه: المشروع بيعمل إيه، وصورة الداشبورد، والأدوات اللي استخدمتها، وإزاي حد يشغّله.
