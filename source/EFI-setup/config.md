---
description: اساسيات اعداد الكونفق للاوبن كور, وما البرامج التي تحتاجها مع طريقه تعامل الشرح معها.
---

# الكونفق

اذا كنت تستخدم كلوفر مسبقا فا فكره الكونفق هي قريبه لاكن هناك اختلافات كبيرة

عكس كلوفر الذي بامكانك فيه اضافه التعريفات وملفات acip بدون اي خطوه اضافيه.
في اوبن كور تحتاج ان تضيف كل الكيكستات بالترتيب و ملفات ال acpi الى ملف الكونفق ليتم تفعيلها اثناء الاقلاع.
لذلك استخدام كونفقات مجهزه مسبقا غير ممكن بدون تعديلها الا اذا استخدمت ملف  EFI جاهز بالكامل

لذلك الطريقه الاكثر شهره هي تعديل على العينة التي تاتي مع اوبن كور واضافه الاعدادات الضرورية

ملفات الكونفق التي يجب تحميلها

Pc

| اسم الجيل | السلسة | تاريخ الاصدار |
| :--- | :--- | :--- |
| [3-Ivy Bridge](/config-setup/3rd-gen) | 3XXX | 2012 |
| [4-Haswell](/config-setup/4th-gen) | 4XXX | 2013-2014 |
| [6-Skylake](/config-setup/6th-gen) | 6XXX | 2015-2016 |
| [7-Kaby Lake](/config-setup/7th-gen) | 7XXX | 2017 |
| [8/9-Coffee Lake](/config-setup/8th-gen) | 8XXX-9XXX | 2017-2019 |
| [10-Comet Lake](/config-setup/10th-gen) | 10XXX | 2020 |

Laptop

| اسم الجيل | السلسة | تاريخ الاصدار |
| :--- | :--- | :--- |
| [3-Ivy Bridge](/config-setup/laptops/3rd-gen/) | 3XXX | 2012 |
| [4-Haswell](/config-setup/laptops/4th-gen/) | 4XXX | 2013-2014 |
| [5-Broadwell](/config-setup/laptops/5th-gen/) | 5XXX | 2014-2015 |
| [6-Skylake](/config-setup/laptops/6th-gen/) | 6XXX | 2015-2016 |
| [7-Kaby Lake](/config-setup/laptops/7th-gen/) | 7XXX | 2017 |
| [8-Coffee Lake](/config-setup/laptops/8th-gen/) | 8XXX | 2017-2018 |
| [9/10-Coffee Lake plus و Comet Lake](/config-setup/laptops/9th-gen/) | 9XXX-10XXX | 2019-2020 |
| [10-ice Lake](/config-setup/laptops/ice-lake/) | 10XXGX | 2019-2020 |

## البرامج

- [ProperTree](https://github.com/corpnewt/propertree)

    هذا هو برنامج متكامل لتعديل كونفقات اوبن كور مبني على python ومتوافق مع جميع الانظمه(يشمل لينكس)

??? info "طريقه التنزيل"
	تنزيل البرنامج يكون بالضغط على زر Code ثم Download ZIP
	![](/img/Github-zip.png)


- [GenSMbios](https://github.com/corpnewt/GenSMBIOS)
	
	برنامج مخصص لتوليد معلومات عن موديل الجهاز (==SMbios==) مثل السيريال ورقم اللوحه وغيرها من المعلومات.

??? info "طريقه التنزيل"
	تنزيل البرنامج يكون بالضغط على زر Code ثم Download ZIP
	![](/img/Github-zip.png)

## نقل الكونفق

لنقل الكونفق لل USB 

اذهب الى ملف docs الموجود في الملف المضغوط الخاص ب Opencore ثم قم بنسخ Sample.plist بعدها قم بتغيير اسمه الى `config.plist` ولصقة في `EFI/OC` 

![](/img/EFI-setup/archive-sample.png)

## كيفية تعديل الكونفق

في الصفحات القادمة سنطلب من اضافه عناصر جديده للكونفق او تعديلها.

![](/img/EFI-setup/propertree-guide.png)

???+ tip "ملحوظة"

	- key = عنوان 
	- Value = قيمة
	- Type = النوع
	
	هناك عده انواع للمدخلات(السطر) في الكونفق
	
	- data التي تدعم وضع value
	- string وهي عباره عن جملة عادية
	- number رقم
	- Dictionary وهذا يعتببر مثل قسم, بحيث تضع تحته الاعدادت مثل `PciRoot(0x0)/Pci(0x16,0x0)` في الصورة

لانشاء سطر جديد على القسم الذي تريد ان يكون تحته السطر ثم اضغط على + في الكيبورد, ثم قم بتغيير العنوان وحدد نوع السطر.

**مثال عملي على استخدام البرنامج في الشرح:**


![](/img/config-setup/3rd-gen/deviceprop.png)

**عنوان السطر هو نفس عنوان المربع في الاسفل**

???+ note "PciRoot(0x0)/Pci(0x2,0x0)"
	هذا القسم مخصص لتحديد باتشات ال Framebuffer لكيكست [WhateverGreen](/EFI-setup/gathering-kexts#gpus)

	| AAPL,ig-platform-id | وصف |
	| :--- | :--- |
	| 0A006601 | يستخدم لكروت انتل المدمجه في حاله استخدامها لعرض الشاشة |
	| 07006201 | يستخدم لكروت انتل المدمجه في حاله استخدامها لعمليات حسابيه فقط بدون عرض الشاشه |


???+ note "PciRoot(0x0)/Pci(0x16,0x0)"
	اذا كانت لديك مذربورد من الفئة السادسة(H61, B65, Q65, P67, H67, Q67, Z68) ستحتاج الى تغيير رقم جهاز ال IMEI حتى يكون مدعوم,
	قم باضافه الاتي تحت Add
	
	| Value | Type | Key |
	| :--- | :--- | :--- |
	| 3A1E0000 | Data | device-id |

## اضافه ملفات الكيكستات و ACPI وتعريفات الفريميور (سنابشوت)

لفتح برنامج Propertree على ويندوز اختار ProperTree.bat اما لينكس فختار ProperTree.command

بعد فتح البرنامج اضغط **Ctrl + o** واختار ملف الكونفق الموجود على ال usb بعد نقله.

بعد ذلك اضغط **Ctrl + Shift + R** ثم اختار ملف OC **داخل ملف ال EFI** على ال usb

البرنامج تلقائيا سيقوم باضافه جميع الملفات من كيكستات و ACPI و تعريفات فريموير الى الكونفق.

بعد ذلك ستلاحظ ان الكيكستات و ال acpi تمت اضافتها

???+ Warning "تنبيه"
	في كل مرة تقوم باضافه اي ملف جديد على ال efi سواء كيكست او ssdt او غيرة تقوم بعمل سنابشوت مره اخرى

![](/img/EFI-setup/propertree-snapshot.png)

