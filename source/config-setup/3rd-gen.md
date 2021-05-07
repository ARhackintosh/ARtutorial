---
description: شرح كيفيه انشاء كونفق اوبن كور لمعالجات انتل الجيل الثالث على المكتبي وكافه الخيارات الضروريه.
---

# الجيل الثالث PC
| الدعم | الاصدار |
| :--- | :--- |
| بداية الدعم على الماك | OS X 10.7, Lion |

???+ Warning "تنبية"
	قد تكون الصور احيانا غير محدثة او لاتظهر التعديلات الصحيحه
	**يرجى دائما اتباع الكلام المكتوب وتجاهل الصور** وظيفتها هي توضيح الاقسام لا غير الا لبعض الاستثانئات

## ACPI

![ACPI](/img/config-setup/3rd-gen/ACPI.png)

### Add

هذا القسم مخصص لملفات SSDT/ACPI,
كامل التفاصيل حول الملفات المطلوبه لكل جيل وطريقه عملها موجود في صفحه [ACPI](/EFI-setup/ACPI)
بعد الاضافه تاكد من عمل [سنابشوت](/EFI-setup/config/#acpi)

### Delete


???+ note "التعديلات"
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

### Add

![](/img/config-setup/3rd-gen/deviceprop.png)

???+ note "PciRoot(0x0)/Pci(0x2,0x0)"
	هذا القسم مخصص لتحديد باتشات ال Framebuffer لكيكست [WhateverGreen](/EFI-setup/gathering-kexts#gpus)

	| AAPL,ig-platform-id | وصف |
	| :--- | :--- |
	| 0A006601 | يستخدم لكروت انتل المدمجه في حاله استخدامها لعرض الشاشة |
	| 07006201 | يستخدم لكروت انتل المدمجه في حاله استخدامها لعمليات حسابيه فقط بدون عرض الشاشه |


???+ note "PciRoot(0x0)/Pci(0x16,0x0)"
	اذا كانت لديك مذربورد من الفئة السادسة(H61, B65, Q65, P67, H67, Q67, Z68) ستحتاج الى تغيير رقم جهاز ال IMEI حتى يكون مدعوم,
	قم باضافه الاتي تحت Add
	
	| Value | Type | Key |
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
	| XhciPortLimit | True | |

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

### Add

![](/img/config-setup/nvram.png)

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

![](/img/config-setup/propertree-platforminfo.png)

هنا نقوم بوضع معلومات الجهاز مثل نوعه و السيريال ورقم اللوحة وغيرها, سنستخدم برنامج [GenSMBios](https://github.com/corpnewt/GenSMBIOS)

بعد تشغيل البرنامج اضغط رقم 1 لتنزيل الملفات الضرورية.

بعدها اضغط رقم 3 لتوليد معلومات الجهاز

بالنسبه للموديل الجهاز (SMBIOS) هناك اختيارين للجيل الثالث:

- `iMac13,1` هذا يستخدم للاجهزه التي تستعمل كرت انتل لعرض الشاشه. **لايعمل على بيج سر**

اذا كنت تستخدم كرت منفصل :

- `iMac13,2` كاتلينا او اقدم

- `MacPro6,1` بيج سر فما فوق.

![](/img/config-setup/gensmbios.png)

يتم نقل الارقام بالشكل الاتي للكونفق:

- `Type` يتم نسخه الى Generic -> SystemProductName.
- `Serial` يتم نسخه الى  Generic -> SystemSerialNumber.
- `Board Serial` يتم نسخه الى  Generic -> MLB.
- `SmUUID` يتم نسخه الى  Generic -> Generic -> SystemUUID.

### Generic
لاتوجد تعديلات هنا

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

???+ note "Quirks"
	
	| العنوان | مفعل | وصف |
	| :--- | :--- | :--- |
	| IgnoreInvalidFlexRatio | True | |
	| UnblockFsConnect | False | ضروري لمذربوردات HP |
