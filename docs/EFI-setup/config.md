# الكونفق

اذا كنت تستخدم كلوفر مسبقا فا فكره الكونفق هي قريبه لاكن هناك اختلافات كبيرة

عكس كلوفر الذي بامكانك فيه اضافه التعريفات وملفات acip بدون اي خطوه اضافيه.
في اوبن كور تحتاج ان تضيف كل الكيكستات بالترتيب و ملفات ال acpi الى ملف الكونفق ليتم تفعيلها اثناء الاقلاع.
لذلك استخدام كونفقات مجهزه مسبقا غير ممكن بدون تعديلها الا اذا استخدمت ملف  EFI جاهز بالكامل

لذلك الطريقه الاكثر شهره هي تعديل على العينة التي تاتي مع اوبن كور واضافه الاعدادات الضرورية,
لكن لتسهيل عمليه البناء قمنا في هاكنتوش بالعربي بعمل مجموعه من الكونفقات المجهزه مسبقا تحتوي على الاعدادات الاجباريه لكل جيل من المعالجات, يتبقى فقط على المستخدم اضافه الخصائص التي تعتمد على الجهاز مثل نوع كرت الشاشه,نوع المذربورد,اعدادات بايوس, الخ..

???+ info "تنبيه"
    حاليا الكونفقات موجوده لمعالجات انتل على الابتوبات ومعالجات انتل العاديه للمكتبي فقط, بقيه المعالجات ستبني من العينه داخل اوبن كور

