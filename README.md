here# MASTER PROMPT — منصة Interview Ready (Enterprise Edition v2)
### مبني على تحليل كامل لـ index.html + الـ 3 نسخ CV + معايير الأمان المرفقة

---

## 0) الشخصية المطلوب تقمصها (Multi-Expert Persona)

أنت فريق افتراضي مدمج في عقل واحد يضم: **Principal Software Architect** + **Principal UX/UI Designer** + **HR Director (توظيف تقني عالمي)** + **عالم نفس سلوكي متخصص في مقابلات العمل** + **CTO بخبرة +25 سنة** + **AI Solutions Architect** + **مستشار مالي وتفاوض رواتب** + **Security Engineer**. اكتب كودًا يبدو مكتوبًا يدويًا بواسطة Senior Engineer حقيقي، وليس ناتج AI عشوائي — ونفّذ المطلوب فعليًا بدل الشرح النظري.

---

## 1) الهدف

بناء **Single Page Application** كامل داخل `index.html` واحد (HTML + CSS + JS فقط)، منصة تجهيز لمقابلات العمل التقنية، بهوية بصرية **مطابقة حرفيًا** لموقع البورتفوليو الحالي (moh222salah.github.io/cv)، تخدم شخصية محمد صلاح كمرشح لأدوار: **Senior Full Stack Developer / ERPNext & Frappe Consultant / AI Automation & LLM Engineer**.

---

## 2) نظام التصميم (مأخوذ حرفيًا من index.html — Design Tokens الإلزامية)

```css
--ink:#0B0E14; --ink-2:#10141C; --ink-3:#161B26; --ink-4:#1C2230;
--paper:#F7F5F0; --paper-2:#FFFFFF;
--verified:#1A6E5C; --verified-light:#2E9A7F;   /* Emerald */
--gold:#C9A24A; --gold-light:#E0BD6E; --gold-dim:#8A6F33;
--text-d:#F4F0E6; --text-d-dim:#9AA3AE;
--text-l:#0B0E14; --text-l-dim:#5A6472;
--disp:'Space Grotesk'; --body:'Inter'; --mono:'JetBrains Mono';
--disp-ar:'Tajawal'; --body-ar:'IBM Plex Sans Arabic';
--r-sm:8px; --r-md:14px; --r-lg:22px; --r-xl:32px;
```

- **الوضع الداكن (افتراضي):** خلفية `--ink` مع طبقات Glass شفافة، Radial gradients ذهبية/زمردية خافتة، حدود `rgba(244,240,230,.08)`.
- **الوضع الفاتح:** خلفية `#FDFDFC` مع نفس الـ radial gradients بشفافية أقل + `backdrop-filter: blur()` على البطاقات (Glassmorphism حقيقي مطابق للملف الأصلي).
- **الخطوط:** إنجليزي = Space Grotesk (عناوين) + Inter (متن) + JetBrains Mono (كود/مصطلحات). عربي = Tajawal (عناوين) + IBM Plex Sans Arabic (متن). تبديل تلقائي للفونت مع تبديل اللغة عبر `data-lang` attribute، وليس نسخ منفصلة من الصفحة.
- **الأيقونات:** مكتبة **Ionicons 7** عبر نفس CDN المستخدم في index.html (`unpkg.com/ionicons@7.1.0`) — بنفس أسلوب `.exp-icon-box` ذات الخلفية Gradient الدائرية (كل قسم يأخذ Gradient مختلف مطابق لأسلوب "orbit-badge" و"exp-icon-box" الموجود في الأصل).
- **الحركة:** GSAP + ScrollTrigger فقط عبر CDN، حركات ناعمة `reveal` + `tilt-card` مطابقة لما هو مطبق بالفعل، بدون أي وميض أو حركة مرهقة للعين. Reduced-motion media query إلزامي.
- **الخلفية:** نفس طبقات `radial-gradient` + `mesh gradient` + `noise texture` الموجودة فعليًا في الملف الأصلي — تُستنسخ لا تُعاد اختراعها.

---

## 3) بنية اللغة والوضع الليلي/النهاري

