# الجيل الرابع laptop
| الدعم | الاصدار |
| :--- | :--- |
| بداية الدعم على الماك | OS X 10.8, Mountain Lion |

إذا كنت تريد طريقه انشاء الكونفق يدويا ولك معرفه باللغه الانجليزي [هنا ](https://dortania.github.io/OpenCore-Install-Guide/config-laptop.plist/haswell.html)رابط يشرح كيفيه انشاء الكونفق للجيل الرابع لللابتوبات

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
	| 0500260A | يستخدم عادة مع كروت HD5000,HD5100,HD5200 |
	| 0600260A | يستخدم عادة مع كروت HD4400,HD4600 |

	اعدادت اضافيه:

	| عنوان  | TYPE | القيمة | ملاحظة |
	| :--- | :--- | :--- | :--- |
	| framebuffer-patch-enable | Data | 01000000 | تفعيل باتشات |
	| framebuffer-cursormem | Data | 00009000 | تصحيح حجم الماوس لحل بعد القلتشات |
	
	اذا كان لديك كرت **HD4200,HD4400,HD4600** تحتاج الى اضافه:

	| عنوان  | النوع | القيمة | ملاحظة |
	| :--- | :--- | :--- | :--- |
	| device | Data | 12040000 | تغيير اسم الكرت حتى يتم دعمه |

## Kernel

### Quirks

![](/img/config-setup/kernel-quirks.png)

???+ info "Quirks"
	اعدادات مخصصه للكيرنل.
	
	| العنوان | مفعل | وصف |
	| :--- | :--- | :--- |
	| AppleCpuPmCfgLock | True | غير ضروري اذا تم تعطيل `CFG-Lock` في البايوس |
	| AppleXcpmCfgLock | True | غير ضروري اذا تم تعطيل `CFG-Lock` في البايوس |
	| DisableIOMapper | True | غير ضروري اذا تم تعطيل `VT-D` في البايوس |
	| LapicKernelPanic | False | اجهزه HP ستحتاج تفعيل هذا الاعداد |
	| PanicNoKextDump | True | |
	| PowerTimeoutKernelPanic | True | |
	| XhciPortLimit | True | |

