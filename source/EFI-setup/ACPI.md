---
description: واهميته مع قائمه الملفات الضروريه و كيفيه انشائها للهاكنتوش ACPI تعريف ما هو ال 
---

# ACPI

???+ Warning "تنبيه"
	ملف `dsdt.aml` لايوضع في الاوبن كور.
	وتاكد من عدم تكرار الملف بعده صيغ. مثلا تكرار نفس الملف بصيغتين `.dsl` و `.aml`.

???+ Failure "لا يعمل على الماك"
	برنامج SSDT-time **لن يعمل على الماك**, تحتاج ان تستخدم ويندوز او لينكس **على نفس الجهاز** حتى تقوم بالخطوات داخل برنامج ssdttime.

## ما هو ال ACPI؟

كما ذكرنا سابقا فملفات ال ACPI هي اشبه بخريطه الكمبيوتر للنظام, وبما ان الماك غير مدعوم على اجهزه الكمبيوتر بشكل رسمي سوف نحتاج الى التعديل على هذه الخريطه.
الملفات المبنية على هذا المعيار هي (Differentiated System Description Table)==DSDT== وهي الخريطة الاساسية التي تحتوي على الكنترولرات المدمجة  (embedded controllers) ساعه النظام و انوية المعالج وغيرها.

بينما ال  (**Secondary System Description Table**)  ==SSDT== يحتوي على معلومات ثانوية فقط,
ظيمكنك التفكير بان ==DSDT== هي خريطة المشروع بينما ==SSDT== هي ملاحظات اضافية.

## مفردات الجدول

- الجيل
	- جيل المعالج

- المعالج
	- اي SSDT يتعلق بالمعالج مثلا لتفعيل التحكم بالطاقه من النظام.

- كنترلورات مدمجة(Embedded controllers(==EC==))
	- جميع اجهزه انتل الحديثة تحتوي على ==EC== وحتى عده اجهزه AMD تظهره بملف ال DSDT لكن بشكل عام هذه الكنتلورات غير مدعومة بشكل رسمي من الماك, وقد تسبب بانك في الكيرنل. لذلك يجب اخفائها من النظام لكن من نظام كاتلينا فما فوق اصبح من الاجباري وجود جهاز ==EC== لذلك سنحتاج الى كتابه جهاز زائف.

	- المشكلة ان ال ==EC== في الابتوبات هو الذي يتحكم بالاختصارات و اظهار حالة البطارية لذلك يجب تفعيله,لكن تغيير اسم ال ==EC== قد يسبب بمشاكل في نظام ويندوز, لذلك انشاء EC زائف مع ابقاء الحقيقي فعال هو الحل الافضل
	
- ساعة AWAC للنظام
	- جميع مذربوردات فئة 300 (تشمل مذربودرات Z370) من انتل تاتي مع ساعة AWAC الجديدة مفعله بشكل افتراضي. وهذه تعتبر مشكله لان نظام الماك لحد الان لا يدعم التعامل معها, لذلك يجب علينا اجبار استخدام ساعات RTC القديمة او انشاء ساعه زائفة من اجل النظام	
	
- NVRAM 

	- ال ==NVRAM== هي مساحه تخزين داخل اجهزه للماك تسجل فيها اعدادات النظام المؤقته مثل سطوع الشاشه,علو الصوت,اعدادات الوقت وغيرها, وهي موجوده في الماك فقط وقد تحتاج الى تعديل بعض الاشياء اذا لم تعمل تلقائيا.

## Pc

