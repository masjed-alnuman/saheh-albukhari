# تعليمات المشروع

## نظرة عامة

موقع «مجلس رواية صحيح البخاري» — صفحة واحدة `index.html` تُنشر عبر GitHub Pages، مع مزامنة Google Apps Script.

## GitHub — جاهز مسبقاً (لا تعِد الإعداد)

- Git وGitHub CLI مثبتان على الجهاز.
- المصادقة محفوظة في Windows Credential Manager بحساب `Mamoun-Almoghrabi` — **لا تطلب توكن ولا تعيد تسجيل الدخول**.
- مسار `gh`: `%LOCALAPPDATA%\Programs\GitHubCLI\gh.exe` (وقد يكون `gh` متاحاً في PATH).
- المستودع: `https://github.com/masjed-alnuman/saheh-albukhari` — الفرع الافتراضي `main`.
- المجلد المحلي مربوط بالمستودع، و`origin/main` متتبَّع.

## عند طلب الرفع

عبارات مثل «ارفع»، «ارفع التغييرات»، «push»، «وصل مباشرة» تعني: نفّذ الرفع فوراً دون إعادة شرح خطوات الإعداد.

1. راجع `git status` و`git diff` باختصار.
2. افحص أي ملف جديد بحثاً عن أسرار قبل الإضافة.
3. `git add` للملفات المناسبة، ثم commit برسالة عربية وصفية، ثم `git push`.
4. تحقق من `git status -sb` وأبلغ المستخدم بالـ commit hash والملفات المرفوعة.
5. إذا فشل الـ push فقط: شغّل `gh auth status` واذكر السبب، دون طلب إعادة الإعداد إلا إذا كانت الجلسة منتهية فعلاً.

## ملفات لا تُرفع أبداً

- `_tools/` — تحتوي أدوات وأسرار Google/OAuth
- `_backup/`
- `apps-script-Bukhari.gs`
- `desktop.ini`
- أي توكن أو مفتاح أو بيانات اعتماد

## قواعد إضافية

- لا تعدّل `logo.jpg` أو تحذفه دون طلب صريح.
- الحفاظ على سجل الـ commits؛ استخدم `git pull --rebase` عند الحاجة بدل الحذف وإعادة الإنشاء.
- رسائل commit بالعربية وواضحة.

## التحقق

- الموقع الحي: https://masjed-alnuman.github.io/saheh-albukhari/
- GitHub Pages يُبنى تلقائياً من فرع `main` بعد كل push.
