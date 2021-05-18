---
description: شرح كيفيه انشاء كونفق اوبن كور لمعالجات انتل الجيل الثالث على الابتوبات وكافه الخيارات الضروريه.
---

# جيل ثالث laptop
| الدعم | الاصدار |
| :--- | :--- |
| بداية الدعم على الماك | OS X 10.7, Lion |

???+ Warning "تنبية"
	قد تكون الصور احيانا غير محدثة او لاتظهر التعديلات الصحيحه
	**يرجى دائما اتباع الكلام المكتوب وتجاهل الصور** وظيفتها هي توضيح الاقسام لا غير الا لبعض الاستثانئات

## ACPI

![ACPI](https://raw.githubusercontent.com/dortania/OpenCore-Install-Guide/master/images/config/config-laptop.plist/ivy-bridge/acpi.png#zoom){: style="width:800px"; loading=lazy }

### Add

هذا القسم مخصص لملفات SSDT/ACPI,
كامل التفاصيل حول الملفات المطلوبه لكل جيل وطريقه عملها موجود في صفحه [ACPI](/EFI-setup/ACPI)
بعد الاضافه تاكد من عمل [سنابشوت](/EFI-setup/config/#acpi)

### Delete


???+ note "Delete"
	هنا نحدد قسم معين من خريطه الجهاز (acpi) من اظهاره للنظام
	وهذا مهم لان نظام الماك لا يدعم تحكم بطاقه معالجات الجيل الثالث بشكل جيد وقد يسبب مشاكل
	الحل لهذه المشكله هو عمل ملف [SSDT-PM](/EFI-setup/ACPI#ssdt-pmaml) بعد تثبيت النظام

	لذلك هذه التعديلات مؤقته حتى يتم تثبيت النظام
	بعد تثبيت قم بعمل ملف [SSDT-PM](/EFI-setup/ACPI#ssdt-pmaml) و عطلها

	حذف Cpupm

	| العنوان | النوع | القيمة |
	| :--- | :--- | :--- |
	| All | Boolean | True |
	| Comment | String | Delete CpuPm |
	| Enabled | Boolean | True |
	| OemTableId | Data | 437075506d000000 |
	| TableLength | Number | 0 |
	| TableSignature | Data | 53534454 |

	حذف Cpu0Ist

	| العنوان | النوع | القيمة |
	| :--- | :--- | :--- |
	| All | Boolean | YES |
	| Comment | String | Delete Cpu0Ist |
	| Enabled | Boolean | YES |
	| OemTableId | Data | 4370753049737400 |
	| TableLength | Number | 0 |
	| TableSignature | Data | 53534454 |

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

## DeviceProperties

![DeviceProperties](https://raw.githubusercontent.com/dortania/OpenCore-Install-Guide/master/images/config/config-laptop.plist/ivy-bridge/DeviceProperties.png#zoom){: style="width:800px"; loading=lazy }

### Add

???+ note "PciRoot(0x0)/Pci(0x2,0x0)"

	هذا القسم مخصص لتحديد باتشات ال Framebuffer لكيكست [WhateverGreen](/EFI-setup/gathering-kexts#gpus)

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
	| framebuffer-patch-enable | Number | 1 | تفعيل باتشات |
	| framebuffer-memorycount | Number | 2 |  |
	| framebuffer-pipecount | Number | 2 |  |
	| framebuffer-portcount | Number | 4 | |
	| framebuffer-stolenmem | Data | 00000004 | وضع رامات الكرت 64 ميجا |
	| framebuffer-con1-enable | Number | 1 | سيسمح لنا بعمل باتشات(تعديلات) حتى نقوم بتشغل المداخل الخارجيه |
	| framebuffer-con1-alldata | Data | 2050000 00040000 07040000 03040000 00040000 81000000 04060000 00040000 81000000 | تعريف المداخل |

???+ note "PciRoot(0x0)/Pci(0x16,0x0)"

	اذا كانت لديك مذربورد من الفئة السادسة(HM65,HM67) ستحتاج الى تغيير رقم جهاز ال IMEI حتى يكون مدعوم,
	قم باضافه الاتي تحت Add
	
	| القيمة | النوع | العنوان |
	| :--- | :--- | :--- |
	| 3A1E0000 | Data | device-id |


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
	| AppleCpuPmCfgLock | True | غير ضروري اذا تم تعطيل `CFG-Lock` في البايوس |
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

![nvram](https://raw.githubusercontent.com/dortania/OpenCore-Install-Guide/master/images/config/config-universal/nvram.png#zoom){: style="width:800px"; loading=lazy }

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

![](https://raw.githubusercontent.com/dortania/OpenCore-Install-Guide/master/images/config/config-laptop.plist/ivy-bridge/smbios.png#zoom){: style="width:800px"; loading=lazy }

### Generic

???+ note "Generic"
	هنا نقوم بوضع معلومات الجهاز مثل نوعه و السيريال ورقم اللوحة وغيرها, سنستخدم برنامج [GenSMBios](https://github.com/corpnewt/GenSMBIOS)

	بعد تشغيل البرنامج اضغط رقم 1 لتنزيل الملفات الضرورية.

	بعدها اضغط رقم 3 لتوليد معلومات الجهاز

	بالنسبه للموديل الجهاز (SMBIOS) هناك عده اختيارات للجيل الثالث على الابتوبات:
	igpu = كرت شاشه مدمج dgpu = كرت منفصل

	??? note "كاتلينا او اقدم  (macOS Catalina 10.15)"
		| SMBIOS | نوع المعالج | نوع كرت الشاشة | حجم الشاشة |
		| :--- | :--- | :--- | :--- |
		| MacBookAir5,1 | ثنائي النواه 17w | iGPU: HD 4000 | 11" |
		| MacBookAir5,2 | ثنائي النواه 17w | iGPU: HD 4000 | 13" |
		| MacBookPro10,1 | رباعي النواه 45w | iGPU: HD 4000 + dGPU: GT650M | 15" |
		| MacBookPro10,2 | ثنائي النواه 35w(فئه عليا) | iGPU: HD 4000 | 13" |

	???+ note "بيج سر (macOS Big Sur 11)"
		| SMBIOS | نوع المعالج | حجم الشاشة |
		| :--- | :--- | :--- |
		| MacBookAir6,1 | ثنائي النواه 15w | 11" |
		| MacBookAir6,2 | ثنائي النواه 15w | 13" |
		| MacBookPro11,1 | ثنائي النواه 28w | 13" |
		| MacBookPro11,2 | رباعي النواه 45w | 15" |
		| MacBookPro11,3 | رباعي النواه 45w | 15" |
		| MacBookPro11,4 | رباعي النواه 45w | 15" |
		| MacBookPro11,5 | رباعي النواه 45w | 15" |

	```bash
	#######################################################
	#            MacBookPro11,5 SMBIOS Info               #
	#######################################################

	Type:         MacBookPro11,5
	Serial:       C02WKSZWG85Y
	Board Serial: C02815401GUGF2CFB
	SmUUID:       B628FD80-9D26-4CA1-A846-5D074E6D5C07
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
	| IgnoreInvalidFlexRatio | True | |
	| ReleaseUsbOwnership | YES | |
	| UnblockFsConnect | False | ضروري لمذربوردات HP |