- زرّان ثابتان في الـ navbar (مطابقين لـ `#themeToggle` و`#langToggle` الموجودين فعليًا): تبديل فوري بدون إعادة تحميل، حفظ التفضيل في `localStorage` (استثناء مسموح به لأنه ليس Artifact بل موقع مستقل مستضاف على GitHub Pages).
- ترجمة كاملة 100% لكل نص عبر نمط `data-en` / `data-ar` + `dir="rtl"/"ltr"` ديناميكي، بنفس أسلوب `.block-i18n` المستخدم بالفعل — **مع تفادي باگ الـ CSS specificity المعروف** (`.block-i18n [data-en],[data-ar]{display:block}` يجب أن يُكتب بترتيب specificity صحيح حتى لا يطغى على `[data-ar]{display:none}` عند التبديل).

---

## 4) الأقسام الرئيسية (Tabs مجمّعة من الفهرس الأصلي الـ60 قسم)

بدلاً من عرض 60 كارت متفرقة، تُجمّع في **7 مجموعات رئيسية (Mega Tabs)** كبطاقات Premium في الصفحة الرئيسية، وكل تاب يحتوي الأقسام الفرعية:

| # | التاب الرئيسي | الأقسام الفرعية بداخله | الأيقونة المقترحة |
|---|---|---|---|
| 1 | **General Interview** | أسئلة عامة، HR، Behavioral، Psychology، Leadership، Management، Communication | `person-outline` |
| 2 | **Full Stack Engineering** | PHP/Laravel، JavaScript/TypeScript، React، Node.js، SQL/MySQL/PostgreSQL، REST API، Authentication، System Design، Architecture، Performance، Security، Testing، Docker/Linux/Git | `code-slash-outline` |
| 3 | **ERPNext & Frappe** | Frappe Framework، Accounting، Manufacturing، CRM، Inventory، HRMS، ZATCA/UBL 2.1/ECDSA/TLV | `layers-outline` |
| 4 | **AI & Automation** | Generative AI، LLMs، Prompt Engineering، RAG، MCP، AI Agents، n8n، OpenAI، Claude، CrewAI، LangChain | `hardware-chip-outline` |
| 5 | **Soft Skills & Career** | Problem Solving، Critical Thinking، Negotiation، Freelancing، LinkedIn، CV Review، Portfolio Review | `sparkles-outline` |
| 6 | **Courses & Certifications** | أسئلة مباشرة عن كل شهادة حقيقية حصل عليها (انظر بند 7) | `ribbon-outline` |
| 7 | **Salary & Financial Negotiation** | تفاوض راتب EGP/SAR، عقود بدون كتابة (درس Ahmed Samy)، تقييم عروض عمل | `cash-outline` |

كل كارت رئيسي يعرض: Icon Gradient دائري، عدد الأسئلة، مستوى الصعوبة الإجمالي، الوقت المقدر، % الإنجاز، Progress Ring دائري متحرك (SVG).

---

## 5) بنية كل سؤال (Accordion فاخر — 13 طبقة إلزامية بالترتيب)

عند فتح أي سؤال (بنفس أسلوب `.t-card.open` glass-card موجود بالأصل):

1. **السؤال** (EN + AR جنبًا لجنب حسب اللغة النشطة)
2. **الإجابة النموذجية** (Model Answer)
3. **الإجابة المختصرة** (30 ثانية)
4. **إجابة احترافية للمقابلة** (STAR method حيث ينطبق)
5. **إجابة بالعامية المصرية** (لتدريب الفهم قبل الحفظ)
6. **Simple English Answer**
7. **Advanced English Answer**
8. **الأخطاء الشائعة** (Common Mistakes)
9. **نصائح للمقابلة** (Interviewer Tips / ما يبحث عنه المُقابِل نفسيًا)
10. **أسئلة متابعة متوقعة** (Follow-up Questions)
11. **درجة الصعوبة** (Badge: Easy/Medium/Hard/Expert) + **المدة المقترحة للإجابة**
12. **تقييم ذاتي** (Self-rating slider 1-5، يُحفظ محليًا)
13. **أزرار الإجراء**: نسخ / إضافة للمفضلة / تمت المراجعة (checkmark أخضر يغيّر حالة الكارت بصريًا)

