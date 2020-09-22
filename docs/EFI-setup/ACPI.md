# ACPI

## ما هو ال ACPI?

كما ذكرنا سابقا فملفات ال ACPI هي اشبه بخريطه الكمبيوتر للنظام, وبما ان الماك غير مدعوم على اجهزه الكمبيوتر بشكل رسمي سوف نحتاج الى التعديل على هذه الخريطه.
الملفات المبنية على هذا المعيار هي (Differentiated System Description Table)==DSDT== وهي الخريطة الاساسية التي تحتوي على لوحات التحكم الداخلية (embedded controllers) ساعه النظام و انوية المعالج وغيرها.

بينما ال  (**Secondary System Description Table**)  ==SSDT== يحتوي على معلومات ثانوية فقط,
ظيمكنك التفكير بان ==DSDT== هي خريطة المشروع بينما ==SSDT== هي ملاحظات اضافية.

نظام الماك دقيق جدا بالنسبة للاجهزه الموجوده في هذه خريطة, لذلك يجب تصحيحة للتاكد من عمل النظام بشكل صحيح.
الاجهزه الرئيسية التي يجب تصحيحها:

- لوحات تحكم مدمجة(Embedded controllers(EC))
	- جميع اجهزه انتل الحديثة تحتوي على EC وحتى عده اجهزه AMD تظهره بملف ال DSDT لكن بشكل عام هذه اللوحات غير مدعومة بشكل رسمي من الماك, وقد تسبب بانك في الكيرنل. لذلك يجب اخفائها من النظام لكن من نظام كاتلينا فما فوق اصبح من الاجباري وجود جهاز EC لذلك سنحتاج الى كتابه جهاز زائف.

	- المشكلة ان ال EC في الابتوبات هو الذي يتحكم بالاختصارات و اظهار حالة البطارية لذلك يجب تفعيله,لكن تغيير اسم ال EC قد يسبب بمشاكل في نظام ويندوز, لذلك انشاء EC زائف مع ابقاء الحقيقي فعال هو الحل الافضل 

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
| AMD (17h) | [SSDT-CPUR for B550](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-CPUR.aml) | ^^ | N/A | ^^ | N/A |

## لابتوب

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
