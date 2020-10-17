# الجيل السابع laptop
| الدعم | الاصدار |
| :--- | :--- |
| بداية الدعم على الماك | macOS 10.12, Sierra |

إذا كنت تريد طريقه انشاء الكونفق يدويا ولك معرفه باللغه الانجليزي [هنا ](https://dortania.github.io/OpenCore-Install-Guide/config-laptop.plist/skylake.html)رابط يشرح كيفيه انشاء الكونفق للجيل السادس  لللابتوبات

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
	| 00001B59 | يستخدم مع  HD615,HD620,HD630,HD640,HD650 |
	| 00001659 | خيار بديل في حاله مواجهه اي مشاكل |
	| 0000C087 | مخصص ل UHD617 و UHD620 |

	في حاله عدم وجود طريقه لتحديد حجم رامات الكرت ==DVMT== في البايوس, قد تواجه كيرنل بانك في الاقلاع, ينصح باضافه الاتي:

	| عنوان  | TYPE | القيمة | ملاحظة |
	| :--- | :--- | :--- | :--- |
	| framebuffer-patch-enable | Data | 01000000 | تفعيل باتشات |
	| framebuffer-stolenmem | Data | 00003001 |  |
	| framebuffer-fbmem | Data | 00009000 |  |
	
	اذا كان لديك كرت **UHD620** تحتاج الى اضافه:

	| عنوان  | النوع | القيمة | ملاحظة |
	| :--- | :--- | :--- | :--- |
	| device | Data | 16590000 | تغيير اسم الكرت حتى يتم دعمه |

	اذا كان لديك كرت من فئه `HD6XX` (لايشمل `UHD6XX`)
	قد تواجه مشكله وهي عند توصيل اي شاشه اضافيه يحصل كيرنل بانك. هنا بعض الباتشات لحل المشكله:
	
	- من 0306 الى 0105
	
	| عنوان  | TYPE | القيمة |
	| :--- | :--- | :--- |
	| framebuffer-con1-enable | Data | 01000000 |
	| framebuffer-con1-alldata | Data | 01050A00 00080000 87010000 02040A00 00080000 87010000 FF000000 01000000 20000000 |
	
	- من 0204 الى 0105
	| عنوان  | TYPE | القيمة |
	| :--- | :--- | :--- |
	| framebuffer-con1-enable | Data | 01000000 |
	| framebuffer-con1-alldata | Data | 01050A00 00080000 87010000 03060A00 00040000 87010000 FF000000 01000000 20000000 |
	
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

	