---

## 6) نظام المصطلحات التقنية (Glossary Badges)

كل مصطلح (REST API, JWT, ERP, OAuth, RAG, LLM, Webhook, MCP, ZATCA, UBL, ECDSA, TLV...) يظهر كـ `<span class="term-badge">` بخط Mono وحد ذهبي رفيع. الضغط عليه يفتح **Modal سريع** (glass modal، بدون إعادة تحميل) يحتوي:
- شرح مبسط جدًا بالعامية المصرية
- English simple explanation
- مثال عملي واحد من مشاريع محمد الحقيقية (مثال: عند شرح ZATCA UBL 2.1 استخدم مثال مشروع **ZATCA Compliance Suite** الفعلي من الـ CV)
- روابط داخلية لمصطلحات مرتبطة (Chip navigation)

---

## 7) مصدر المحتوى الحقيقي (من تحليل الـ 3 CV المرفقة)

المحتوى يجب أن يُبنى على إنجازات حقيقية موثّقة في الـ CVs الثلاثة (ERP/AI/Full Stack) — استخدمها كأمثلة فعلية داخل الإجابات النموذجية بدل أمثلة عامة:

- **General Ledger Report**: خفّض وقت التقفيل الشهري من 3 أيام إلى 4 ساعات (88%)، وفّر +40,000 SAR سنويًا — يُستخدم كمثال إجابة على أسئلة "Performance / SQL Optimization / Business Impact".
- **VIP ACC System**: منصة SaaS محاسبية Multi-Tenant — مثال لأسئلة System Design / Architecture / RBAC.
- **ZATCA Compliance Suite**: UBL 2.1 / ECDSA / TLV QR / FATOORA API — مثال لأسئلة Security/Compliance/Integration.
- **Intelligent Invoice Processing (n8n + OpenAI)**: 300+ مستند يوميًا بدقة تصنيف ~91%، تقليل المعالجة من 6 ساعات لأقل من 30 دقيقة — مثال لأسئلة AI Automation/RAG/Agentic Workflows.
- **AI-Powered Legal Ops Platform (Kuwait)**: تقليل العبء الإداري +70% — مثال لأسئلة Multi-step Agent Orchestration.
- **CampaignOS**: مثال لأسئلة Marketing Automation/WhatsApp & Email API.
- شهادات فعلية (لقسم Courses & Certifications): Frappe (4 شهادات)، Google IT Automation with Python، Microsoft Azure AI Engineer (AI-102)، Anthropic Claude API Fundamentals، DeepLearning.AI (LangChain/RAG/Agents)، Google Cloud Generative AI، AWS Bedrock — كل شهادة تحصل على 3-5 أسئلة مقابلة حقيقية تختبر الفهم الفعلي (ليس الحفظ) للمحتوى.
- درس التفاوض المالي: قصة نزاع العقد الشفهي (بدون الإشارة لاسم العميل) تُستخدم كمثال إجابة حي على سؤال "احكيلي عن موقف صعب مع عميل" ضمن Behavioral/Negotiation.

**ملاحظة مهمة:** لا تُدرج أي بيانات تواصل شخصية (رقم هاتف/إيميل) داخل محتوى الأسئلة والأجوبة — هذه فقط في صفحة "About/Contact" إن وُجدت.

---

## 8) البحث، الفلاتر، الداشبورد، الجيمفيكيشن (كما في الأمر الأصلي — بلا اختصار)

- بحث لحظي (Instant Search) يغطي: السؤال / الإجابة / المصطلحات / الأقسام / الهاشتاجات.
- فلاتر: Difficulty, Category, Language, Completed, Favorites, Recently Opened.
- Dashboard: عدد الأسئلة، عدد الأقسام، % الإنجاز، المفضلة، آخر مراجعة، Streak، Study Time.
- Progress: Linear + Circular Progress، Achievements، Badges، Levels، XP System — كلها محسوبة محليًا (LocalStorage) بدون Backend.
- Export: JSON / Markdown / PDF Layout للسؤال أو القسم.
- Print-friendly view لكل قسم.

---

## 9) معايير الأمان الإلزامية على مستوى الكود (مستخلصة من الصور المرفقة — غير قابلة للتفاوض)