**[رابط التحميل](https://github.com/ARhackintosh/OC-Configs)**

???+ tip "ملحوظه"
     لتنزيل الكونفقات قم بالضغط على code ثم Download zip وسوف يحمل كامل المشروع داخل ملف مضغوط ثم قم بتغيير اسم الملف الى config.plist 
    
    ![](/img/Github-zip.png)

ملفات الكونفق التي يجب تحميلها

Pc

| اسم الجيل | السلسة | اسم الملف |
| :--- | :--- | :--- |
| [3-Ivy Bridge](/config-setup/3rd-gen) | 3XXX | [3rdgen-ivy-bridge.plist](https://github.com/ARhackintosh/OC-Configs/blob/master/3rdgen-ivy-bridge.plist)  |
| [4-Haswell](/config-setup/4th-gen) | 4XXX | [4thgen-Haswell.plist](https://github.com/ARhackintosh/OC-Configs/blob/master/4thgen-Haswell.plist) |
| [6-Skylake](/config-setup/6th-gen) | 6XXX | [6thgen-Skylake.plist](https://github.com/ARhackintosh/OC-Configs/blob/master/6thgen-Skylake.plist) |
| [7-Kaby Lake](/config-setup/7th-gen) | 7XXX | [7thgen-Kaby-lake.plist](https://github.com/ARhackintosh/OC-Configs/blob/master/7thgen-Kaby-lake.plist) |
| [8/9-Coffee Lake](/config-setup/8th-gen) | 8XXX-9XXX | [8th-9thgen-Coffeelake.plist.plist](https://github.com/ARhackintosh/OC-Configs/blob/master/8th-9thgen-Coffeelake.plist) |
| [10-Comet Lake](/config-setup/10th-gen) | 10XXX | [10thgen-Comet-lake.plist](https://github.com/ARhackintosh/OC-Configs/blob/master/10thgen-Comet-lake.plist) |

Laptop

| اسم الجيل | السلسة | اسم الملف |
| :--- | :--- | :--- |
| [3-Ivy Bridge](/config-setup/laptops/3rd-gen/) | 3XXX | [3rdgen-laptops.plist](https://github.com/ARhackintosh/OC-Configs/blob/master/laptops/3rdgen-laptops.plist)  |
| [4-Haswell](/config-setup/laptops/4th-gen/) | 4XXX | [4thgen-laptops.plist](https://github.com/ARhackintosh/OC-Configs/blob/master/laptops/4thgen-laptops.plist) |
| [5-Broadwell](/config-setup/laptops/5th-gen/) | 5XXX | [5thgen-laptops.plist](https://github.com/ARhackintosh/OC-Configs/blob/master/laptops/5thgen-laptops.plist) |
| [6-Skylake](/config-setup/laptops/6th-gen/) | 6XXX | [6thgen-laptops.plist](https://github.com/ARhackintosh/OC-Configs/blob/master/laptops/6thgen-laptops.plist) |
| [7-Kaby Lake](/config-setup/laptops/7th-gen/) | 7XXX | [7thgen-laptops.plist](https://github.com/ARhackintosh/OC-Configs/blob/master/laptops/7thgen-laptops.plist) |
| [8-Coffee Lake](/config-setup/laptops/8th-gen/) | 8XXX | [8th-9thgen-Coffeelake.plist.plist](https://github.com/ARhackintosh/OC-Configs/blob/master/laptops/8thgen-laptops.plist) |
| [9-Coffee Lake](/config-setup/laptops/9th-gen/) | 9XXX | [9thgen(or comet-lake)-laptops.plist](https://github.com/ARhackintosh/OC-Configs/blob/master/laptops/9thgen(or comet-lake)-laptops.plist) |
| [10-Comet Lake](/config-setup/laptops/comet-lake/) | 10XXX | [9thgen(or comet-lake)-laptops.plist](https://github.com/ARhackintosh/OC-Configs/blob/master/laptops/9thgen(or comet-lake)-laptops.plist) |
| [10-ice Lake](/config-setup/laptops/ice-lake/) | 10XXG | [10thgen-laptops.plist](https://github.com/ARhackintosh/OC-Configs/blob/master/laptops/10thgen-laptops.plist) |

## البرامج

- [ProperTree](https://github.com/corpnewt/propertree)

    هذا هو برنامج متكامل لتعديل كونفقات اوبن كور مبني على python ومتوافق مع جميع الانظمه(يشمل لينكس)

    طريقه تحميل البرنامج هي مثل الكونفقات 

- [GenSMbios](https://github.com/corpnewt/GenSMBIOS)
	
	برنامج مخصص لتوليد معلومات عن موديل الجهاز (==SMbios==) مثل السيريال ورقم اللوحه وغيرها من المعلومات.

## نقل الكونفق

لنقل الكونفق لل USB 

اذا كنت تستخدم احد الكونفقات الجاهزه من هاكنتوش بالعربي, فقم بتغيير اسمه الى `config.plist` بعد ذلك قم نسخة الى `EFI/OC`

في حالة عدم توفر كونفق جاهز لجهازك اذهب الى ملف docs الموجود في الملف المضغوط الخاص ب Opencore ثم قم بنسخ Sample.plist بعدها قم بتغيير اسمه الى `config.plist` ولصقة في `EFI/OC` 

![](/img/EFI-setup/archive-sample.png)

طبعا هذه الكونفقات ناقصة وليست مكتملة لذلك سنشرح في قسم تجيهز الكونفق االخطوات والتعديلات الضرورية لكل جيل.

## اضافه ملفات الكيكستات و ACPI وتعريفات الفريميور

لفتح برنامج Propertree على ويندوز اختار ProperTree.bat اما لينكس فختار ProperTree.command

بعد فتح البرنامج اضغط **Ctrl + o** واختار ملف الكونفق الموجود على ال usb بعد نقله.

بعد ذلك اضغط **Ctrl + Shift + R** ثم اختار ملف ال EFI على ال usb

البرنامج تلقائيا سيقوم باضافه جميع الملفات من كيكستات و ACPI و تعريفات فريموير الى الكونفق.

بعد ذلك ستلاحظ ان الكيكستات و ال acpi تمت اضافتها

![](/img/EFI-setup/propertree-snapshot.png)
