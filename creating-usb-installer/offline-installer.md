# التثبيت بدون انترنت

سوف نحتاج الى

سكربت **PackAppWin.py** من مطور **doesprintfwork** تحميل [من هنا](https://github.com/doesprintfwork/MakeInstallmacOS)

برنامج **\(bdu\) Boot Disk Utility** البرنامج الذي سوف نستخدمه لحرق الماك ونسخ الملفات الضروريه لل **usb**  
تحميل يكون من علامه الحفظ اخر الموقع _\*\*_[من هنا](http://cvad-mac.narod.ru/index/bootdiskutility_exe/0-5)

سوف تحتاج برنامج **7zip** بديل مفتوح المصدار افضل من winrar يجب ان يكون مثبت في `C:\Program Files (x86)\7zip` تحميل من [هنا](https://www.7-zip.org/)

برنامج **transmac** لنقل الملفات لل usb تحميل [من هنا](https://www.acutesystems.com/scrtm.htm) \(حمل tmsetup.exe\)

برنامج **Paragon partion manger \(ppm\)** المخصص لتغير حجم اقسام الفلاش [التحميل من هنا](https://www.paragon-software.com/free/pm-express/#)

اول نبدا مع سكربت نذهب الى ملف الذي تم تحميله ثم ننسخ سكربت packappwin.py الى ملف تنزيل الماك والذي سيكون في نفس ملف الموجود فيه اداه gibmacos ثم `macOS Downloads/publicrelase` ثم بعدها اذهب الى ملف الماك الذي نزلته وضع سكربت packappwin.py في نفس الملف

![](../.gitbook/assets/image%20%2844%29.png)

ثم نفتح السكربت اذا قال لك اختار البرنامج الذي سوف تستخدمه لفتح السكربت اختار اظهر زياده من البرامج ثم البحث عن البرنامج في هذا الكمبيوتر

![](../.gitbook/assets/image%20%2852%29.png)

ثم بعدها اذهب الى هاذا المكان `C:\Users\USERNAME\AppData\Local\Programs\Python` استبدل USERNAME باسم حسابك على الويندوز ستجد ملف داخله افتح الملف وستجد البرنامج python.exe ثم اختار open او فتح

![](../.gitbook/assets/image%20%2866%29.png)

بعد ما يفتح ال cmd نختار p

![](../.gitbook/assets/image%20%2871%29.png)

بعد انتهاء السكربت سوف تلاحظ وجود ملف جديد يسمى SharedSupport

## BootDisk Utility

ننتقل لbdu

نذهب الى option/configuration/checknow للبحث عن اخر اصدار عن الكلوفر

ثم بعدها اختار ال usb الخاص فيك ثم اضغط format **\(سوف نفرمت الفلاش تاكد من نسخ جميع الملفات!!\)**

![](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-Le58xqzAwHioaNemfml%2F-LhVhPnzA4e86uCEV81a%2F-LhViriAJ70BK5y8gFUm%2Fezgif-4-b59bb851e67a.gif?alt=media&token=0acc35ae-1161-44d2-921d-42b730c204fa)

1. ثم اذهب الى **tools/Extract HFS from dmg file**

![](../.gitbook/assets/image%20%2836%29.png)

2.اختار ملف BaseSystem.dmg من ملف تنزيلات الماك من برنامج gibmacos ثم اختار فتح او open

![](../.gitbook/assets/image%20%2862%29.png)

ثم اختار سطح المكتب كمكان لحفظ الملف

![](../.gitbook/assets/image%20%2830%29.png)

بعد ذلك البرنامج سيتسخدم 7zip لاستخراج الملف

![](../.gitbook/assets/image%20%2856%29.png)

بعدها سوف تجد ملف

4.hfs على سطح المكتب

الان نرجع الى bdu ثم اضغط على علامه الزائد بجانب ال usb  
ثم اختار part 2

![](../.gitbook/assets/image%20%2868%29.png)

ثم اضغط على زر restore  
بعدها نختار ملف الذي تم استخراجه \(4.hfs\)  
ثم اضغط ok وانتظر حتى يتم نقل الملفات

## Paragon Partion Manger

الان سوف نحتاج الى تغير حجم قسم الماك

نفتح البرنامج ثم بعدها اختار القسم الثاني من الفلاش الذي حجمه 1.87gb

![](../.gitbook/assets/image%20%2847%29.png)

ثم بعدها اجعل حجم ال newvolume اكبر ما يمكن وثم اضغط change now

![](../.gitbook/assets/image%20%2867%29.png)

## transmac

الان ياتي دور برنامج Transmac افتح البرنامج كمشرف \(adminstartor\)

ثم نقوم بسحب ملف SharedSupport من ملف الماك ملف macOS Base System/instal macOS Catalina.app/Contents داخل برنامج Transmac

![](../.gitbook/assets/image%20%285%29.png)

## نقل الكونفق والكيكست

بعد اغلاق البرنامج ستلاحظ وجود USB باسم CLOVER اختارها ثم اذهب الى ملف ال EFI ثم CLOVER استبدل الكونفق الموجود بالخاص بجهازك بعد معالجته من برنامج GenSMBIOS **اذا كان جهازك مكتبي  
اما للابتوبات فضع ملف الكونفق مباشره بعد تغير الاسم الى config.plist**

![](../.gitbook/assets/image%20%2814%29.png)

بعدها افتح ملف kexts ثم others الكيكست تظهر كملفات في الويندوز احذف الكيكست الموجود مسبقا FakeSMC.kext واستبدله ب virtualsmc  
وبعد فك الضغط ضع الملف الذي ينتهي ب .kext في الملف others

**مثال** لkext موجوده في ملف Other

![&#x645;&#x62B;&#x627;&#x644;](../.gitbook/assets/image%20%2843%29.png)

## كاتلينا فما فوق 10.15+

في اصادر 10.15 من الماك سنحتاج الى خطوه اضافيه بحيث ابل وضعت شرط لي استخدام اجهزه EC فا يجب خداع النظام حتى يتم الاقلاع بحيث سيتم تعديل ال DSDT لاضافه اجهزه EC وهميه

سوف نستخدم اداه SSDTtime من IOIIIO نفتح الاداه عبر ملف SSDTTIME.bat

نختار رقم 4 لاستخراج DSDT من المذربورد

![](../.gitbook/assets/image%20%2846%29.png)

الان الاداه سوف تختار ملف ال DSDT التي استخرجته  
اختار رقم 2 FakeEC حتى نضيف التعديلات الازمه

![](../.gitbook/assets/image%20%2823%29.png)

بعدها نذهب الى ملف Results يوجد بنفس الملف الي توجد به الاداه  
سوف تجد ملف SSDT-EC.aml

![](../.gitbook/assets/image%20%2848%29.png)

انسخ الملف ثم اذهب الى ال usb ثم الى EFI/CLOVER/  
ثم انشء ملف ACPI

![](../.gitbook/assets/image%20%2860%29.png)

ثم انشء ملف Patched

![](../.gitbook/assets/image%20%2828%29.png)

داخل ملف Patched ضع ملف SSDT-EC.aml

![](../.gitbook/assets/image%20%2832%29.png)

