# Ryzen جميع الاجيال
| الدعم | الاصدار |
| :--- | :--- |
| بداية الدعم على الماك | macOS 10.13, High Sierra |


???+ Warning "تنبية"
	قد تكون الصور احيانا غير محدثة او لاتظهر التعديلات الصحيحه
	**يرجى دائما اتباع الكلام المكتوب وتجاهل الصور** وظيفتها هي توضيح الاقسام لا غير الا لبعض الاستثانئات

تاكد من الحصول على ملف [Sample.plist من داخل الاوبن كور](/EFI-setup/config/#_3)

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
	اعدادات مخصصه لباتشات Boot.efi و تصليحات الفريموير.
	
	| العنوان | مفعل | وصف |
	| :--- | :--- | :--- |
	| DevirtualizeMmio | False | مذربوردات TRx40 تحتاج لهذا الخيار |
	| EnableWriteUnprotector | False | |
	| RebuildAppleMemoryMap | True | |
	| SetupVirtualMap | True | مذربوردات **B550,A520,TRx4**0 **يجب ان تعطل هذا الخيار**, ايضا مذربوردات **B450,X470,X570** **مع بايوس محدث(اخر 2020**).  |
	| SyncRuntimePermissions | True | |


## DeviceProperties

### Add

هذا القسم مخصص لتعريف الكروت المدمجه في معالجات انتل(`PciRoot(0x0)/Pci(0x2,0x0)`).وكروت الصوت (`PciRoot(0x0)/Pci(0x1b,0x0)`)

كروت الصوت سنقوم بتعريفها بستخدام bootargs

لذلك قم بحذف جميع خيارات PciRoot.

### Delete 
لا توجد تعديلات هنا, ابقي كل شيء كما هو

## Kernel

![kernel](https://raw.githubusercontent.com/dortania/OpenCore-Install-Guide/master/images/config/AMD/kernel.png#zoom){: style="width:800px"; loading=lazy }

### Add

قسم مخصص للكيكستات وترتيبها, لا تعدل شيء, لان عمليه [سنابشوت](/EFI-setup/config/#acpi) قامت باضافتها للكونفق

### Emulate

???+ note "Emulate"
	| العنوان | مفعل | وصف |
	| :--- | :--- | :--- |
	| DummyPowerManagement | True | يقوم بتعطيل التحكم بطاقه المعالج من النظام على المعالجات الغير مدعومه مثل AMD |

### Force

مخصص لكيكستات في انظمه الماك القديمه, لا نحتاجه

### Block 

منع بعض كيكستات النظام من العمل, لا نحتاجه

### Patch 

هنا نقوم باضافه الباتشات المخصصه لمعالجات AMD, هذه الباتشات مطوره من فريق AMDOSX لهم الشكر, بحيث بدونهم لن يكون الهاكنتوش الخام ممكن على معالجات AMD

قم بتنزيل الباتشات من [هنا](https://github.com/AMD-OSX/AMD_Vanilla) (تنزيل عبر زر code) ثم داخل ملف 17h ستجد ملف patches.plist قم بفتحه ببرنامج propoer tree, ثم ضع بجانبه نافذه الكونفق الخاص بك, ثم قم بعمليه النسخ مثل الصورة:

![باتشات amd](/img/config-setup/amd/amd-patches.gif)

### Quirks

???+ note "Quirks"
	اعدادات مخصصه للكيرنل.
	
	| العنوان | مفعل |
	| :--- | :--- |
	| PanicNoKextDump | True |
	| PowerTimeoutKernelPanic | True |
	| XhciPortLimit | True |

### Scheme

مخصص لانظمه الماك القديمه, لانحتاجه.

## Misc

![Misc](https://raw.githubusercontent.com/dortania/OpenCore-Install-Guide/master/images/config/config-universal/misc.png#zoom){: style="width:800px"; loading=lazy }

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

![nvram](https://raw.githubusercontent.com/dortania/OpenCore-Install-Guide/master/images/config/config-universal/nvram.png#zoom){: style="width:800px"; loading=lazy }

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
	| **npci=0x2000** | يقوم بايقاف تحليل اعطال في قطع ال PCI, ويحل مشكله توقف عند `PCI Start Configuration` خيار اخر هو `npci= 0x3000`. **غير ضروري في حاله تفعيل Above4GDecoding في البايوس** |

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

![](https://raw.githubusercontent.com/dortania/OpenCore-Install-Guide/master/images/config/config-universal/iMacPro-smbios.png#zoom){: style="width:800px"; loading=lazy }

### Generic

???+ note "Generic"
	هنا نقوم بوضع معلومات الجهاز مثل نوعه و السيريال ورقم اللوحة وغيرها, سنستخدم برنامج [GenSMBios](https://github.com/corpnewt/GenSMBIOS)

	بعد تشغيل البرنامج اضغط رقم 1 لتنزيل الملفات الضرورية.

	بعدها اضغط رقم 3 لتوليد معلومات الجهاز

	بالنسبه للموديل الجهاز (SMBIOS) هناك خيارين للجيل الثامن:

	- `iMacPro1,1` مع كروت AMD RX 4xx+ ==Polaris== او احدث

	- `MacPro7,11` مع كروت AMD RX 4xx+ ==Polaris== او احدث

	- `MacPro6,1` مع كروت AMD R5/R7/R9 او اقدم

	- `iMac14,2` كروت انفيديا  6xx او احدث (**لايدعم بيج سر macOS 11 Big Sur**)

	```bash
	#######################################################
	#              iMacPro1,1 SMBIOS Info                 #
	#######################################################

	Type:         iMacPro1,1
	Serial:       C02T32ZNHX87
	Board Serial: C02702303GUJG36UE
	SmUUID:       E12CAE4E-7898-4EE0-81C8-DB9EC9E488E3
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
	| UnblockFsConnect | False | ضروري لمذربوردات HP |

