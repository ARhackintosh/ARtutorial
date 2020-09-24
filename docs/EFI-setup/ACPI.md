# ACPI

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

| **الجيل** | **المعالج** | **EC** | **AWAC** | **NVRAM** | **USB** |
| :-------: | :-----: | :----: | :------: | :-------: | :-----: |
| الجيل الثالث (Ivy Bridge) | [CPU-PM](https://dortania.github.io/OpenCore-Post-Install/universal/pm.html#sandy-and-ivy-bridge-power-management) (Run in Post-Install) | [SSDT-EC](https://dortania.github.io/Getting-Started-With-ACPI/Universal/ec-fix.html) | N/A | N/A | N/A |
| الجيل الرابع(Haswell) | [SSDT-PLUG](https://dortania.github.io/Getting-Started-With-ACPI/Universal/plug.html) | ^^ | ^^ | ^^ | ^^ |
| الجيل الخامس (Broadwell) | ^^ | ^^ | ^^ | ^^ | ^^ |
| الجيل السادس (Skylake) | ^^ | [SSDT-EC-USBX](https://dortania.github.io/Getting-Started-With-ACPI/Universal/ec-fix.html) | ^^ | ^^ | ^^ |
| الجيل السابع (Kaby Lake) | ^^ | ^^ | ^^ | ^^ | ^^ |
| الجيل الثامن/ التاسع (Coffee Lake) | ^^ | ^^ | [SSDT-AWAC](https://dortania.github.io/Getting-Started-With-ACPI/Universal/awac.html) | [SSDT-PMC](https://dortania.github.io/Getting-Started-With-ACPI/Universal/nvram.html) | ^^ |
| الجيل العاشر (Comet Lake) | ^^ | ^^ | ^^ | N/A | [SSDT-RHUB](https://dortania.github.io/Getting-Started-With-ACPI/Universal/rhub.html) |
| AMD Ryzen (17h) | [SSDT-CPUR for B550](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-CPUR.aml) | ^^ | N/A | ^^ | N/A |

- Backlight
	- كيكستات تستخدم لتصحيح التحكم بسطوع الشاشة في النظام.
	
- I2C Trackpad
	- كيكستات تستخدم لتفعيل تعريف VoodooI2C لتعريف تراك بادات تستخدم هذا البروتكول.
	
- IRQ 
	- يستخدم لتصحيح بعض التعارضات داخل ال DSDT, يستخدم للابتوبات بشكل عام.
	- اجهزه من الجيل السادس فما فوق من النادر ان تعاني من هذه المشكله, هذه الSSDT موجهه بشكل اكبر للجيل الخامس او اقدم.
	
## Laptop

| **الجيل** | **المعالج** | **EC** | **Backlight** | **I2C Trackpad** | **AWAC** | **USB** | **IRQ** |
| :-------: | :-----: | :----: | :-----------: | :--------------: | :------: | :-----: | :-----: |
| الجيل الثالث (Ivy Bridge) | [CPU-PM](https://dortania.github.io/OpenCore-Post-Install/universal/pm.html#sandy-and-ivy-bridge-power-management) (Run in Post-Install) | [SSDT-EC](https://dortania.github.io/Getting-Started-With-ACPI/Universal/ec-fix.html) | [SSDT-PNLF](https://dortania.github.io/Getting-Started-With-ACPI/Laptops/backlight.html) | N/A | N/A | N/A | [IRQ SSDT](https://dortania.github.io/Getting-Started-With-ACPI/Universal/irq.html) |
| الجيل الرابع(Haswell)  | [SSDT-PLUG](https://dortania.github.io/Getting-Started-With-ACPI/Universal/plug.html) | ^^ | ^^ | [SSDT-GPI0](https://dortania.github.io/Getting-Started-With-ACPI/Laptops/trackpad.html) | ^^ | ^^ | ^^ |
| الجيل الخامس (Broadwell)| ^^ | ^^ | ^^ | ^^ | ^^ | ^^ | ^^ |
| الجيل السادس (Skylake)  | ^^ | [SSDT-EC-USBX](https://dortania.github.io/Getting-Started-With-ACPI/Universal/ec-fix.html) | ^^ | ^^ | ^^ | ^^ | N/A |
| الجيل السابع (Kaby Lake) | ^^ | ^^ | ^^ | ^^ | ^^ | ^^ | ^^ |
| الجيل الثامن (Coffee Lake) | ^^ | ^^ | [SSDT-PNLF-CFL](https://dortania.github.io/Getting-Started-With-ACPI/Laptops/backlight.html) | ^^ | ^^ | ^^ | ^^ |
| الجيل التاسع (Coffee Lake) | ^^ | ^^ | ^^ | ^^ | [SSDT-AWAC](https://dortania.github.io/Getting-Started-With-ACPI/Universal/awac.html) | ^^ | ^^ |
|   الجيل العاشر 14nm+ (Comet Lake) | ^^ | ^^ | ^^ | ^^ | ^^ | ^^ | ^^ |
| الجيل العاشر 10nm (Ice Lake) | ^^ | ^^ | ^^ | ^^ | ^^ | [SSDT-RHUB](https://dortania.github.io/Getting-Started-With-ACPI/Universal/rhub.html) | ^^ |

???+ Warning "تنبية"
	جميع ملفات ال SSDT التي تنتهي ب `aml.` او `dsl.` توضع في EFI/OC/ACPI


### CPU-PM.aml

???+ Warning "تنبية"
	هذا ال SSDT يتم عمله بعد تثبيت النظام.

هذا الSSDT يقوم بتفعيل التحكم بالطاقه على معالجات الجيل الثاني(**غير مدعومة**) و الجيل الثالث على الابتوبات.

سوف تحتاج الى سكربت [ssdtPRGen](https://github.com/Piker-Alpha/ssdtPRGen.sh) لعمل الملف

![](/img/EFI-setup/ACPI/ssdtPRGen.png)

بعد انتهاء عمل البرنامج ستجد ملف SSDT.aml موجود في `/Users/your-name>/Library/ssdtPRGen/ssdt.aml`

 يمكنك ايجاده بسهوله بختصار Cmd+Shift+G ثم لصق`~/Library/ssdtPRGen/`

بعد ذلك ننصحك بتغيير اسم الملف الى SSDT-pm.aml حتى تجده بشكل اسهل.


### SSDT-EC.aml

هذا ال SSDT يقوم بعمل  EC مزيف للاصدار كاتلينا(10.15+) فما فوق, لان النظام لا يعمل بدونها.

سوف تحتاج الى سكربت [SSDTTime](https://github.com/corpnewt/SSDTTime)

??? info "طريقه تحميل السكربت"
	تحمل السكربت بالضغط على زر Code ثم Download ZIP لتحميل السكربت كامل 
	![](/img/Github-zip.png)

![](/img/EFI-setup/ACPI/dumb-dsdt.png)

بعد فتح السكربت قم بختيار رقم 7 حتى ناخذ ال DSDT الاساسي.

بعد ذلك اختار رقم 2 اذا كان جهازك مكتبي و رقم 3 اذا كان جهازك لابتوب.

بعد ذلك ستجد الSSDT موجود في ملف جديد اسمه Results موجود في موقع البرنامج على جهازك.


