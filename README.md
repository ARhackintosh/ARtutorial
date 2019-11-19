# البداية

## تنوييه !

{% hint style="danger" %}
نحن غير مسئولون عما مايحدث في جهازك اثناء وبعد تثبيت الهاكنتوش.
{% endhint %}

## المعرفه التقنية

قبل ما ابدء احتاج انبه ان الهاكنتوش **ليس نظام عادي** ويحتاج تدخل تقني اكثر بكثير من الويندوز بحيث مع كل تحديث يحتاج تجهيزات يدويه وايضا قد تحصل مشاكل في الاقلاع قد تمنعك من الوصول للنظام. الهاكنتوش يحتاج الكثير من البحث تعريفات على حسب القطع وحل مشاكل وغيره اذا كنت تحتاج جهازك يعمل بشكل دائم **بدون اي مشاكل** الهاكنتوش ليس لك. اذا كانت معرفتك التقنيه **ضعيفه** مثل عدم معرفه ماهو جيل المعالج و ماهو bios الهاكنتوش ليس لك. الهاكنتوش نظام اعقد ويتطلب معرفه تقنيه متقدمه مع صبر على مشاكله المعتاده

في هذا الشرح سوف نثبت الماك الخام **\(vanilla\)** على معالجات **intel** لاكن ما يعني خام ؟ خام يعني ان النظام أصلي لم يتم التعديل عليه ابدا ويكون التعديل في قسم ال **EFI** المخصص للاقلاع القسم الاساسي لنظام الماك في الهاكنتوش يطابق الموجود في اجهزه الماك الاصليه

## اختصارات سيتم استخدامها اثناء الشرح :

راح تستخدم هاذه الاختصارات في الشرح

**كلوفر \(clover\) :** هو عبار عن **bootloader** البوت لودر هو البرنامج المسوؤل عن اقلاع النظام , اجهزه الماك يكون فيها برنامج مخصص للاقلاع لنظام الماك , بالنسبه للكمبيوتر العادي سوف نحتاج كلوفر للاقلاع. ايضا هو المسئول عن ادخال ال Kexts و الباتشات والعديد من المهام الاخرى.

**كيرنل بانك \(Kernel panic\) :** اختصارها **KP** وهي **فشل في اقلاع النظام** وتعليق الجهاز في مرحله الاقلاع عندما تضع v- ويتوقف تحرك المكتوب بدون الاقلاع هذا هو ال KP

**الكيكست \(kext\) :** معنى كلمه "kext" هي اختصار ل **Kernel extenions** او اضافات الكيرنل باختصار الكيكست هي التعريفات لنظام الماك

**الكونفق \(config.plist\)** **:** هو الملف الذي يقول لكوفر ماذا يفعل مبني على ترتيب XML الشبيه ب HTML وهو من اهم الاشياء في الهاكنتوش

**اووب \(OOB\) :** هو اختصار لكلمه **Out of the box** او انه يعمل بشكل مباشر بدون الحاجه الى اي نوع من التعديل

**دي اس دي تي \(DSDT\) :** كل كمبيوتر له ترتيب فريد من القطع والمواصفات مثل نوع المعالج والمذربورد ونوع الاعدادات الخ هذا ما يمثله ال **DSDT**

**اس اس دي تي \(SSDT\) :** وهو ملف احتياطي بديل ل DSDT

## الشروط :

راح تكون هناك شروط حتى يكون جهازك مدعوم من هاكنتوش بالعربي :

### المعالج :

لازم يكون من **الجيل الثالث** فما **فوق**. كيف تعرف معالجك اي جيل ؟ بسيطه من الويندوز ابحث عن **About Your PC** او **حول هذا الكمبيوتر**

عند قسم المعالج يجب ان يكون اول رقم بعد اسم المعالج اكثر من 2 يعني **core i7-4790k** او **core i3 6100 او Core i5 3600** او حتى **core i9 9900k** اذا كان اول رقم اقل من **3** مثل **core i7 2700k** فنحن لانقدم المساعده له. لا يعني انه مستحيل تثبيت الهاكنتوش عليه لاكن يستحسن ان تغير الجهاز لانه قديم.

### الرام :

بالنسبه للرام فجهازك يجب ان يحتوي على الاقل **4 جيجا** رام لاكن الحد الفعلي هو **8 جيجا** رام وهو التي تنصح ابل فيه لاخر اصدر من الماك

### كرت الشاشة :

بالنسبه لكروت الشاشه **المنفصله في الابتوبات غير مدعومه** وسوف يتم استخدام **الكرت الداخلي \(intel\)** للماك  
كانت هناك محاولات ناجحه لتفعيل الكروت المنفصله في الابتوات **لاكنها ليست مؤكده لكل الاجهزه**

بالنسبه للكمبيوتر المكتبي فكروت **AMD** هي افضل خيار لانها مدعومه **بشكل مباشر من النظام** ابتعد عن كروت **XFX** لانها تواجه احيانا بعض المشاكل ابل تدعم بشكل رسمي هاذي الكروت

* **Radeon RX 470**
* **Radeon RX 480**
* **Radeon RX 570**
* **Radeon RX 580**
* **Radeon RX 5700 XT \(Catalina 10.15.1+\)**
* **Radeon Pro WX 7100**
* **Radeon RX Vega 56**
* **Radeon RX Vega 64**
* **Radeon RX Vega Frontier Edition**
* **Radeon Pro WX 9100**

