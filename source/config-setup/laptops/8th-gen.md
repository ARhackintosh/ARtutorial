---
description: شرح كيفيه انشاء كونفق اوبن كور لمعالجات انتل الجيل الثامن على الابتوبات وكافه الخيارات الضروريه.
---

# الجيل الثامن laptops
| الدعم | الاصدار |
| :--- | :--- |
| [Coffee lake](https://en.wikipedia.org/wiki/Coffee_Lake) بداية الدعم على الماك | macOS 10.13, High Sierra |
| [Whisky lake](hhttps://en.wikipedia.org/wiki/Whiskey_Lake_(microprocessor)) بداية الدعم على الماك | macOS 10.14.1, Mojave |

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

???+ note "Patch"
	ضروري لتوجيه كل الاوامر المهمه ل [SSDT-XOSI](/EFI-setup/ACPI/#ssdt-xosiaml)

	| العنوان | النوع | القيمة |
	| :--- | :--- | :--- |
	| Comment | String | Change _OSI to XOSI |
	| Enabled | Boolean | YES |
	| Count | Number | 0 |
	| Limit | Number | 0 |
	| Find | Data | 5f4f5349 |
	| Replace | Data | 584f5349 |

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

### Quirks

قسم مخصص للاعدادت خاصه ب ACPI, لا توجد تعديلات هنا, ابقي كل شيء كما هو

## DeviceProperties

![](https://raw.githubusercontent.com/dortania/OpenCore-Install-Guide/master/images/config/config-laptop.plist/coffeelake/DeviceProperties.png#zoom){: style="width:800px"; loading=lazy }

### Add

???+ note "PciRoot(0x0)/Pci(0x2,0x0)"
	هذا القسم مخصص لتحديد باتشات ال Framebuffer لكيكست [WhateverGreen](/EFI-setup/gathering-kexts#gpus)

	| AAPL,ig-platform-id | وصف |
	| :--- | :--- |
	| 0900A53E | يستخدم مع UHD630 |
	| 00001E19 | يستخدم مع UHD620 |

	في حاله عدم وجود طريقه لتحديد حجم رامات الكرت ==DVMT== في البايوس, قد تواجه كيرنل بانك في الاقلاع, ينصح باضافه الاتي:

	| عنوان  | TYPE | القيمة | ملاحظة |
	| :--- | :--- | :--- | :--- |
	| framebuffer-patch-enable | Data | 01000000 | تفعيل باتشات |
	| framebuffer-stolenmem | Data | 00003001 |  |
	| framebuffer-fbmem | Data | 00009000 |  |
	
	اذا كان لديك كرت **UHD620** على معالج [Coffee lake](https://en.wikipedia.org/wiki/Coffee_Lake  تحتاج الى اضافه:

	| عنوان  | النوع | القيمة | ملاحظة |
	| :--- | :--- | :--- | :--- |
	| device | Data | 9B3E0000 | تغيير اسم الكرت حتى يتم دعمه |

???+ note "PciRoot(0x0)/Pci(0x16,0x0)"
	`layout-id`

	- يقوم بتحديد كوداك الصوت الموجود في المذربورد.

	- لانحتاجه لانه سوف نقوم بتحديده في [nvram](#nvram) لاحقا
	لذلك بامكانك حذفه, لان لن يتم استخدامة

### Delete 
لا توجد تعديلات هنا, ابقي كل شيء كما هو

## Kernel

![kernel](https://raw.githubusercontent.com/dortania/OpenCore-Install-Guide/master/images/config/config-universal/kernel.png#zoom){: style="width:800px"; loading=lazy }

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

### Add

![nvram](https://raw.githubusercontent.com/dortania/OpenCore-Install-Guide/master/images/config/config-universal/nvram.png#zoom){: style="width:800px"; loading=lazy }

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
	| **-wegnoegpu** | يستخدم لتعطيل جميع الكروت الخارجيه, مفيد بحاله اذا كان كرتك المنفصل غير مدعوم من النظام مثل كروت انفيديا الحديثة. **تمت اضافته سابقا**|

	- **csr-active-config**: `00000000`

	اعداد مخصص ل SIP('System Integrity Protection') 
	خيار  `00000000` سوف يقوم بتفعيله ويفضل ابقائه كما هو لانه افضل لامان النظام

	- **run-efi-updater**: `No`

	مخصص لتعطيل تحديثات فريومير اجهزه ماك, لان جهازك ليس ماك حقيقي

	- **prev-lang:kbd**: <>

	مخصص لتحديد لغه الكيبورد 
	ابقه فارغ او حددها من هذه [القائمة](https://github.com/acidanthera/OpenCorePkg/blob/master/Utilities/AppleKeyboardLayouts/AppleKeyboardLayouts.txt)

### Delete

**مخصص فقط للاجهزه التي لاتعمل فيها ال  ==NVRAM==**

- LegacyEnable: TRUE
	- يقوم بتخزين اعدادت ال nvram في ملف nvram.plist لمحاكاه دعم nvram
- LegacyOverwrite: TRUE
	- يسمح بتفعيل الاعدادات الموجوده في nvram.plist

???+ note "Delete"
	اجبار اعاده كتابه المتغيرات داخل nvram

	| الخيار | مفعل |
	| :--- | :--- |
	| WriteFlash | True |

## PlatformInfo

![](https://raw.githubusercontent.com/dortania/OpenCore-Install-Guide/master/images/config/config-laptop.plist/coffeelake/smbios.png#zoom){: style="width:800px"; loading=lazy }

### Generic

???+ note "Generic"
	هنا نقوم بوضع معلومات الجهاز مثل نوعه و السيريال ورقم اللوحة وغيرها, سنستخدم برنامج [GenSMBios](https://github.com/corpnewt/GenSMBIOS)

	بعد تشغيل البرنامج اضغط رقم 1 لتنزيل الملفات الضرورية.

	بعدها اضغط رقم 3 لتوليد معلومات الجهاز

	بالنسبه للموديل الجهاز (SMBIOS) هناك عده اختيارات للجيل الثامن على الابتوبات:
	igpu = كرت شاشه مدمج dgpu = كرت منفصل

	| SMBIOS | نوع المعالج | نوع كرت الشاشة | حجم الشاشة |
	| :--- | :--- | :--- | :--- |
	| MacBookPro15,1 | سداسي النواه 45w | iGPU: UHD 630 + dGPU: RP555/560X | 15" | Yes |
	| MacBookPro15,2 | رباعي النواه 15w | iGPU: Iris 655 | 13" | Yes |
	| MacBookPro15,3 | سداسي النواه 45w | iGPU: UHD 630 + dGPU: Vega16/20 | 15" | Yes |
	| MacBookPro15,4 | رباعي النواه 15w | iGPU: Iris 645 | 13" | Yes |

	```bash
	#######################################################
	#            MacBookPro15,4 SMBIOS Info               #
	#######################################################

	Type:         MacBookPro15,4
	Serial:       FVFDMAY9L40Y
	Board Serial: FVF044700GU0000FB
	SmUUID:       3B68C9DD-9C07-4ADA-97E2-BBDF4E6B23AF
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

???+ note "Quirks"
	
	| العنوان | مفعل | وصف |
	| :--- | :--- | :--- |
	| ReleaseUsbOwnership | YES | |
	| UnblockFsConnect | False | ضروري لمذربوردات HP |

