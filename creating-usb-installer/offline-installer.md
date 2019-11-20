# التثبيت بدون انترنت

الان نبدء بنسخ الماك مع Make install الجزء الاخر من اداه gibMacOS

اول شيء اوصل ال USB في الجهاز تاكد من معرفه حجم ال USB والشركه المصنعه

الان بعد ما نفتح البرنامج راح يظهر عندنا في الاعلى اجهزه تخزين وجود كلمه \(removable\) يعني يمكن فصله عن الجهاز مثل USB وسيتم ذكر اسم الشركه المصنعه وسعه ال USB يجب التاكد منها.  
تحت ال USB راح نلاقي ال Partions او اقسام ال USB الان **راح نفرمت ال USB** ا**ذا كان عندك اي معلومات مهمه انسخها قبل ما تفرمت**

![](https://github.com/ARhackintosh/ARtutorial/tree/bfeda5d8b3a38dd329307a9b6ac4811c5a3a0995/creating-usb-installer/.gitbook/assets/image%20%2859%29.png)

الان نكتب الرقك المكتوب بجانب ال USB في هاذا الحال رقم 1

![](https://github.com/ARhackintosh/ARtutorial/tree/bfeda5d8b3a38dd329307a9b6ac4811c5a3a0995/creating-usb-installer/.gitbook/assets/image%20%2851%29.png)

بعد ما نضغط زر انتر سوف ينبهنا البرنامج انه ستيم فرمته ال USB بالكامل بعد التاكد من ملفاتك اكتب y واضغط انتر

![](https://github.com/ARhackintosh/ARtutorial/tree/bfeda5d8b3a38dd329307a9b6ac4811c5a3a0995/creating-usb-installer/.gitbook/assets/image%20%287%29.png)

بعد الفرمته الاساسيه البرنامج سوف يطلب موقع النظام في نفس الملف الخاص ب اداه gibmacos افتح ملف MacOS Downloads  
ثم publicrelease ثم افتح ملف النظام الذي نزلته من البرنامج الاول \(gibMacOS\) بهاذا الحاله 10.15 macOS Catalina

![](https://github.com/ARhackintosh/ARtutorial/tree/bfeda5d8b3a38dd329307a9b6ac4811c5a3a0995/creating-usb-installer/.gitbook/assets/image%20%2850%29.png)

افتح الملف وانسخ موقعه وضعه في ال CMD ثم اضغط زر انتر

![](https://github.com/ARhackintosh/ARtutorial/tree/bfeda5d8b3a38dd329307a9b6ac4811c5a3a0995/creating-usb-installer/.gitbook/assets/image%20%2874%29.png)

الان سوف يبدء البرنامج بعمليه النسخ **تعتمد على سرعه ال USB الخاص فيك**

![](https://github.com/ARhackintosh/ARtutorial/tree/bfeda5d8b3a38dd329307a9b6ac4811c5a3a0995/creating-usb-installer/.gitbook/assets/image%20%2835%29.png)

ايضا البرنامج سيقوم بتنزيل الكلوفر و تثبيته على ال USB

![](https://github.com/ARhackintosh/ARtutorial/tree/bfeda5d8b3a38dd329307a9b6ac4811c5a3a0995/creating-usb-installer/.gitbook/assets/image%20%2855%29.png)

بعد الانتهاء اغلق البرنامج

![](https://github.com/ARhackintosh/ARtutorial/tree/bfeda5d8b3a38dd329307a9b6ac4811c5a3a0995/creating-usb-installer/.gitbook/assets/image%20%2842%29.png)

بعد اغلاق البرنامج ستلاحظ وجود USB باسم CLOVER اختارها ثم اذهب الى ملف ال EFI ثم CLOVER استبدل الكونفق الموجود بالخاص بجهازك بعد معالجته من برنامج GenSMBIOS **اذا كان جهازك مكتبي  
اما للابتوبات فضع ملف الكونفق مباشره بعد تغير الاسم الى config.plist**

![](https://github.com/ARhackintosh/ARtutorial/tree/bfeda5d8b3a38dd329307a9b6ac4811c5a3a0995/creating-usb-installer/.gitbook/assets/image%20%2814%29.png)

بعدها افتح ملف kexts ثم others الكيكست تظهر كاملفات في الويندوز احذف الكيكست الموجود مسبقا FakeSMC.kext واستبدله ب virtualsmc  
وبعد فك الضغط ضع الملف الذي ينتهي ب .kext في الملف others

**مثال** لkext موجوده في ملف Other

![&#x645;&#x62B;&#x627;&#x644;](https://github.com/ARhackintosh/ARtutorial/tree/bfeda5d8b3a38dd329307a9b6ac4811c5a3a0995/creating-usb-installer/.gitbook/assets/image%20%2843%29.png)

## كاتلينا فما فوق 10.15+

في اصادر 10.15 من الماك سنحتاج الى خطوه اضافيه بحيث ابل وضعت شرط لي استخدام اجهزه EC فا يجب خداع النظام حتى يتم الاقلاع بحيث سيتم تعديل ال DSDT لاضافه اجهزه EC وهميه

سوف نستخدم اداه SSDTtime من IOIIIO نفتح الاداه عبر ملف SSDTTIME.bat

نختار رقم 4 لاستخراج DSDT من المذربورد

![](https://github.com/ARhackintosh/ARtutorial/tree/bfeda5d8b3a38dd329307a9b6ac4811c5a3a0995/creating-usb-installer/.gitbook/assets/image%20%2846%29.png)

الان الاداه سوف تختار ملف ال DSDT التي استخرجته  
اختار رقم 2 FakeEC حتى نضيف التعديلات الازمه

![](https://github.com/ARhackintosh/ARtutorial/tree/bfeda5d8b3a38dd329307a9b6ac4811c5a3a0995/creating-usb-installer/.gitbook/assets/image%20%2823%29.png)

بعدها نذهب الى ملف Results يوجد بنفس الملف الي توجد به الاداه  
سوف تجد ملف SSDT-EC.aml

![](https://github.com/ARhackintosh/ARtutorial/tree/bfeda5d8b3a38dd329307a9b6ac4811c5a3a0995/creating-usb-installer/.gitbook/assets/image%20%2848%29.png)

انسخ الملف ثم اذهب الى ال usb ثم الى EFI/CLOVER/  
ثم انشء ملف ACPI

![](https://github.com/ARhackintosh/ARtutorial/tree/bfeda5d8b3a38dd329307a9b6ac4811c5a3a0995/creating-usb-installer/.gitbook/assets/image%20%2860%29.png)

ثم انشء ملف Patched

![](https://github.com/ARhackintosh/ARtutorial/tree/bfeda5d8b3a38dd329307a9b6ac4811c5a3a0995/creating-usb-installer/.gitbook/assets/image%20%2828%29.png)

داخل ملف Patched ضع ملف SSDT-EC.aml

![](https://github.com/ARhackintosh/ARtutorial/tree/bfeda5d8b3a38dd329307a9b6ac4811c5a3a0995/creating-usb-installer/.gitbook/assets/image%20%2832%29.png)