ال **RX 590** و **560** ايضا مدعومين لانهم من نفس المعماريه طبعا هاذي القائمه لا تشمل جميع الكروت لاكنها هي الكروت التي المؤكد عملها من داخل النظام مثلا كرت Radeon Vii يعمل مباشره من النظام بينما كرت **R9 380** احتاج كيكست [**WhateverGreen**](https://github.com/acidanthera/WhateverGreen) ليعمل

بالنسبه لكروت انفيديا فهاذه لائحه تعرض بعض الكروت المدعومه في اخر اصدار من الماك

### لائحة بعض كروت Nvidia المدعومة على macOS Catalina 10.15

| **GT** | **GTX** | **Quadro** |
| :---: | :---: | :---: |
| GT 740 | GTX Titan \| GK 110 | Quadro 410 |
| GT 730 | GTX Titan Black \| GK 110 | Quadro K420 |
| GT 720 | GTX Titan Z | Quadro K600 |
| GT 710 | GTX 780 Ti | Quadro K2000/D |
| GT 640 \(Kepler edition, GK 107/208 core\) | GTX 770 | Quadro K4000/D |
| GT 630 \(Kepler edition, GK 208 core\) | GTX 760 Ti | Quadro K4200 |
| - | GTX 690 | Quadro K5000 |
| - | GTX 680 | Quadro K5200 |
| - | GTX 670 | Quadro K6000 |
| - | GTX 660 Ti | Quadro NVS510 |
| - | GTX 650 Ti | - |
| - | GTX 645 \(Fermi\) | - |

بالنسبه لكروت **Nvidia الاخرى** بشكل عام انا انصح ان تبقى على الويندوز لان البرامج على ويندوز مصممه لاستخدام كروت انفيديا بشكل افضل لاكن اذا كنت تريد تثبيت الماك مع كرت انفيديا ستكون محدود الى اصدار **High Sierra 10.13** بحيث هذا **اخر اصدار سمحت أبل لانفيديا باصدار التعريفات له**

## الاحتيجات :

هذا الشرح يركز على الكمبيوتر **المكتبي** بالنسبه **الابتوبات** ستكون الخطوات أعقد و مخصصة لكل جهاز بشكل اكبر لاكن ستكون بالاساس شبيهه بالمكتبي.

أداة تنزيل الماك ونسخه **\(GibmacOS\)** من المطور الرهيب **corpnewt** تحميل من [هنا](https://github.com/corpnewt/gibMacOS)

سكربت **PackAppWin.py** من مطور **doesprintfwork** تحميل [من هنا](https://github.com/doesprintfwork/MakeInstallmacOS)

ايضا سوف نحتاج اداه السيريل للماك **\(GenSMbios\) للمكتبي فقط** من نفس المطور تحملها من [هنا ](https://github.com/corpnewt/GenSMBIOS)

اداه **SSDTime** المعدله من مطور **IOIIIO** تحتاجه فقط **لكاتلينا وفوق** تحميل من [هنا](https://github.com/IOIIIO/SSDTTime)

كيكست [Virtualsmc.kext](https://github.com/acidanthera/VirtualSMC/releases) هذا يستبدل **Fakesmc** بحيث سيكون محاكي ال [smc](https://en.wikipedia.org/wiki/System_Management_Controller) القطعه المسئوله عن التحكم في النظام في اجهزه ابل  
 بدونها لا يمكن الاقلاع

{% hint style="info" %}
التحميل من الروابط في الاعلى يكون من زر **Clone or download** ثم اختار **Download zip** ثم انشئ ملف تفك في ضغط الملفات
{% endhint %}

برنامج **\(bdu\) Boot Disk Utility** البرنامج الذي سوف نستخدمه لحرق الماك ونسخ الملفات الضروريه لل **usb**  
 تحميل يكون من علامه الحفظ اخر الموقع ****[من هنا](http://cvad-mac.narod.ru/index/bootdiskutility_exe/0-5)

سوف تحتاج برنامج **7zip** بديل مفتوح المصدار افضل من winrar  يجب ان يكون مثبت في   `C:\Program Files (x86)\7zip` تحميل من [هنا](https://www.7-zip.org/)

برنامج **transmac** لنقل الملفات لل usb تحميل [من هنا](https://www.acutesystems.com/scrtm.htm) \(حمل tmsetup.exe\)

برنامج **Paragon partion manger \(ppm\)** المخصص لتغير حجم اقسام الفلاش [التحميل من هنا](https://www.paragon-software.com/free/pm-express/#)

التعريفات **\(Kext\)** سوف تكون على حسب جهازك. **سنشرح هذا في القسم القادم**

يو اس بي **\(USB\)** مساحته **8GB** و أكثر

**شويه صبر وعزم واحتراف في البحث على الانترنت**

### الدعم :

سنوفر الدعم **للطريقه الرسميه فقط لن نقدم الدعم لنسخ معدله** مثل ~~**Zone**~~ والنسخ الجاهزه مثل ~~**Olarila**~~ ايضا سنتجنب برامج **توني ماك** \(**unibeast** و **multibeast**\) قدر المستطاع بسبب انها **مغلقه المصدر** ونقص بعض الاشياء الاساسيه في الكونفق التي قد تؤدي الى حجب حساب ال **iCloud** المرتبط بالهاكنتوش وعيوب [اخرى](https://github.com/khronokernel/Tonymcx86-stance)

