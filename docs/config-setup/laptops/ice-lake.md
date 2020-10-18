# ice lake
| الدعم | الاصدار |
| :--- | :--- |
| بداية الدعم على الماك | macOS 10.15, Catalina |

إذا كنت تريد طريقه انشاء الكونفق يدويا ولك معرفه باللغه الانجليزي [هنا ](https://dortania.github.io/OpenCore-Install-Guide/config-laptop.plist/icelake.html)رابط يشرح كيفيه انشاء الكونفق للجيل التاسع  لللابتوبات

**هذه الصفحة معدة على اساس انك تستخدم كونفقات هاكنتوش بالعربي**

???+ Warning "تنبية"
	قد تكون الصور احيانا غير محدثة او لاتظهر التعديلات الصحيحه
	**يرجى دائما اتباع الكلام المكتوب وتجاهل الصور** وظيفتها هي توضيح الاقسام لا غير الا لبعض الاستثانئات
	

## DeviceProperties

### Add

![](/img/config-setup/deviceproperties.png)

???+ info "PciRoot(0x0)/Pci(0x2,0x0)"

	في حاله عدم وجود طريقه لتحديد حجم رامات الكرت ==DVMT== في البايوس, قد تواجه كيرنل بانك في الاقلاع, ينصح باضافه الاتي:

	| عنوان  | TYPE | القيمة | ملاحظة |
	| :--- | :--- | :--- | :--- |
	| framebuffer-patch-enable | Number | 1 | تفعيل باتشات |
	| framebuffer-stolenmem | Data | 00003001 |  |
	| framebuffer-fbmem | Data | 00009000 |  |

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