بما أن الموقع يحتوي منطق JS يتعامل مع بيانات المستخدم محليًا (Notes, Favorites, Progress)، طبّق هذه المعايير كـ Engineering Checklist إلزامي قبل التسليم:

1. **لا أسرار في الكود إطلاقًا**: لا API keys أو tokens مكتوبة داخل الـ JS حتى لو كانت لخدمة CDN — أي تكامل مستقبلي مع API خارجي يُبنى بحيث يُدخل المفتاح من طرف المستخدم في وقت التشغيل ولا يُخزَّن في الكود المصدري.
2. **لا تسريب معلومات في الأخطاء**: أي `try/catch` في الـ JS يعرض رسالة عامة للمستخدم (مثال: "حدث خطأ، حاول مجددًا") ولا يعرض تفاصيل تقنية (stack trace, paths) في الواجهة؛ التفاصيل الكاملة تُسجَّل فقط في console أثناء التطوير وتُزال قبل الإنتاج.
3. **Sanitization لأي إدخال مستخدم**: خانة "Notes" و"Self-rating" يجب تنقية مدخلاتها (escape HTML) قبل الحقن في الـ DOM لمنع أي XSS محلي عبر `innerHTML`.
4. **لا تخزين بيانات حساسة في LocalStorage**: يُخزَّن فقط تقدم المستخدم التعليمي (progress, favorites, notes)، ولا يُخزَّن أي بيانات شخصية حساسة.
5. **Dependency hygiene**: كل مكتبة CDN (GSAP, Ionicons, إلخ) تُثبَّت بإصدار محدد (pinned version) وليس `@latest`، لتفادي مفاجآت أمنية أو كسر بصري مستقبلي.
6. **Content Security**: لا تنفيذ لأي كود خارجي عبر `eval()` أو `Function()` مطلقًا.
7. هذه المعايير تُطبَّق بروح "Security by Design" حتى في مشروع Frontend بحت — تحسبًا لأي مرحلة لاحقة يُضاف فيها Backend حقيقي (auth, rate limiting, RLS) عند تحويل المنصة من Static Site إلى SaaS Product قابل للبيع.

---

## 10) القيود التقنية الصارمة

**مسموح:** Pure HTML5 / Pure CSS3 / Pure Vanilla JS + CDN فقط لـ (GSAP, ScrollTrigger, SplitType, Lenis, Ionicons, Swiper عند الحاجة).
**ممنوع تمامًا:** Bootstrap, Tailwind, React, Vue, Angular, jQuery — الالتزام يطابق التكنولوجيا الفعلية المستخدمة في index.html الأصلي (لا مكتبة CSS framework، تصميم يدوي بالكامل بـ CSS Variables + BEM-like naming).

---

## 11) جودة الكود ومعايير الإنتاج

- Semantic HTML5 + ARIA كاملة + Keyboard Navigation + Focus states + High Contrast + prefers-reduced-motion.
- SEO كامل: Meta tags, OpenGraph, Twitter Cards, Schema.org (JSON-LD), Manifest, Robots, Canonical.
- استهداف Lighthouse: Performance 100 / Accessibility 100 / SEO 100 / Best Practices 100.
- تعليقات عربية/إنجليزية واضحة أعلى كل قسم CSS/JS رئيسي، بنية تسمح بفصل لاحق لملفات (styles.css / app.js / data.json) بدون إعادة كتابة.
- عرض المحتوى لا يتجاوز 80-90 حرف في السطر، Focus Reading Mode اختياري لتقليل المشتتات أثناء المراجعة الطويلة.

---

## 12) مخرج التنفيذ

أنشئ الموقع الكامل داخل `index.html` واحد بهذا المستوى، بحيث يبدو امتدادًا طبيعيًا وليس ملحقًا منفصلًا عن البورتفوليو الحالي — نفس اللمسة البصرية، نفس نظام الألوان، نفس نظام الأيقونات، نفس سلوك التبديل بين العربي/الإنجليزي والداكن/الفاتح، لكن بمحتوى ووظيفة مختلفة تمامًا (منصة تدريب مقابلات بدل صفحة سيرة ذاتية).
