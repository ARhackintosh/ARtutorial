---
description: USB غير لازمة, مع كيفيه نقل الملف الى (Tools) وادوات (Drivers) من حذف تعريفات (OC) الخاص بالاوبن كور EFI كيفيه تجهيز ملف 
---
# نقل ملفات اوبن كور

لتجهيز ملفات اوبن كور حمل ملف ال EFI [من صفحه OpenCorePkg على github]({{ oc.git }})

بالنسبة للنسخ هناك نسختان من اوبن كور:

- ==Debug==: هذه نسخه مخصصه لاظهار كامل معلومات الاقلاع, وتساعد بشكل كبير على حل مشاكل تثبيت الهاكنتوش
الاقلاع فيها ابطئ بشكل عام, لكن تحويل النسخه الى ==Release== سهل جدا.

- ==Release==: اقلاع اسرع بشكل كبير, لكن بدون اي معلومات مفيدة عن اقلاع النظام وهذا خطأ شائع جدا يقع فيه الجدد في الهاكنتوش.
لذلك يجب استخدام فقط بعد انتهاء عملية الاقلاع **والتاكد من خلو النظام من المشاكل**

## ملفات الفريموير

بعد التنزيل قم بنسخ ملف ال`EFI` الموجود داخل `X64` من داخل الارشيف ولصقه في قسم ال EFI من ال USB

بعد ذلك توجه الى ``EFI/OC/Drivers`` وقم بحذف جميع الملفات ماعدا ==OpenRuntime.efi== **و** ==OpenCanopy.efi== لتفعيل الواجهه الرسوميه للاوبن كور

![](/img/Opencore/drivers.png)

بعد ذلك قم بتنزيل **[Hfsplus.efi](https://github.com/acidanthera/OcBinaryData/blob/master/Drivers/HfsPlus.efi)** عنطريق الضغط على زر download  ثم ضعه داخل ملف ``EFI/OC/Drivers``

## Tools
توجه الى ``EFI/OC/Tools`` وقم بحذف جميع الملفات الا ==OpenShell.efi== لانه يساعد على حل المشاكل في الاقلاع.

![](/img/Opencore/tools.png)

???+ Warning "تنبيه"
	توضع ملفات الكيكست(`kext.`) في ``EFI/OC/Kexts``
	
	ملفات ال ACPI (`.dsl`و  `.aml`) في `EFI/OC/ACPI`
	
	واخيرا تعريفات الفريموير(`efi.`) في `EFI/OC/Drivers`
