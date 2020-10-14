# جيل ثالث laptop
| الدعم | الاصدار |
| :--- | :--- |
| بداية الدعم على الماك | OS X 10.7, Lion |
| ملحوظة | كرت الشاشه المدمج لم يتم تاكيد دعمه في macOS 11(big sur) |

إذا كنت تريد طريقه انشاء الكونفق يدويا ولك معرفه باللغه الانجليزي [هنا ](https://dortania.github.io/OpenCore-Install-Guide/config-laptop.plist/ivy-bridge.html)رابط يشرح كيفيه انشاء الكونفق للجيل الثالث لللابتوبات

**هذه الصفحة معدة على اساس انك تستخدم كونفقات هاكنتوش بالعربي**

???+ Warning "تنبية"
	قد تكون الصور احيانا غير محدثة او لاتظهر التعديلات الصحيحه
	**يرجى دائما اتباع الكلام المكتوب وتجاهل الصور** وظيفتها هي توضيح الاقسام لا غير الا لبعض الاستثانئات

## DeviceProperties

### Add

![](/img/config-setup/3rd-gen/6-series-mobo.png)

???+ info "PciRoot(0x0)/Pci(0x16,0x0)"

	اذا كانت لديك مذربورد من الفئة السادسة(HM65,HM67) ستحتاج الى تغيير رقم جهاز ال IMEI حتى يكون مدعوم,
	قم باضافه الاتي تحت Add
	
	| Value | Type | Key |
	| :--- | :--- | :--- |
	| 3A1E0000 | Data | device-id |

![](/img/config-setup/deviceproperties.png)

???+ info "PciRoot(0x0)/Pci(0x2,0x0)"
	هذا القسم مخصص لتحديد باتشات ال Framebuffer لكيكست [WhateverGreen](/EFI-setup/gathering-kexts.md#gpus)

	| AAPL,ig-platform-id | وصف |
	| :--- | :--- |
	| 03006601 | يستخدم لشاشات بدقه 1366x768 او اقل |
	| 04006601 | يستخدم لشاشات بدقه 1600x900 او اكثر |
	| 09006601 | خيار ثالث في حاله عدم عمل الخيارات السابقه(اذا كانت تستخدم الشاشه `eDP`) |
	
	**ملاحظات:**
	
	- مداخل VGA لاتعمل ابدا اذا اشتغلت فهي بالحظ تقريبا.
	
	- اذا استخدمت خيار `04006601` فستحتاج اضافه خيارات جديده لتصليح مداخل الشاشه:

	| عنوان  | النوع | القيمة | ملاحظة |
	| :--- | :--- | :--- | :--- |
	| عنوان | TYPE | قيمه خاصه بك | ملاحظات |
	| framebuffer-patch-enable | Number | 1 | تفعيل باتشات |
	| framebuffer-memorycount | Number | 2 |  |
	| framebuffer-pipecount | Number | 2 |  |
	| framebuffer-portcount | Number | 4 | |
	| framebuffer-stolenmem | Data | 00000004 | وضع رامات الكرت 64 ميجا |
	| framebuffer-con1-enable | Number | 1 | سيسمح لنا بعمل باتشات(تعديلات) حتى نقوم بتشغل المداخل الخارجيه |
	| framebuffer-con1-alldata | Number | 4 | |
	| framebuffer-portcount | Data | 02050000 00040000 07040000 03040000 00040000 81000000 04060000 00040000 81000000 | تعريف المداخل |
	
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
