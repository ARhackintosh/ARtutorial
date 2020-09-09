<div dir="rtl">
  
## (v2)الاصدار الثاني من شرح تثبيت الهاكنتوش من [هاكنتوش بالعربي](هاكنتوش.com)

![dev-Build](https://github.com/ARhackintosh/ARtutorial/workflows/dev-Build/badge.svg)

**مرخص تحت**:

<img src="https://topologic.app/wp-content/uploads/2019/01/AGPLv3-Logo.png"  width="250">


اهلا بكم في قسم الاصدار الثاني (v2) من شرح تثبيت الهاكنتوش
هذا الجزء (branch) هو للتطوير 
بحيث نقوم بعمل جميع التغييرات واختبارها ثم دفعها الى العامه production
سيتم انشاء branch production عندما تنتهي مرحلة التطوير

## الميزات المخطط اضافتها
- دعم ماك Big Sur
- اضافه دعم [opencore](https://github.com/acidanthera/OpenCorePkg)
- استخدام الكونفق الجديد لمعالجات amd
- محاوله تقليل عدد البرامج المستخدمة
- تركيز اكبر على الابتوبات(نحتاج متطوعين لهم خبره)
- قسم للاسئلة الشائعة
- دعم لينكس؟
* [x] نقل الشرح الى موقعنا

## حاله الشرح:
بعد اعاده البحث في شروط ابل, اتضح ان حتى الماك الوهمي يكسر القوانين

ولايوجد فعلا اي طريقه لاتكسر الشروط لتثبيت ماك بيج سر لانه لايمكن تثبيت النظام مباشره من ويندوز

بسبب عدم وجود حلول واقعيه تم اتاخذ قرار اخذ صوره (ملف DMG) من usb تم تجيهزه داخل نظام الماك يحتوي على نظام بيج سر بدون اي تعديلات مع قسم EFI داخلي 

بحيث نختصر عمليه الحرق و نتجه الى تجيهز التعريفات و الكونفق

للانظمه الاقدم من macOS 11 سيتم اعتماد نفس الطريقه السابقه مع احتمال تخطي برنامج BDU 

نحن منفحتين لتغيير القرار اذا وجد طريقه مباشره لتثبيت ماك Big Sur  من الويندوز او لينكس


## بنيه الشرح
الشرح مبني على برنامج [mkdocs](https://github.com/mkdocs/mkdocs/)
مع ثيم [material](https://github.com/squidfunk/mkdocs-material)

الشرح مكتوب بصيغه markdown
اذا كنت لا تعرف طريقه الكتابه بصيغه markdown اتبع هذا [الشرح](https://academy.hsoub.com/apps/productivity/%D9%83%D9%8A%D9%81-%D8%AA%D9%83%D8%AA%D8%A8-%D8%A8%D8%B5%D9%8A%D8%BA%D8%A9-%D9%85%D8%A7%D8%B1%D9%83%D8%AF%D8%A7%D9%88%D9%86-%D8%A8%D8%A8%D8%B3%D8%A7%D8%B7%D8%A9-r290/) 

ايضا ننصح بستخدام [المحرر رمز](https://ramz.netlify.app/) لتحرير الشرح لدعمه اللغه العربيه وصيغه markdown

**تاكد من حذف ``<div dir="rtl">`` من بعض الملفات**

بالاضافه الى بعض الخصائص الاضافيه مثل

1. [Admonition](https://squidfunk.github.io/mkdocs-material/extensions/admonition/)
2. [critc](https://squidfunk.github.io/mkdocs-material/extensions/pymdown/#critic)
3. [Details](https://squidfunk.github.io/mkdocs-material/extensions/pymdown/#details)
4. [Tabbed](https://squidfunk.github.io/mkdocs-material/extensions/pymdown/#tabbed)
5. [Tasklist](https://squidfunk.github.io/mkdocs-material/extensions/pymdown/#tasklist)
6. [MagicLink](https://squidfunk.github.io/mkdocs-material/extensions/pymdown/#magiclink)
7. [css مخصص](./docs/extra.css)
8. [Caret, Mark & Tilde](https://squidfunk.github.io/mkdocs-material/reference/formatting/#caret-mark-tilde)

جميع التغييرات يتم بنائها من dev-build ثم دفعها الى github pages

</div>

**رابط الشرح**:

https://tutorial.هاكنتوش.com

