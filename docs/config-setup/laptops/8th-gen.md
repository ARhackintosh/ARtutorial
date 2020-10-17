# الجيل الثامن laptops
| الدعم | الاصدار |
| :--- | :--- |
| [Coffee lake](https://en.wikipedia.org/wiki/Coffee_Lake) بداية الدعم على الماك | macOS 10.13, High Sierra |
| [Whisky lake](hhttps://en.wikipedia.org/wiki/Whiskey_Lake_(microprocessor)) بداية الدعم على الماك | macOS 10.14.1, Mojave |

إذا كنت تريد طريقه انشاء الكونفق يدويا ولك معرفه باللغه الانجليزي [هنا ](https://dortania.github.io/OpenCore-Install-Guide/config-laptop.plist/coffee-lake.html)رابط يشرح كيفيه انشاء الكونفق للجيل الثامن  لللابتوبات

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


