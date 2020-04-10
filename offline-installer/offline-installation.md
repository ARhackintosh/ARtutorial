# التثبيت بدون انترنت

## برامج اضافية

سكربت **PackAppWin.py** من مطور **doesprintfwork** تحميل [من هنا](https://github.com/doesprintfwork/MakeInstallmacOS)

برنامج **\(bdu\) Boot Disk Utility** البرنامج الذي سوف نستخدمه لحرق الماك ونسخ الملفات الضروريه لل **usb**  
تحميل يكون من علامه الحفظ اخر الموقع _\*\*_[من هنا](http://cvad-mac.narod.ru/index/bootdiskutility_exe/0-5)

سوف تحتاج برنامج **7zip** بديل مفتوح المصدار افضل من winrar يجب ان يكون مثبت في `C:\Program Files (x86)\7zip` تحميل من [هنا](https://www.7-zip.org/)

برنامج **transmac** لنقل الملفات لل usb تحميل [من هنا](https://www.acutesystems.com/scrtm.htm) \(حمل tmsetup.exe\)

برنامج **Paragon partion manger \(ppm\)** المخصص لتغير حجم اقسام الفلاش [التحميل من هنا](https://www.paragon-software.com/free/pm-express/#)

## PackAppwin.py

اول نبدا مع سكربت نذهب إلى ملف الذي تم تحميله ثم ننسخ سكربت packappwin.py إلى ملف تنزيل الماك والذي سيكون في نفس ملف الموجود فيه اداه gibmacos ثم `macOS Downloads/publicrelase` ثم بعدها اذهب إلى ملف الماك الذي نزلته وضع سكربت packappwin.py في نفس الملف

![](../.gitbook/assets/image%20%28101%29.png)

ثم نفتح السكربت اذا قال لك اختار البرنامج الذي سوف تستخدمه لفتح السكربت اختار اظهر زياده من البرامج ثم البحث عن البرنامج في هذا الكمبيوتر

![](../.gitbook/assets/image%20%28117%29.png)

ثم بعدها اذهب إلى هاذا المكان `C:\Users\USERNAME\AppData\Local\Programs\Python` استبدل USERNAME باسم حسابك على الويندوز ستجد ملف داخله افتح الملف وستجد البرنامج python.exe ثم اختار open أو فتح

![](../.gitbook/assets/image-86.png)

بعد ما يفتح ال cmd نختار p

![](../.gitbook/assets/image-92.png)

بعد انتهاء السكربت سوف تلاحظ وجود ملف جديد يسمى SharedSupport

## BootDisk Utility

ننتقل لbdu

نذهب إلى option/configuration/checknow للبحث عن اخر اصدار عن الكلوفر

ثم بعدها اختار ال usb الخاص فيك ثم اضغط format **\(سوف نفرمت الفلاش تاكد من نسخ جميع الملفات!!\)**

![](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-Le58xqzAwHioaNemfml%2F-LhVhPnzA4e86uCEV81a%2F-LhViriAJ70BK5y8gFUm%2Fezgif-4-b59bb851e67a.gif?alt=media&token=0acc35ae-1161-44d2-921d-42b730c204fa)

1. ثم اذهب إلى **tools/Extract HFS from dmg file**

![](../.gitbook/assets/image%20%2886%29.png)

2.اختار ملف BaseSystem.dmg من ملف تنزيلات الماك من برنامج gibmacos ثم اختار فتح أو open

![](../.gitbook/assets/image%20%28143%29.png)

ثم اختار سطح المكتب كمكان لحفظ الملف

![](../.gitbook/assets/image%20%2872%29.png)

بعد ذلك البرنامج سيتسخدم 7zip لاستخراج الملف

![](../.gitbook/assets/image%20%28130%29.png)

بعدها سوف تجد ملف

4.hfs على سطح المكتب

الان نرجع إلى bdu ثم اضغط على علامه الزائد بجانب ال usb  
ثم اختار part 2

![](../.gitbook/assets/image-89.png)

ثم اضغط على زر restore  
بعدها نختار ملف الذي تم استخراجه \(4.hfs\)  
ثم اضغط ok وانتظر حتى يتم نقل الملفات

## Paragon Partion Manger

الان سوف نحتاج إلى تغير حجم قسم الماك

نفتح البرنامج ثم بعدها اختار القسم الثاني من الفلاش الذي حجمه 1.87gb

![](../.gitbook/assets/image%20%28105%29.png)

ثم بعدها اجعل حجم ال newvolume اكبر ما يمكن وثم اضغط change now

![](../.gitbook/assets/image-88.png)

## transmac

الان ياتي دور برنامج Transmac افتح البرنامج كمشرف \(adminstartor\)

ثم نقوم بسحب ملف SharedSupport من ملف الماك ملف macOS Base System/instal macOS Catalina.app/Contents داخل برنامج Transmac

![](../.gitbook/assets/image%20%2812%29.png)

## نقل الكونفق والكيكست

بعد اغلاق البرنامج ستلاحظ وجود USB باسم CLOVER اختارها ثم اذهب إلى ملف ال EFI ثم CLOVER استبدل الكونفق الموجود بالخاص بجهازك بعد معالجته من برنامج GenSMBIOS **اذا كان جهازك مكتبي**  
**اما للابتوبات فضع ملف الكونفق مباشره بعد تغير الاسم إلى config.plist**

![](../.gitbook/assets/image%20%2833%29.png)

بعدها افتح ملف kexts ثم others الكيكست تظهر كملفات في الويندوز احذف الكيكست الموجود مسبقا FakeSMC.kext واستبدله ب virtualsmc  
اذا قمت بتنزيل كيكستات سوف تلاحظ انها مضغوطه قم بفك الضغط ثم ضع الملف الذي ينتهي ب .kext في الملف others

**مثال** لkext موجوده في ملف Other

![&#x645;&#x62B;&#x627;&#x644;](../.gitbook/assets/image%20%28100%29.png)

## كاتلينا فما فوق 10.15+ \(SSDTTime\)

في اصادر 10.15 من الماك سنحتاج إلى خطوه اضافيه بحيث ابل وضعت شرط لي استخدام اجهزه EC فا يجب خداع النظام حتى يتمالإقلاع بحيث سيتم تعديل ال DSDT لاضافه اجهزه EC وهميه

سوف نستخدم اداه SSDTtime نفتح الاداه عبر ملف SSDTTIME.bat

نختار رقم 4 لاستخراج DSDT من المذربورد

![](../.gitbook/assets/image%20%28103%29.png)

الان الاداه سوف تختار ملف ال DSDT التي استخرجته  
اختار رقم 2 FakeEC حتى نضيف التعديلات الازمه

![](../.gitbook/assets/image%20%2856%29.png)

بعدها نذهب إلى ملف Results يوجد بنفس الملف الي توجد به الاداه  
سوف تجد ملف SSDT-EC.aml

![](../.gitbook/assets/image%20%28106%29.png)

انسخ الملف ثم اذهب إلى ال usb ثم إلى EFI/CLOVER/  
ثم ملف ACPI

![](../.gitbook/assets/image%20%28141%29.png)

ثم ملف Patched

![](../.gitbook/assets/image%20%2868%29.png)

داخل ملف Patched ضع ملف SSDT-EC.aml

![](../.gitbook/assets/image%20%2877%29.png)

