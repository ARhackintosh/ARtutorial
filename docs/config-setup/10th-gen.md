# الجيل العاشر
| الدعم | الاصدار |
| :--- | :--- |
| بداية الدعم على الماك | macOS 10.15, High Sierra |

انشاء الكونفق يدويا ولك معرفه باللغه الانجليزية [هنا ](https://dortania.github.io/OpenCore-Install-Guide/config.plist/comet-lake.html)رابط يشرح كيفيه انشاء الكونفق للجيل العاشر

**هذه الصفحة معدة على اساس انك تستخدم كونفقات هاكنتوش بالعربي**

???+ Warning "تنبية"
	قد تكون الصور احيانا غير محدثة او لاتظهر التعديلات الصحيحه
	**يرجى دائما اتباع الكلام المكتوب وتجاهل الصور** وظيفتها هي توضيح الاقسام لا غير الا لبعض الاستثانئات

## DeviceProperties

### Add

![](/img/config-setup/deviceproperties.png)

???+ info "PciRoot(0x0)/Pci(0x2,0x0)"
	هذا القسم مخصص لتحديد باتشات ال Framebuffer لكيكست [WhateverGreen](/EFI-setup/gathering-kexts.md#gpus)

	| AAPL,ig-platform-id | وصف |
	| :--- | :--- |
	| 07009B3E | يستخدم لكروت انتل المدمحة في حاله استخدامها لعرض الشاشة |
	| 0300C89B | يستخدم لكروت انتل المدمجه في حاله استخدامها لعمليات حسابيه فقط بدون عرض الشاشه |
	
	ايضا اذا كنت تستخدم**الكرت المدمج لعرض الشاشه** ستحتاج الى اضافه اعدادت اضافيه :

	| عنوان  | النوع | القيمة | ملاحظة |
	| :--- | :--- | :--- | :--- |
	| AAPL,ig-platform-id | Data | 07009B3E | |
	| framebuffer-patch-enable | Data | 01000000 | |
	| framebuffer-stolenmem | Data | 00003001 | |

	**مثال** للاعدادت في الكونفق
	
	![](/img/config-setup/deviceproperties-example.png)
