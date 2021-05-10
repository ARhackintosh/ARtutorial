---
description: شرح كيفيه انشاء كونفق اوبن كور لمعالجات انتل الجيل العاشر على المكتبي وكافه الخيارات الضروريه.
---

# الجيل العاشر
| الدعم | الاصدار |
| :--- | :--- |
| بداية الدعم على الماك | macOS 10.15, Catalina |

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

???+ note "Quirks"
	| العنوان | مفعل | وصف |
	| :--- | :--- | :--- |
	| DevirtualiseMmio | True | |
	| EnableWriteUnprotector | False | |
	| ProtectUefiServices | True | |
	| RebuildAppleMemoryMap | True | |
	| SetupVirtualMap | False|.|
	| SyncRuntimePermissions | True | |

## DeviceProperties

![](https://raw.githubusercontent.com/dortania/OpenCore-Install-Guide/master/images/config/config.plist/commetlake/DeviceProperties.png){: style="width:800px"; loading=lazy }

### Add

???+ note "PciRoot(0x0)/Pci(0x2,0x0)"
	هذا القسم مخصص لتحديد باتشات ال Framebuffer لكيكست [WhateverGreen](/EFI-setup/gathering-kexts#gpus)

	| AAPL,ig-platform-id | وصف |
	| :--- | :--- |
	| 07009B3E | يستخدم لكروت انتل المدمحة في حاله استخدامها لعرض الشاشة |
	| 00009B3E | خيار بديل في  حاله عدم عمل 07009B3E |
	| 0300C89B | يستخدم لكروت انتل المدمجه في حاله استخدامها لعمليات حسابيه فقط بدون عرض الشاشه |
	
	ايضا اذا كنت تستخدم**الكرت المدمج لعرض الشاشه** ستحتاج الى اضافه اعدادت اضافيه :

	| عنوان  | النوع | القيمة | ملاحظة |
	| :--- | :--- | :--- | :--- |
	| AAPL,ig-platform-id | Data | 07009B3E | |
	| framebuffer-patch-enable | Data | 01000000 | |
	| framebuffer-stolenmem | Data | 00003001 | |

	**مثال** للاعدادت في الكونفق
	
	![](/img/config-setup/deviceproperties-example.png)

???+ note "PciRoot(0x0)/Pci(0x1C,0x1)/Pci(0x0,0x0)"
	في حاله لديك كرت انتل **intel i225-V 2.5GBe** لل ethernet 
	سنقوم بتعديل اسم الكرت حتى يتم دعمه من النظام بشكل مباشر

	| عنوان | نوع | القيمة |
	| :--- | :--- | :--- |
	| device-id | Data | F2150000 |

	- **ملاحظة** : اذا توقف الاقلاع على كيكست i210 اضيف المدخلات تحت `PciRoot(0x0)/Pci(0x1C,0x4)/Pci(0x0,0x0)` بدلا عن `PciRoot(0x0)/Pci(0x1C,0x1)/Pci(0x0,0x0)`
	- **ملاحظة** : اذا المذربورد الخاص بك لا يحتوي على كرت i225 **لا تضيف هذه الاعدادات**

???+ note "PciRoot(0x0)/Pci(0x16,0x0)"
	`layout-id`

	- يقوم بتحديد كوداك الصوت الموجود في المذربورد.

	- لانحتاجه لانه سوف نقوم بتحديده في [nvram](#nvram) لاحقا
	لذلك بامكانك حذفه, لان لن يتم استخدامة

### Delete 
لا توجد تعديلات هنا, ابقي كل شيء كما هو

## Kernel

![kernel](https://raw.githubusercontent.com/dortania/OpenCore-Install-Guide/master/images/config/config-universal/kernel.png#zoom){: style="width:800px"}

### Add

قسم مخصص للكيكستات وترتيبها, لا تعدل شيء, لان عمليه [سنابشوت](/EFI-setup/config/#acpi) قامت باضافتها للكونفق

### Emulate

مخصص لتغيير نوع المعالج, لا نحتاجه

### Force

مخصص لكيكستات في انظمه الماك القديمه, لا نحتاجه

### Block 

منع بعض كيكستات النظام من العمل, لا نحتاجه

### Patch

???+ "Patch"
	 هذا باتش مخصص لدعم كرت شبكه I225-V 2.5GBe من انتل, وهو متواجد في مذربوردات الفئه العليه في الجيل العاشر, اذا جهاز لا يستخدم هذا الكرت لا تضيف هذا الباتش.

	| عنوان | نوع | قيمة |
	| :--- | :--- | :--- |
	| Base | String | __Z18e1000_set_mac_typeP8e1000_hw |
	| Comment | String | I225-V patch |
	| Enabled | Boolean | True |
	| Find | Data | `F2150000` |
	| Identifier | String | com.apple.driver.AppleIntelI210Ethernet |
	| MinKernel | String | 19.0.0 |
	| Replace | Data | `F3150000` |

	باقي العنواين اتركها بلا تعديل

### Quirks

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

![Misc](https://raw.githubusercontent.com/dortania/OpenCore-Install-Guide/master/images/config/config-universal/misc.png#zoom){: style="width:800px"}

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
	| SecureBootModel | `Default` | هذه كلمة, اكتبها مثل المكتوب بالظبط, **فيه حاله كنت تستخدم تعريفات انفيديا اكتب** `Disabled` |
	| Vault | `Optional` | هذه كلمة, اكتبها مثل المكتوب بالظبط |

### Tools
مستخدم لتشغيل ادوات حل المشاكل في الاوبن كور, [سنابشوت](/EFI-setup/config/#acpi)
 في propertree قام باضافتها لك

### Entries
لاتوجد تعديلات هنا

## NVRAM

![nvram](https://raw.githubusercontent.com/dortania/OpenCore-Install-Guide/master/images/config/config-universal/nvram.png#zoom){: style="width:800px"}

### Add

![](/img/config-setup/nvram-add.png)

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

### Delete

???+ note "Delete"
	اجبار اعاده كتابه المتغيرات داخل nvram

	| الخيار | مفعل |
	| :--- | :--- |
	| WriteFlash | True |


## PlatformInfo

![](/img/config-setup/propertree-platforminfo.png)

### Generic

???+ note "Generic"

	هنا نقوم بوضع معلومات الجهاز مثل نوعه و السيريال ورقم اللوحة وغيرها, سنستخدم برنامج [GenSMBios](https://github.com/corpnewt/GenSMBIOS)

	بعد تشغيل البرنامج اضغط رقم 1 لتنزيل الملفات الضرورية.

	بعدها اضغط رقم 3 لتوليد معلومات الجهاز

	بالنسبه للموديل الجهاز (SMBIOS) هناك خيارين للجيل العاشر:

	- `iMac20,1` i7-10700K او اقل

	- `iMac20,2` i9-10850k او اقوى

	![](/img/config-setup/gensmbios.png)

	يتم نقل الارقام بالشكل الاتي للكونفق:

	- `Type` يتم نسخه الى Generic -> SystemProductName.
	- `Serial` يتم نسخه الى  Generic -> SystemSerialNumber.
	- `Board Serial` يتم نسخه الى  Generic -> MLB.
	- `SmUUID` يتم نسخه الى  Generic -> Generic -> SystemUUID.

## UEFI

**ConnectDrivers**: True

تشغيل جميع تعريفات `.efi`

### Drivers
اضافه جميع التعريفات (ملفات EFI),
تم اضافتها مسبقا بواسطه [سنابشوت](/EFI-setup/config/#acpi)
propertree 

### APFS
اعدادت مخصصه لتعريف APFS

لا توجد تعديلات هنا, ابقي كل شيء كما هو

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

???+ note "اذا كان لديك جهاز HP"
	يجب عليك تفعيل UnblockFsConnect
	
	| العنوان | مفعل | وصف |
	| :--- | :--- | :--- |
	| UnblockFsConnect | True | ضروري لمذربوردات HP |


