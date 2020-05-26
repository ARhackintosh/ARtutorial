# usb نقل الماك الى

## Packappwin.py

اول نبدا مع سكربت نذهب الى ملف الذي تم تحميله ثم ننسخ سكربت packappwin.py الى ملف تنزيل الماك والذي سيكون في نفس ملف الموجود فيه اداه gibmacos ثم `macOS Downloads/publicrelase` ثم بعدها اذهب الى ملف الماك الذي نزلته وضع سكربت packappwin.py في نفس الملف

![](.gitbook/assets/image%20%28114%29.png)

ثم نفتح السكربت اذا ظهر لك اختيار البرنامج الذي سوف تستخدمه لفتح السكربت اختار اظهر زياده من البرامج ثم البحث عن البرنامج في هذا الكمبيوتر

![](.gitbook/assets/image%20%28122%29.png)

ثم بعدها اذهب الى هاذا المكان `C:\Users\USERNAME\AppData\Local\Programs\Python` استبدل USERNAME باسم حسابك على الويندوز ستجد ملف داخله افتح الملف وستجد البرنامج python.exe ثم اختار open او فتح

![](.gitbook/assets/image%20%28118%29.png)

بعد ما يفتح ال cmd نختار p

![](.gitbook/assets/image%20%28104%29.png)

بعد انتهاء السكربت سوف تلاحظ وجود ملف جديد يسمى SharedSupport

## BootDisk Utility

ننتقل لbdu

نذهب الى option/configuration/checknow للبحث عن اخر اصدار عن الكلوفر

ثم بعدها اختار ال usb الخاص فيك ثم اضغط format **\(سوف نفرمت الفلاش تاكد من نسخ جميع الملفات!!\)**

![](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-Le58xqzAwHioaNemfml%2F-LhVhPnzA4e86uCEV81a%2F-LhViriAJ70BK5y8gFUm%2Fezgif-4-b59bb851e67a.gif?alt=media&token=0acc35ae-1161-44d2-921d-42b730c204fa)

1. ثم اذهب الى **tools/Extract HFS from dmg file**

![](.gitbook/assets/image%20%28110%29.png)

2.اختار ملف BaseSystem.dmg من ملف تنزيلات الماك من برنامج gibmacos ثم اختار فتح او open

![](.gitbook/assets/image%20%28145%29.png)

ثم اختار سطح المكتب كمكان لحفظ الملف

![](.gitbook/assets/image%20%286%29.png)

بعد ذلك البرنامج سيتسخدم 7zip لاستخراج الملف

![](.gitbook/assets/image%20%28132%29.png)

بعدها سوف تجد ملف

4.hfs على سطح المكتب

الان نرجع الى bdu ثم اضغط على علامه الزائد بجانب ال usb  
ثم اختار part 2

![](.gitbook/assets/image%20%28111%29.png)

ثم اضغط على زر restore  
بعدها نختار ملف الذي تم استخراجه \(4.hfs\)  
ثم اضغط ok وانتظر حتى يتم نقل الملفات

## Paragon Partion Manger

الان سوف نحتاج الى تغير حجم قسم الماك

نفتح البرنامج ثم بعدها اختار القسم الثاني من الفلاش الذي حجمه 1.87gb

![](.gitbook/assets/image%20%28135%29.png)



ثم بعدها اجعل حجم ال newvolume اكبر ما يمكن وثم اضغط change now

![](.gitbook/assets/image%20%28127%29.png)

## transmac

الان ياتي دور برنامج Transmac افتح البرنامج كمشرف \(adminstartor\)

ثم نقوم بسحب ملف SharedSupport من ملف الماك ملف macOS Base System/instal macOS Catalina.app/Contents داخل برنامج Transmac

![](.gitbook/assets/image%20%28121%29.png)

## نقل الكونفق والكيكست

بعد اغلاق البرنامج ستلاحظ وجود USB باسم CLOVER اختارها ثم اذهب الى ملف ال EFI ثم CLOVER استبدل الكونفق الموجود بالخاص بجهازك بعد معالجته من برنامج GenSMBIOS 

![](.gitbook/assets/image%20%2883%29%20%281%29.png)

بعدها افتح ملف kexts ثم others الكيكست تظهر كملفات في الويندوز احذف الكيكست الموجود مسبقا FakeSMC.kext واستبدله ب virtualsmc  
وبعد فك الضغط ضع الملف الذي ينتهي ب .kext في الملف others

**مثال** لkext موجوده في ملف Other

![&#x645;&#x62B;&#x627;&#x644;](.gitbook/assets/image%20%2819%29.png)

## كاتلينا فما فوق 10.15+ \(SSDTTime\)

في اصادر 10.15 من الماك سنحتاج الى خطوه اضافيه بحيث ابل وضعت شرط لي استخدام اجهزه EC فا يجب خداع النظام حتى يتم الاقلاع بحيث سيتم تعديل ال DSDT لاضافه اجهزه EC وهميه

سوف نستخدم اداه SSDTtime نفتح الاداه عبر ملف SSDTTIME.bat

نختار رقم 4 لاستخراج DSDT من المذربورد

![](.gitbook/assets/image%20%28130%29.png)

الان الاداه سوف تختار ملف ال DSDT التي استخرجته  
اختار رقم 2 FakeEC حتى نضيف التعديلات الازمه

![](.gitbook/assets/image%20%28120%29.png)

بعدها نذهب الى ملف Results يوجد بنفس الملف الي توجد به الاداه  
سوف تجد ملف SSDT-EC.aml

![](.gitbook/assets/image%20%2895%29.png)

انسخ الملف ثم اذهب الى ال usb ثم الى EFI/CLOVER/  
ثم ملف ACPI

![](.gitbook/assets/image%20%2896%29.png)

ثم ملف Patched

![](.gitbook/assets/image%20%28116%29.png)

داخل ملف Patched ضع ملف SSDT-EC.aml

![](.gitbook/assets/image%20%28136%29.png)

