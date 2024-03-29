---
description: شرح كيفيه انشاء كونفق اوبن كور لمعالجات انتل الجيل الرابع والخامس على المكتبي وكافه الخيارات الضروريه.
comments: true
---

# الجيل الرابع والخامس PC
| الدعم | الاصدار |
| :--- | :--- |
| بداية الدعم على الماك | OS X 10.8, Mountain Lion |

???+ Warning "تنبية"
	قد تكون الصور احيانا غير محدثة او لاتظهر التعديلات الصحيحه
	**يرجى دائما اتباع الكلام المكتوب وتجاهل الصور** وظيفتها هي توضيح الاقسام لا غير الا لبعض الاستثانئات

## ACPI

### Add

هذا القسم مخصص لملفات SSDT/ACPI,
كامل التفاصيل حول الملفات المطلوبه لكل جيل وطريقه عملها موجود في صفحه [ACPI](/EFI-setup/ACPI)
بعد الاضافه تاكد من عمل [سنابشوت](/EFI-setup/config/#acpi)

### Delete

لا توجد تعديلات هنا, ابقي كل شيء كما هو , قسم مخصص لمنع اجزاء معينه من ACPI من ظهورها للنظام

### Patch

هذا القسم مخصص لعمل باتشات مباشره اثناء الاقلاع
لكن نحن لا نحتاجه, لان جميع التعديلات موجوده في ملفات ال SSDT/ACPI

وهذه الطريقه تسمح باقلاع انظمه اخرى مثل لينكس او ويندوز من اوبن كور بدون مشاكل

### Quirks

قسم مخصص للاعدادت خاصه ب ACPI, لا توجد تعديلات هنا, ابقي كل شيء كما هو

## Booter

قسم مخصص لعمل باتشات boot.efi مع OpenRuntime
لاتوجد تعديلات هنا

### MmioWhitelist

قسم مخصص لتحديد مساحات معينه لاظهارها للنظام, مهم عند استخدامه مع `DevirtualiseMmio`
لاتوجد تعديلات هنا

### Quirks

اعدادت مخصصه ل Boot.efi
لاتوجد تعديلات هنا

## DeviceProperties

![](https://dortania-mirror.tutorial.هاكنتوش.com/images/config/config.plist/haswell/DeviceProperties.png){: style="width:800px"; loading=lazy }

### Add

???+ note "PciRoot(0x0)/Pci(0x2,0x0)"
	هذا القسم مخصص لتحديد باتشات ال Framebuffer لكيكست [WhateverGreen](/EFI-setup/gathering-kexts#gpus)

	| AAPL,ig-platform-id | وصف |
	| :--- | :--- |
	| 0300220D | يستخدم لكروت انتل المدمجه في الجيل الرابع على ال PC في حاله استخدامها لعرض الشاشة |
	| 04001204 | يستخدم لكروت انتل المدمجه في الجيل الرابع على ال PC في حاله استخدامها لعمليات حسابيه فقط بدون عرض الشاشه |
	| 07002216 | يستخدم لكروت انتل المدمجة الخاصه بالجيل الخامس على ال PC |
	
	اذا كان لديك كرت HD 4400 فهو غير مدعوم من الماك بشكل رسمي لذلك ستحتاج تغيير اسمه, اضف الاتي للكونفق تحت `PciRoot(0x0)/Pci(0x2,0x0)` :
	
	| عنوان | نوع | القيمة |
	| :--- | :--- | :--- |
	| device-id | Data | 12040000 |
	
	ايضا اذا كنت تستخدم **الكرت المدمج لعرض الشاشه** ستحتاج الى اضافه اعدادت اضافيه :

	| عنوان  | النوع | القيمة | ملاحظة |
	| :--- | :--- | :--- | :--- |
	| AAPL,ig-platform-id | Data | قيمة الكرت الخاص بك | |
	| framebuffer-patch-enable | Data | 01000000 | |
	| framebuffer-stolenmem | Data | 00003001 | |
	| framebuffer-fbmem | Data | 00009000 | اذا لا يوجد خيار تحديد رام الكرت في البايوس |
	| device-id | Data | 12040000 |ضروري فقط ل HD4400 |
	
	**مثال** كرت HD4400 بدون وجود خيار للتحكم بحجم الرام في البايوس:
	
	![](/img/config-setup/4th-gen/HD4400-example.png)

???+ note "PciRoot(0x0)/Pci(0x16,0x0)"
	`layout-id`

	- يقوم بتحديد كوداك الصوت الموجود في المذربورد.

	- لانحتاجه لانه سوف نقوم بتحديده في [nvram](#nvram) لاحقا
	لذلك بامكانك حذفه, لان لن يتم استخدامة

### Delete 
لا توجد تعديلات هنا, ابقي كل شيء كما هو

## Kernel

![kernel](https://dortania-mirror.tutorial.هاكنتوش.com/images/config/config-universal/kernel-modern-XCPM.png){: style="width:800px"; loading=lazy }

### Add

قسم مخصص للكيكستات وترتيبها, لا تعدل شيء, لان عمليه [سنابشوت](/EFI-setup/config/#acpi) قامت باضافتها للكونفق

### Emulate

مخصص لتغيير نوع المعالج, لا نحتاجه

### Force

مخصص لكيكستات في انظمه الماك القديمه, لا نحتاجه

### Block 

منع بعض كيكستات النظام من العمل, لا نحتاجه

### Patch

مخصص لعمل باتشات للكيرنل و الكيكستات
لا نحتاجه حاليا

### Quirks

![](/img/config-setup/kernel-quirks.png)

???+ note "Quirks"
	اعدادات مخصصه للكيرنل.
	
	| العنوان | مفعل | وصف |
	| :--- | :--- | :--- |
	| AppleXcpmCfgLock | True | غير ضروري اذا تم تعطيل `CFG-Lock` في البايوس |
	| DisableIOMapper | True | غير ضروري اذا تم تعطيل `VT-D` في البايوس |
	| LapicKernelPanic | False | اجهزه HP ستحتاج تفعيل هذا الاعداد |
	| PanicNoKextDump | True | |
	| PowerTimeoutKernelPanic | True | |
	| XhciPortLimit | false | يفعل فقط في حاله استخدام ماك اقدم من اصدار macOS Big Sur 11.3 |

### Scheme

مخصص لانظمه الماك القديمه, لانحتاجه.

## Misc

![Misc](https://dortania-mirror.tutorial.هاكنتوش.com/images/config/config-universal/misc.png){: style="width:800px"; loading=lazy }

### Boot
اعدادت مخصصه لشاشه الاقلاع, لاتوجد تعديلات هنا

### Debug

???+ note "Debug"
	قسم مخصص للاظهار سجل عمليه الاقلاع في الاوبن كور والنظام
	سنعدل كل شيء الا `DisplayDelay`

	| الخيار | مفعل |
	| :--- | :--- |
	| AppleDebug | True |
	| ApplePanic | True |
	| DisableWatchDog | True |
	| Target | 67 |

### Security

???+ note "Debug"
	خيارات الامان

	| الخيار | مفعل | ملاحظة|
	| :--- | :--- | :--- |
	| AllowNvramReset | True | |
	| AllowSetDefault | True | |
	| BlacklistAppleUpdate | True | |
	| ScanPolicy | 0 | |
	| SecureBootModel | `Disabled` | هذه كلمة, اكتبها مثل المكتوب بالظبط |
	| Vault | `Optional` | هذه كلمة, اكتبها مثل المكتوب بالظبط |

### Tools
مستخدم لتشغيل ادوات حل المشاكل في الاوبن كور, [سنابشوت](/EFI-setup/config/#acpi)
 في propertree قام باضافتها لك

### Entries
لاتوجد تعديلات هنا

## NVRAM

![nvram](https://dortania-mirror.tutorial.هاكنتوش.com/images/config/config-universal/nvram.png){: style="width:800px"; loading=lazy }

### Add

???+ note "7C436110-AB2A-4BBB-A880-FE41995C9F82"

	هنا نقوم باضافه شروط اقلاع اضافيه مثلا لتحديد كروت الصوت وغيرها.
	 **اوامر اقلاع عامة:**

	| اوامر اقلاع  | وصف |
	| :--- | :--- |
	| **-v** |هذا احد اهم اوامر الاقلاع في عالم الهاكنتوش, يقوم بتفعيل وضع تفصيل حاله الاقلاع لاظهار جميع العمليات التي يقوم بها النظام. بدونه لايمكن معرفة سبب بانك بشكل صحيح فهو يظهر  معلومات مثلا حالة الاجهزه ايت مرحلة اقلاع فيها الجهاز وغيرها   |
	| **debug=0x100** | يقوم بتعطيل اعاده التشغيل في حالة حصول بانك في الاقلاع, لاعطائك فرصة لقرائة سبب توقف النظام **يستحسن استخدامة اثناء التثبيت وحل المشاكل** |
	| **keepsyms=1** | مرافق ل debug=0x100 بحيث يخبر النظام بطباعة علامات عند حصول بانك لاعطاء معلومات اكثر عن سبب حصول البانك بالاساس. |
	| **alcid=XX** | يستخدم لتحديد نوع كروت الصوت لتعريف [AppleALC.kext](/EFI-setup/gathering-kexts#sound) قائمة الكروت الصوت والرقم الخاص بها [من هنا](https://github.com/acidanthera/applealc/wiki/supported-codecs) **استخدم الارقام بعد كلمت layout** |

	* **اوامر اقلاع لكروت الشاشة**:

	| اوامر اقلاع | وصف |
	| :--- | :--- |
	| **agdpmod=pikera** | يستخدم لتعطيل board id على كروت navi(RX 5xxx) بدونه ستواجهه شاشة سوداء, لاتستخدمة على كروت من نوع اخر. |
	| **nvda_drv_vrl=1** | ضروري لتفعيل تعريفات انفيديا على فئة GTX 9xx و 10xx على سييرا وهاي سييرا |
	| **-wegnoegpu** | يستخدم لتعطيل جميع الكروت الخارجيه, مفيد بحاله اذا كان كرتك المنفصل غير مدعوم من النظام مثل كروت انفيديا الحديثة. |

	- **csr-active-config**: `00000000`

	اعداد مخصص ل SIP('System Integrity Protection') 
	خيار  `00000000` سوف يقوم بتفعيله ويفضل ابقائه كما هو لانه افضل لامان النظام

	- **run-efi-updater**: `No`

	مخصص لتعطيل تحديثات فريومير اجهزه ماك, لان جهازك ليس ماك حقيقي

	- **prev-lang:kbd**: <>

	مخصص لتحديد لغه الكيبورد 
	ابقه فارغ او حددها من هذه [القائمة](https://github.com/acidanthera/OpenCorePkg/blob/master/Utilities/AppleKeyboardLayouts/AppleKeyboardLayouts.txt)

### Delete

???+ note "Delete"
	اجبار اعاده كتابه المتغيرات داخل nvram

	| الخيار | مفعل |
	| :--- | :--- |
	| WriteFlash | True |

## PlatformInfo

![](https://dortania-mirror.tutorial.هاكنتوش.com/images/config/config.plist/haswell/smbios.png){: style="width:800px"; loading=lazy }

### Generic

???+ note "Generic"
	هنا نقوم بوضع معلومات الجهاز مثل نوعه و السيريال ورقم اللوحة وغيرها, سنستخدم برنامج [GenSMBios](https://github.com/corpnewt/GenSMBIOS)

	بعد تشغيل البرنامج اضغط رقم 1 لتنزيل الملفات الضرورية.

	بعدها اضغط رقم 3 لتوليد معلومات الجهاز

	بالنسبه للموديل الجهاز (SMBIOS) هناك عده اختيارات للجيل الرابع:

	- `iMac14,4` اذا كنت ستسخدم الكرت مدمج فقط

	- `iMac15,1` اذا كنت ستسخدم كرت منفصل

	اما للجيل الخامس:

	- `iMac16,2` 

	```bash
	#######################################################
	#                iMac16,2 SMBIOS Info                 #
	#######################################################

	Type:         iMac16,2
	Serial:       C02TPRYMGG7G
	Board Serial: C02719108GUGQRYCB
	SmUUID:       A5E04F5A-71EC-4307-8B13-37416EF97C09
	```
	يتم نقل الارقام بالشكل الاتي للكونفق:

	- `Type` يتم نسخه الى Generic -> SystemProductName.
	- `Serial` يتم نسخه الى  Generic -> SystemSerialNumber.
	- `Board Serial` يتم نسخه الى  Generic -> MLB.
	- `SmUUID` يتم نسخه الى  Generic -> Generic -> SystemUUID.

## UEFI

**ConnectDrivers**: True

تشغيل جميع ملفات الفريموير `.efi`

### Drivers
اضافه جميع ملفات الفريموير (EFI),
تم اضافتها مسبقا بواسطه [سنابشوت](/EFI-setup/config/#acpi)
propertree 

### APFS
**هذه التعديلات فقط ضروريه اذا كنت تستخدم اي اصدار اقدم من Big Sur**

| الخيار | القيمة | الملاحظة |
| :--- | :--- | :--- |
| MinDate | `-1` | غير ضروري اذا تستخدم macOS 11 Big sur او احدث |
| MinVersion | `-1` | غير ضروري اذا تستخدم macOS 11 Big sur او احدث  |

### Audio
مخصص لاعدادات AudioDXE (غير متعلق بدعم  كرت الصوت في الماك)

لا توجد تعديلات هنا, ابقي كل شيء كما هو

### Input

مخصص لاعدادت الماوس والكيبورد

لا توجد تعديلات هنا, ابقي كل شيء كما هو

### Output
اعدادات مظهر اوبن كور

لا توجد تعديلات هنا, ابقي كل شيء كما هو

### ProtocolOverrides

مهم للانظمه الوهميه فقط

لا توجد تعديلات هنا, ابقي كل شيء كما هو

### Quirks

???+ note "Quirks"

	| العنوان | مفعل | وصف |
	| :--- | :--- | :--- |
	| IgnoreInvalidFlexRatio | True | |
	| UnblockFsConnect | False | ضروري لمذربوردات HP |