| **الجيل** | **المعالج** | **EC** | **EC-USBX** | **AWAC** | **NVRAM** | **USB** | **IMEI** |
| :-------: | :-----: | :----: | :------: | :------: | :-------: | :-----: | :-----: |
|  الثالث (Ivy Bridge) | [CPU-PM](#cpu-pmaml) (بعد تثبيث النظام) | [SSDT-EC](#ssdt-ecaml) | - | - | - | - | [SSDT-IMEI](#ssdt-imeiaml) |
|  الرابع(Haswell) | [SSDT-PLUG](#ssdt-plugaml) | [SSDT-EC](#ssdt-ecaml) | - | - | - | - | - | - |
|  الخامس (Broadwell) | [SSDT-PLUG](#ssdt-plugaml) | [SSDT-EC](#ssdt-ecaml) | - | - | - | - | - |
|  السادس (Skylake) | [SSDT-PLUG](#ssdt-plugaml) | [SSDT-EC](#ssdt-ecaml) | [SSDT-USBX](#ssdt-usbxaml) | - | - | - | - |
|  السابع (Kaby Lake) | [SSDT-PLUG](#ssdt-plugaml) | [SSDT-EC](#ssdt-ecaml) | [SSDT-USBX](#ssdt-usbxaml) | - | - | - | - |
|  الثامن/ التاسع (Coffee Lake) | [SSDT-PLUG](#ssdt-plugaml) | [SSDT-EC](#ssdt-ecaml) | [SSDT-USBX](#ssdt-usbxaml) | [SSDT-AWAC](#ssdt-awacaml) | [SSDT-PMC](#ssdt-pmcaml) | - | - |
|  العاشر (Comet Lake) | [SSDT-PLUG](#ssdt-plugaml) | [SSDT-EC](#ssdt-ecaml) |[SSDT-USBX](#ssdt-usbxaml) | [SSDT-AWAC](#ssdt-awacaml) | - | [SSDT-RHUB](#ssdt-rhubaml) | - |
| AMD Ryzen (17h) | [SSDT-CPUR for B550](#ssdt-b550-cpuraml) | [SSDT-EC](#ssdt-ecaml) | [SSDT-USBX](#ssdt-usbxaml) | - | - | - | - |

- Backlight
	- SSDTs تستخدم لتصحيح التحكم بسطوع الشاشة في النظام.
	
- I2C Trackpad
	- SSDTs تستخدم لتفعيل تعريف VoodooI2C لتعريف تراك بادات تستخدم هذا البروتكول.
	
- IRQ 
	- يستخدم لتصحيح بعض التعارضات داخل ال DSDT, يستخدم للابتوبات بشكل عام.
	- اجهزه من الجيل السادس فما فوق من النادر ان تعاني من هذه المشكله, هذه الSSDT موجهه بشكل اكبر للجيل الخامس او اقدم.
	
## Laptop

**يرجى الانتباة لعمود IRQ اخر الجدول لاظهاره قم بسحب الجدول في الاسفل الى اليسار**

| **الجيل** | **المعالج** | **EC** | **EC-USBX** | **Backlight** | **I2C Trackpad** | **AWAC** | **USB** | **IMEI** | **IRQ** |
| :-------: | :-----: | :----: | :-------: | :-----------: | :--------: | :------: | :-----: | :-----: | :-----: |
|  الثالث (Ivy Bridge) | [CPU-PM](#cpu-pmaml) (بعد تثبيث النظام) | [SSDT-EC](#ssdt-ecaml) | - | [SSDT-PNLF](#ssdt-pnlfaml) | - | - | - | [SSDT-IMEI](#ssdt-imeiaml) | [SSDT-HPET](#ssdt-hpetaml) |
|  الرابع(Haswell)  | [SSDT-PLUG](#ssdt-plugaml) | [SSDT-EC](#ssdt-ecaml) | - | [SSDT-PNLF](#ssdt-pnlfaml)| [SSDT-XOSI](#ssdt-xosiaml) | - | - | - | [SSDT-HPET](#ssdt-hpetaml) |
|  الخامس (Broadwell)| [SSDT-PLUG](#ssdt-plugaml) | [SSDT-EC](#ssdt-ecaml) | - | [SSDT-PNLF](#ssdt-pnlfaml) | [SSDT-XOSI](#ssdt-xosiaml) | - | - | - | [SSDT-HPET](#ssdt-hpetaml) |
|  السادس (Skylake)  | [SSDT-PLUG](#ssdt-plugaml) | [SSDT-EC](#ssdt-ecaml) | [SSDT-USBX](#ssdt-usbxaml) | [SSDT-PNLF](#ssdt-pnlfaml) | [SSDT-XOSI](#ssdt-xosiaml) | - | - | - | - |
|  السابع (Kaby Lake) | [SSDT-PLUG](#ssdt-plugaml) | [SSDT-EC](#ssdt-ecaml) | [SSDT-USBX](#ssdt-usbxaml) | [SSDT-PNLF](#ssdt-pnlfaml) | [SSDT-XOSI](#ssdt-xosiaml) | - | - | - | - |
|  الثامن (Coffee Lake) | [SSDT-PLUG](#ssdt-plugaml) | [SSDT-EC](#ssdt-ecaml) | [SSDT-USBX](#ssdt-usbxaml) | [SSDT-PNLF-CFL](#ssdt-pnlfaml) | [SSDT-XOSI](#ssdt-xosiaml) | [SSDT-AWAC](#ssdt-awacaml) | - | - | - |
|  التاسع (Coffee Lake) | [SSDT-PLUG](#ssdt-plugaml) | [SSDT-EC](#ssdt-ecaml) | [SSDT-USBX](#ssdt-usbxaml) | [SSDT-PNLF-CFL](#ssdt-pnlfaml) | [SSDT-XOSI](#ssdt-xosiaml) | [SSDT-AWAC](#ssdt-awacaml) | - | - | - |
|  العاشر (Comet Lake) | [SSDT-PLUG](#ssdt-plugaml) | [SSDT-EC](#ssdt-ecaml) | [SSDT-USBX](#ssdt-usbxaml) | [SSDT-PNLF-CFL](#ssdt-pnlfaml)| [SSDT-XOSI](#ssdt-xosiaml) | [SSDT-AWAC](#ssdt-awacaml) | - | - | - |
|  العاشر (Ice Lake) | [SSDT-PLUG](#ssdt-plugaml) | [SSDT-EC](#ssdt-ecaml) | [SSDT-USBX](#ssdt-usbxaml) | [SSDT-PNLF-CFL](#ssdt-pnlfaml) | [SSDT-XOSI](#ssdt-xosiaml) | [SSDT-AWAC](#ssdt-awacaml) | [SSDT-RHUB](#ssdt-rhubaml) | - | - |

???+ Warning "تنبية"
	جميع ملفات ال SSDT التي تنتهي ب `aml.` او `dsl.` توضع في EFI/OC/ACPI


### CPU-PM.aml

???+ Warning "تنبية"
	هذا ال SSDT يتم عمله بعد تثبيت النظام.

- ماذا يعمل هذا ال SSDT؟

	هذا الSSDT يقوم بتفعيل التحكم بالطاقه على معالجات الجيل الثاني(**غير مدعومة**) و الجيل الثالث على الابتوبات.

سوف تحتاج الى سكربت [ssdtPRGen](https://github.com/Piker-Alpha/ssdtPRGen.sh) لعمل الملف

![](https://dortania.github.io/OpenCore-Post-Install/assets/img/prgen-run.224e35cf.png)

بعد انتهاء عمل البرنامج ستجد ملف SSDT.aml موجود في `/Users/your-name>/Library/ssdtPRGen/ssdt.aml`

 يمكنك ايجاده بسهوله بختصار Cmd+Shift+G ثم لصق`~/Library/ssdtPRGen/`

بعد ذلك ننصحك بتغيير اسم الملف الى SSDT-pm.aml حتى تجده بشكل اسهل.


### SSDT-EC.aml

- ماذا يعمل هذا ال SSDT؟

	هذا ال SSDT يقوم بعمل  EC مزيف للاصدار كاتلينا(10.15+) فما فوق, لان النظام لا يعمل بدونها.

سوف تحتاج الى سكربت [SSDTTime](https://github.com/corpnewt/SSDTTime)

??? info "طريقه تحميل السكربت"
	تحمل السكربت بالضغط على زر Code ثم Download ZIP لتحميل السكربت كامل 
	![](/img/Github-zip.png)

![](/img/EFI-setup/ACPI/dumb-dsdt.png)

بعد فتح السكربت قم بختيار Dump DSDT (في هذه الحالة رقم 8) حتى ناخذ ال DSDT الاساسي.

بعد ذلك اختار رقم **2 اذا كان جهازك مكتبي و رقم 3 اذا كان جهازك لابتوب.**

بعد ذلك ستجد الSSDT موجود في ملف جديد اسمه Results موجود في موقع البرنامج على جهازك.

### SSDT-USBX.aml
- ماذا يعمل هذا ال SSDT؟

	هذا ال SSDT ضروري للجيل السادس فما فوق من معالجات انتل ومعالجات Ryzen.


قم بتحميل (**قم بالضغط على زر download**) [SSDT-USBX.aml](https://github.com/dortania/OpenCore-Post-Install/blob/master/extra-files/SSDT-USBX.aml) وضعه في ملف ال ACPI.

### SSDT-PLUG.aml

- ماذا يعمل هذا ال SSDT؟

	يقوم هذا الSSDT بتفعيل التحكم بطاقه المعالج من الماك للجيل الرابع فما فوق من معالجات انتل.

سوف تحتاج الى سكربت [SSDTTime](https://github.com/corpnewt/SSDTTime)

??? info "طريقه تحميل السكربت"
	تحمل السكربت بالضغط على زر Code ثم Download ZIP لتحميل السكربت كامل 
	![](/img/Github-zip.png)

![](/img/EFI-setup/ACPI/dumb-dsdt.png)

بعد فتح السكربت قم بختيار Dump DSDT (في هذه الحالة رقم 8) حتى ناخذ ال DSDT الاساسي.
ثم اختار رقم 4 

بعد ذلك ستجد `SSDT-PLUG.aml` موجود في ملف جديد اسمه Results موجود في موقع البرنامج على جهازك.

### SSDT-B550-CPUR.aml
- ماذا يعمل هذا ال SSDT؟

	هذا SSDT ضروري لكل مذربوردات B550 من AMD.

حمله من [هنا](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-CPUR.aml)(**قم بالضغط على زر download**) ثم قم بوضعه بملف ACPI

### SSDT-AWAC.aml

- ماذا يعمل هذا ال SSDT؟

	يقوم بحل مشكله ساعه AWAC المزيد من التفاصيل [هنا](#_1)
??? info "قائمة المذربوردات التي تحتاج هذا ال SSDT"
	* B360
	* B365
	* H310
	* H370
	* Z370 (مذربوردات Gigabyte و Asrock مع بايوسات جديدة.)
	* Z390
	* B460
	* Z490
	* 400 series (الجيل العاشر, يشمل Z490)
	* 495 series (جيل عاشر نسخه 10nm(Comet lake))

سوف تحتاج الى سكربت [SSDTTime](https://github.com/corpnewt/SSDTTime)

??? info "طريقه تحميل السكربت"
	تحمل السكربت بالضغط على زر Code ثم Download ZIP لتحميل السكربت كامل 
	![](/img/Github-zip.png)

![](/img/EFI-setup/ACPI/dumb-dsdt.png)

بعد فتح السكربت قم بختيار Dump DSDT (في هذه الحالة رقم 8) حتى ناخذ ال DSDT الاساسي.
ثم اختار رقم 6 

???+ info "ملاحظة"
	قد تظهر لك كلمه `ssdt-awac not needed` بحيث بعض الحالات الاجهزه لاتحتاج هذا ال ssdt. اذا ظهرت لك هذه الرساله تخطى هذا الملف.
	![](/img/EFI-setup/ACPI/awac-notneeded.jpg)

بعد ذلك ستجد `SSDT-AWAC.aml` او `SSDT-RTC0.aml` على حسب جهازك, موجود في ملف جديد اسمه Results موجود داحل موقع البرنامج على جهازك.


### SSDT-PMC.aml
- ماذا يعمل هذا ال SSDT؟

	هذا ال SSDT يقوم بحل مشاكل NVRAM على مذربوردات فئه 300 من انتل (بستثناء Z370) 

سوف تحتاج الى سكربت [SSDTTime](https://github.com/corpnewt/SSDTTime)

??? info "طريقه تحميل السكربت"
	تحمل السكربت بالضغط على زر Code ثم Download ZIP لتحميل السكربت كامل 
	![](/img/Github-zip.png)

![](/img/EFI-setup/ACPI/dumb-dsdt.png)

بعد فتح السكربت قم بختيار  Dump DSDT (في هذه الحالة رقم 8) حتى ناخذ ال DSDT الاساسي.
ثم اختار رقم 5

بعد ذلك ستجد `SSDT-PMC.aml` موجود في ملف جديد اسمه Results موجود داخل موقع البرنامج على جهازك.

### SSDT-RHUB.aml

- ماذا يعمل هذا ال SSDT؟

	يقوم بحل مشكله بعض المذربوردات من فئه 400(asus و ASRock لاتعاني من هذه المشكله, msi غير مؤكد) كسرت قواعد ال ACPI وتسبب مشاكل في اقلاع الماك.

سوف تحتاج الى سكربت [SSDTTime](https://github.com/corpnewt/SSDTTime)

??? info "طريقه تحميل السكربت"
	تحمل السكربت بالضغط على زر Code ثم Download ZIP لتحميل السكربت كامل 
	![](/img/Github-zip.png)

![](/img/EFI-setup/ACPI/dumb-dsdt.png)

بعد فتح السكربت قم بختيار Dump DSDT (في هذه الحالة رقم 8) حتى ناخذ ال DSDT الاساسي.

`7. USB Reset`  ثم اختار

بعد ذلك ستجد `SSDT-RHUB.aml` موجود في ملف جديد اسمه Results موجود في موقع البرنامج على جهازك.

### SSDT-PNLF.aml

- ماذا يعمل هذا ال SSDT؟

	يقوم بحل مشكله التحكم بسطوع شاشه على الابتوبات.

- [SSDT-PNLF.aml](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-PNLF.aml)
	
	يعمل لكل الاجهزه تحت الجيل الثامن.

- [SSDT-PNLF-CFL.aml](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-PNLF-CFL.aml)
	
	مخصص للجيل الثامن فما فوق.

### SSDT-XOSI.aml

- ماذا يعمل هذا ال SSDT؟
	
	يقوم هذا ال SSDT بتجهيز خريطه الجهاز حتى يتم تعريف التراك باد بستخدام [Voodoi2c](https://tutorial.هاكنتوش.com/EFI-setup/gathering-kexts/#_3)

حمله من [هنا](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-XOSI.aml)(**قم بالضغط على زر download**) ثم قم بوضعه بملف ACPI

### SSDT-HPET.aml

- ماذا يعمل هذا ال SSDT؟
	
	يقوم هذا الSSDT بحل مشاكل تعارض IRQ في خرائط ال DSDT, وهو ضروري للابتوبات.

سوف تحتاج الى سكربت [SSDTTime](https://github.com/corpnewt/SSDTTime)

??? info "طريقه تحميل السكربت"
	تحمل السكربت بالضغط على زر Code ثم Download ZIP لتحميل السكربت كامل 
	![](/img/Github-zip.png)

![](/img/EFI-setup/ACPI/dumb-dsdt.png)

بعد فتح السكربت قم بختيار Dump DSDT (في هذه الحالة رقم 8) حتى ناخذ ال DSDT الاساسي.

بعد ذلك اختار رقم 1.

ثم عند ظهور هذه الشاشه **اضغط انتر**

![](/img/EFI-setup/ACPI/ssdt-hpet.png)

بعد ذلك ستجد الSSDT موجود في ملف جديد اسمه Results موجود في موقع البرنامج على جهازك.

### SSDT-IMEI.aml

- ماذا يعمل هذا ال SSDT؟

	يقوم بحل مشكله مذروبوردات الجيل السادس(**مثل H61, B65, Q65, P67, H67, Q67, Z68...**) مع معالجات الجيل الثالث. لانها غير مدعومه بالماك بشكل رسمي, ويحل مشكله عدم ظهور المذربورد بشكل صحيح في ال ACPI.

- **لا تضعه اذا لم يكن لديك مذربورد من الجيل السادس**

قم بتحميل (**قم بالضغط على زر download**) [SSDT-IMEI.aml](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-IMEI.amll) وضعه في ملف ال ACPI.
