# تثبيت كاتلينا او اقدم

## برامج

- أداة تنزيل الماك ونسخه **[GibmacOS](https://github.com/corpnewt/gibMacOS)** من المطور الرهيب **corpnewt**

- ايضا سوف نحتاج اداه السيريل للماك **[GenSMbios](https://github.com/corpnewt/GenSMBIOS)** من نفس المطور

- اداه **[SSDTTime](https://github.com/IOIIIO/SSDTTime)** من نفس مطور تحتاجه فقط **لكاتلينا وفوق**

- سكربت **[PackAppWin.py](https://github.com/doesprintfwork/MakeInstallmacOS)** من مطور **doesprintfwork** 

- برنامج **[(bdu) Boot Disk Utility](http://cvad-mac.narod.ru/index/bootdiskutility_exe/0-5)** البرنامج الذي سوف نستخدمه لحرق الماك ونسخ الملفات الضروريه لل **usb**  
تحميل يكون من علامه الحفظ اخر الموقع

- سوف تحتاج برنامج **[7zip](https://www.7-zip.org/)** بديل مفتوح المصدار افضل من winrar يجب ان يكون مثبت في `C:\Program Files (x86)\7zip` 
- برنامج **[Paragon Hfs windows(PHW)](https://www.paragon-software.com/home/hfs-windows/)** لنقل الملفات لل usb

- برنامج **[Paragon partion manger (PPM)](https://www.paragon-software.com/free/pm-express/#)** المخصص لتغير حجم اقسام الفلاش

## تنزيل الماك

بعد ما يتم تنزيل اداة gibmacos نفك الضغط و بعدها نفتح الملف ونختار gibMacOS.bat

![](/img/Catalina-or-older/gibMacOS.png#zoom)

في حاله عدم وجود بايثون 3 على حهازك البرنامج سيطلب منك تحميله اكتب y للموافقه

![](/img/no-python.png#zoom)

البرنامج يرتب النسخ **بحسب وقت اصدارها** ابل ايضا تحدث الاصدارات القديمه نحن نريد اصدار 10.15 كاتلينا وهو اخر اصدار من الماك وفي هاذه الحالة تم رفع تحديث امني لي الإصدار الذي قبله فظهر في الاعلى اعلى من الإصدار الاخير من الماك لذا سوف نختار رقم 2

![](/img/Catalina-or-older/system-list.png#zoom)

ثم سيقوم البرنامج ببدء التنزيل

![](/img/Catalina-or-older/g-download.png#zoom)

???+ info "معلومة"
    سرعه التنزيل تعتمد على سرعه الانترنت الخاص بك

سوف تظهر قائمه الملفات التي تم تنزيلها بنجاح واذا لم يوجد اي ملف تحت failed مبروك لقد تم تنزيل النسخة بنجاح تحت File saved to  
يوجد موقع حفظ الملف سوف نحتاجه في الخطوة القادمه

![](/img/Catalina-or-older/g-done.png#zoom)

### تحميل نسخ اقدم

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

بعد ما يفتح ال cmd نختار p

![](../.gitbook/assets/image%20%2892%29.png)

بعد انتهاء السكربت سوف تلاحظ وجود ملف جديد يسمى SharedSupport

## BootDisk Utility

ننتقل لbdu

نذهب إلى option/configuration/checknow للبحث عن اخر اصدار عن الكلوفر

ثم بعدها اختار ال usb الخاص فيك ثم اضغط format **\(سوف نفرمت الفلاش تاكد من نسخ جميع الملفات!!\)**

![](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-Le58xqzAwHioaNemfml%2F-LhVhPnzA4e86uCEV81a%2F-LhViriAJ70BK5y8gFUm%2Fezgif-4-b59bb851e67a.gif?alt=media&token=0acc35ae-1161-44d2-921d-42b730c204fa)

1. ثم اذهب إلى **tools/Extract HFS from dmg file**

![](../.gitbook/assets/image%20%2846%29.png)

2.اختار ملف BaseSystem.dmg من ملف تنزيلات الماك من برنامج gibmacos ثم اختار فتح أو open

![](../.gitbook/assets/image%20%2879%29.png)

ثم اختار سطح المكتب كمكان لحفظ الملف

![](../.gitbook/assets/image%20%2837%29.png)

بعد ذلك البرنامج سيتسخدم 7zip لاستخراج الملف

![](../.gitbook/assets/image%20%2872%29.png)

بعدها سوف تجد ملف

4.hfs على سطح المكتب

الان نرجع إلى bdu ثم اضغط على علامه الزائد بجانب ال usb  
ثم اختار part 2

![](../.gitbook/assets/image%20%2889%29.png)

ثم اضغط على زر restore  
بعدها نختار ملف الذي تم استخراجه \(4.hfs\)  
ثم اضغط ok وانتظر حتى يتم نقل الملفات

## Paragon Partion Manger

الان سوف نحتاج إلى تغير حجم قسم الماك

نفتح البرنامج ثم بعدها اختار القسم الثاني من الفلاش الذي حجمه 1.87gb

![](../.gitbook/assets/image%20%2859%29.png)

ثم بعدها اجعل حجم ال newvolume اكبر ما يمكن وثم اضغط change now

![](../.gitbook/assets/image%20%2888%29.png)

## transmac

الان ياتي دور برنامج Transmac افتح البرنامج كمشرف \(adminstartor\)

ثم نقوم بسحب ملف SharedSupport من ملف الماك ملف macOS Base System/instal macOS Catalina.app/Contents داخل برنامج Transmac

![](../.gitbook/assets/image%20%286%29%20%281%29.png)

## نقل الكونفق والكيكست

بعد اغلاق البرنامج ستلاحظ وجود USB باسم CLOVER اختارها ثم اذهب إلى ملف ال EFI ثم CLOVER استبدل الكونفق الموجود بالخاص بجهازك بعد معالجته من برنامج GenSMBIOS **اذا كان جهازك مكتبي**  
**اما للابتوبات فضع ملف الكونفق مباشره بعد تغير الاسم إلى config.plist**

![](../.gitbook/assets/image%20%2816%29%20%281%29.png)

بعدها افتح ملف kexts ثم others الكيكست تظهر كملفات في الويندوز احذف الكيكست الموجود مسبقا FakeSMC.kext واستبدله ب virtualsmc  
اذا قمت بتنزيل كيكستات سوف تلاحظ انها مضغوطه قم بفك الضغط ثم ضع الملف الذي ينتهي ب .kext في الملف others

**مثال** لkext موجوده في ملف Other

![&#x645;&#x62B;&#x627;&#x644;](../.gitbook/assets/image%20%2855%29.png)

## كاتلينا فما فوق 10.15+ \(SSDTTime\)

في اصادر 10.15 من الماك سنحتاج إلى خطوه اضافيه بحيث ابل وضعت شرط لي استخدام اجهزه EC فا يجب خداع النظام حتى يتمالإقلاع بحيث سيتم تعديل ال DSDT لاضافه اجهزه EC وهميه

سوف نستخدم اداه SSDTtime نفتح الاداه عبر ملف SSDTTIME.bat

نختار رقم 4 لاستخراج DSDT من المذربورد

![](../.gitbook/assets/image%20%2858%29.png)

الان الاداه سوف تختار ملف ال DSDT التي استخرجته  
اختار رقم 2 FakeEC حتى نضيف التعديلات الازمه

![](../.gitbook/assets/image%20%2829%29%20%281%29.png)

بعدها نذهب إلى ملف Results يوجد بنفس الملف الي توجد به الاداه  
سوف تجد ملف SSDT-EC.aml

![](../.gitbook/assets/image%20%2860%29%20%281%29.png)

انسخ الملف ثم اذهب إلى ال usb ثم إلى EFI/CLOVER/  
ثم ملف ACPI

![](../.gitbook/assets/image%20%2877%29.png)

ثم ملف Patched

![](../.gitbook/assets/image%20%2835%29.png)

داخل ملف Patched ضع ملف SSDT-EC.aml

![](../.gitbook/assets/image%20%2839%29%20%281%29.png)




