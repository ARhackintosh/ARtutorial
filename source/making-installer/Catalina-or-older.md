
???+ info "محلوظه"
	في حاله كان **لديك نظام ماك من قبل** يمكنك نسخ النسخه من الماك, بعد تنزيلها من gibmacos, افتح **BuildmacOSInstallApp.command** ثم قم بسحب ملف الذي يحتوي على نظام الماك الى التيرمنال, في حاله ظهور النسخه في نفس الملف قم بنقلها الى ملف التطبيقات.[ثم قم بنسخها من التيرمنال](https://forum.هاكنتوش.com/threads/kif-tnsx-nzam-almak-al-usb-mn-altirmnal.107/)

## برامج

- أداة تنزيل الماك  **[GibmacOS](https://github.com/corpnewt/gibMacOS)** من المطور الرهيب **corpnewt**

- سكربت **[PackAppWin.py](https://github.com/doesprintfwork/MakeInstallmacOS)** من مطور **doesprintfwork** 

- برنامج **[(bdu) Boot Disk Utility](http://cvad-mac.narod.ru/index/bootdiskutility_exe/0-5)** البرنامج الذي سوف نستخدمه لحرق الماك ونسخ الملفات الضروريه لل **usb**
لتنزيل البرنامج اضغط على علامه الحفظ اخر الموقع

- سوف تحتاج برنامج **[7zip](https://www.7-zip.org/)** بديل مفتوح المصدار افضل من winrar يجب ان يكون مثبت في `C:\Program Files (x86)\7zip` 

- برنامج **[Paragon Hfs windows(PHW)](https://www.paragon-software.com/home/hfs-windows/)** لنقل الملفات لل usb

- برنامج **[Paragon partion manger (PPM)](https://www.paragon-software.com/free/pm-express/#)** المخصص لتغير حجم اقسام الفلاش

## تنزيل الماك

بعد ما يتم تنزيل اداة gibmacos نفك الضغط و بعدها نفتح الملف ونختار gibMacOS.bat

![](/img/Catalina-or-older/gibMacOS.png#zoom)

???+ info "في حاله عدم وجود بايثون"
	في حاله عدم وجود بايثون 3 على حهازك البرنامج سيطلب منك تنزيله اكتب y للموافقه

	![](/img/no-python.png#zoom)

البرنامج يرتب النسخ **بحسب وقت اصدارها** ابل ايضا تحدث الاصدارات القديمه نحن نريد اصدار 10.15 كاتلينا, وفي هاذه الحالة تم رفع تحديث امني للاصدار السابق فظهر اعلى من الإصدار المطلوب من الماك لذا سنختار رقم 2

![](/img/Catalina-or-older/system-list.png#zoom)

ثم سيقوم البرنامج ببدء التنزيل

![](/img/Catalina-or-older/g-download.png#zoom)

???+ info "معلومة"
    سرعه التنزيل تعتمد على سرعه الانترنت الخاص بك

سوف تظهر قائمه الملفات التي تم تنزيلها بنجاح واذا لم يوجد اي ملف تحت failed مبروك لقد تم تنزيل النسخة بنجاح تحت File saved to
يوجد موقع حفظ الملف سوف نحتاجه في الخطوة القادمه

![](/img/Catalina-or-older/g-done.png#zoom)

### تنزيل نسخ اقدم

اذا كنت تحتاج نسخ اقدم مثل لو كان لديك كرت انفيديا اضغط M في الصفحة الرئيسيه ثم اكتب رقم النسخة بهاذه الحالة سوف تكون 10.13

![](/img/Catalina-or-older/old-ver.png#zoom)

سوف تظهر اختيارات جديده نختار اعلى اختيار من الإصدار المطلوب بهاذه الحالة MacOS High Sierra

![](/img/Catalina-or-older/g-old-list.png#zoom)

ثم البرنامج سيقوم بتنزيل النسخة مقسمه على 11 ملف

![](/img/Catalina-or-older/g-download.png#zoom)

## PackAppwin.py

هذا السكربت يقوم بتجميع الملفات حتى يمكننا التثبيت بدون الحاجه الى انترنت.
اولا اذهب الى مكان تنزيل الملف ثم قم بنسخه, وبعد ذلك توجه الى مكان برنامج Gibmacos 
اذهب الى مكان تنزيل الماك `/macOS Downloads/publicrelease/xxx-xxxxx` ثم قم بلصق السكربت

![](/img/Catalina-or-older/packappwin-paste.png)

ثم قم بفتح السكربت

??? info "في حاله ظهور كيفيه فتح الملف."
    
     اختار بحث عن برنامج اخر في هذا الكمبيوتر
    
    ![](/img/Catalina-or-older/select-app.png)

    ثم بعدها اذهب إلى `C:\Users\%USERNAME%\AppData\Local\Programs\Python` ستجد ملف داخله افتحه, ثم ستجد البرنامج python.exe ثم اختار open أو فتح 

    ![](/img/Catalina-or-older/select-python.png)

بعد فتح السكربت قم بختيار P

![](/img/Catalina-or-older/menu.png)

بعد انتهاء السكربت سوف تلاحظ وجود ملف جديد يسمى SharedSupport فهو يحتوي على الملفات الناقصه للتثبيت بدون الحاجه الى انترنت, سنستخدمه لاحقا.

## BootDisk Utility

اولا نذهب الى اعدادات البرنامج الموجوده في **Options ثم Configuration**

ثم نتاكد ان اعدادات البرنامج كالاتي

![](/img/Catalina-or-older/BDU-Config.png#zoom)

???+ info "معلومة"
	هذه الاعدادات تقوم بتعطيل تنزيل الكلوفر التلقائي لان البرنامج للاسف مازال لا يدعم اوبن كور.

**تاكد من اختيار ال usb ثم الضغط على زر format حتى نقوم بفرمته ال usb بشكل صحيح**

![](/img/Catalina-or-older/bdu-format.png)

1. ثم اذهب إلى **tools/Extract HFS from dmg file**.

![](/img/Catalina-or-older/BDU-Extract.png#zoom)

2.اختار ملف ==BaseSystem.dmg== من ملف تنزيلات الماك من برنامج gibmacos ثم اختار **فتح أو open**.

![](/img/Catalina-or-older/BDU-Basesystemdmg.png#zoom)

ثم بعد ذلك قم بختيار سطح المكتب كمكان نحفظ فيه الملف او اي مكان اخر الموضوع راجع لك.

![](/img/Catalina-or-older/BDU-Desktop.png#zoom)

بعدها سوف تجد ملف 4.hfs على سطح المكتب

الان نعود إلى bdu ثم نضغط على علامه الزائد بجانب ال usb, ثم اختار part 2

![](/img/Catalina-or-older/BDU-USB.png#zoom)

ثم اضغط على زر restore
 
بعدها نختار ملف الذي تم استخراجه (4.hfs), ثم اضغط ok ثم انتظر حتى يتم نقل الملفات

## Paragon Partion Manger

بعد نسخ الملف ستلاحظ ان حجم القسم هو حوالي 1.87GB وهو غير كافي ابدا لبقيه ملفات النظام الاخرى, لذلك سنحتاج الى برنامج PPM حتى نقوم بتغير حجم القسم (**Partition**)

اولا افتح البرنامج ثم ابحث عن القسم بالحجم الاكبر (**حجمه حوالي 1.87GB**) ثم قم بالضغط على **Move or Resize**
![](/img/Catalina-or-older/PPM-select.png#zoom)

بعد ذلك ستفتح نافذه جديدة, قم بتغيير حجم New volume size الى اكبر شيء ممكن, **تاكد ان اسم القسم ==macOS Base System== او ==OS X Base System==**), بعد ذلك قم بالضغط على Change now
![](/img/Catalina-or-older/PPM-Resize.png#zoom)

## Paragon HFS+ For Windows

???+ Warning "تنبيه"
	اذا لم تقم بعمل اعاده تشغيل لجهازك بعد تثبيت Paragon HFS+ الرجاء عمل اعادة تشغيل للتاكد من عمل البرنامج بشكل صحيح.

من المفترض ان تلاقي usb في مستكشف الملفات تحت اسم ==macOS Base System== او ==OS X Base System==

??? info "في حالة عدم ظهور ال usb"
	قم بفتح برنامج PHW وبعد ذلك اختار ال usb ثم mount 
	![](/img/Catalina-or-older/PHW-Mount.png#zoom)

افتح ال usb (او القسم) ثم توجه الى  `Install macOS xxx.app/Contents`  وقم بلصق ملف Sharedsupport الذي انشئناه مع سكربت packappwin.py, بحيث تصبح الملفات بهذا الشكل 

![](/img/Catalina-or-older/USB-paste.png#zoom)



