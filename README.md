# مجلس رواية صحيح البخاري — مسجد النعمان بن بشير

نظام تفقد وحضور تراكمي، مع تسجيل وقت الحضور ووقت بدء كل مجلس، ومزامنة عبر Google Sheets.

- **الموقع الحي:** https://masjed-alnuman.github.io/saheh-albukhari/
- **المستودع:** https://github.com/masjed-alnuman/saheh-albukhari
- **الإصدار:** 2.4.0

## حالة النشر الحالية

- **مشروع Apps Script:** «مزامنة حضور مجلس البخاري» (منشور ومربوط)
  - scriptId: `1ls6NSOkflUwJ1Y2jSeiF_f84fuShLFUXFK3SuzEDSyAfPwCpLFC_lh6k`
  - Web App: `https://script.google.com/macros/s/AKfycbznlROSbs0W-jliySIEfgNovTe2BsN2U6BBSlMvmdCz9Psm0NZ7QZ9gHFIK3IVp2IIBLQ/exec`
  - الصلاحية: `ANYONE_ANONYMOUS` / ينفّذ باسم `USER_DEPLOYING`
- **الشيت:** «سجل حضور مجلس صحيح البخاري»
  - ID: `1xZC_GGDVyBeoIIMVZ5-D_QOrMrDL8j45KTIOdkeYUJk`
- الرابط القديم محفوظ في `LEGACY_WEBHOOKS` داخل `index.html` ويتم ترحيله تلقائياً على أي جهاز.

---

## الملفات

| المسار | الوظيفة | يُرفع على GitHub؟ |
|---|---|---|
| `index.html` | الموقع كامل (واجهة + منطق + كود Apps Script) | ✅ نعم |
| `logo.jpg` | شعار المسجد | ✅ نعم |
| `apps-script-Bukhari.gs` | نسخة كود Google Apps Script للصق في الشيت | ❌ لا |
| `_backup/index-v1.html` | النسخة القديمة من الموقع (احتياط) | ❌ لا |
| `_tools/` | أدوات تطوير (Python) للنشر والفحص | ❌ لا |
| `_tools/.secrets/` | **بيانات سرية** (توكن Google + بيانات OAuth) | ❌ **أبداً** |

> ⚠️ لا ترفع مجلد `_tools` أو `_backup` أو `desktop.ini` إلى GitHub.
> الموقع يحتاج فقط `index.html` و`logo.jpg`.

---

## النشر (تحديث الموقع)

1. افتح المستودع على GitHub ← **Add file** ← **Upload files**.
2. اسحب `index.html` فقط ← **Commit changes**.
3. انتظر دقيقة، ثم افتح الموقع الحي وتحقق من ظهور «الإصدار 2.2.0» في الفوتر.

> يوجد توكن GitHub `public_repo` مستخدم سابقاً (تم إلغاؤه). لا تحفظ توكنات داخل هذا المجلد.

---

## إعداد Google Apps Script

الكود موجود داخل `index.html` (تبويب الإعدادات ← «كود Google»)، ونسخة مستقلة في `apps-script-Bukhari.gs`.

**الطريقة اليدوية:**
1. افتح الشيت ← **Extensions** ← **Apps Script**.
2. امسح الكود القديم والصق الجديد، ثم احفظ.
3. **Deploy** ← **Manage deployments** ← ✏️ ← **Version: New version** ← **Deploy**.
4. تأكد `Who has access = Anyone`.

**الطريقة البرمجية (أدوات المشروع):**
```powershell
python _tools\check_api.py          # هل Apps Script API مفعّل؟
python _tools\oauth_google.py       # موافقة لمرة واحدة (يفتح رابطاً)
python _tools\deploy_apps_script.py # إنشاء/تحديث المشروع ونشره
```
- يجب تفعيل Apps Script API من: https://script.google.com/home/usersettings
- الشيت المستهدف: `سجل حضور مجلس صحيح البخاري`
  (ID: `1xZC_GGDVyBeoIIMVZ5-D_QOrMrDL8j45KTIOdkeYUJk`)

---

## QR الحضور عند الباب

- زر **«ملصق QR»** يفتح رمزاً واحداً للمجلس كله، مع زر طباعة ملصق A4 جاهز للتعليق.
- رابط الملصق: `https://masjed-alnuman.github.io/saheh-albukhari/?gate=1`
- الطالب يمسحه ← يكتب اسمه أو رقمه ← يختار اسمه من القائمة ← **إرسال**.
- تظهر له رسالة: «تم تسجيل الحضور ✓» مع المجلس والتاريخ والساعة، و«من البداية» أو «+N دقائق».
- يسجّل الحضور تلقائياً في الشيت عبر نفس المزامنة.
- زر **«مسح QR»** يبقى متاحاً للمشرف لمسح رموز الطلاب الفردية (من بطاقة الطالب ← «رمز QR»).

## ملاحظات تشغيلية

- البيانات تُحفظ محلياً في `localStorage` أولاً، ثم تُزامن مع Google Sheets.
- وقت الحضور يُسجَّل تلقائياً عند الضغط على «حاضر».
- وقت بدء الدرس يُضبط من زر الساعة (في شريط الأدوات أو رأس عمود الخميس).
- «من البداية» تظهر لمن سُجِّل قبل وقت البدء، و`+N د` لمن تأخر.
- الجدول يعرض آخر ١٢ أسبوعاً افتراضياً (يمكن اختيار «كل الأسابيع»)، وكل البيانات محفوظة.
- نسخ احتياطي: نسخ محلية تلقائية + تنزيل JSON + أوراق Excel.
- كود Google يحتفظ بنسخة احتياطية داخل الشيت (`_حالة_المزامنة_نسخة`) ويسترجعها عند تلف الحالة الأساسية.

---

## أوامر مفيدة

```powershell
# تحديث ملف الكود المستقل من داخل index.html بعد أي تعديل
python _tools\extract_gs.py

# عرض شيتات Drive للعثور على الشيت
python _tools\find_sheet.py
```
