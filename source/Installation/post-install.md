# بعد التثبيت

???+ Success "ادعمنا"
	اذا استمعت باستخدام **شرح تثبيت الهاكنتوش من هاكنتوش بالعربي**
	فضلا ادعمنا لنكمل مشروعنا بدون اعلانات و اي تتبع للمستخدم,
	
	ونحافظ على خصوصيه المستخدم باعلى الدرجات

	<a href="https://www.buymeacoffee.com/arhackintosh" target="_blank"><img src="/../img/bmc.png" alt="Buy Me A Coffee" style="height: 40px !important;width: 140px !important;" ></a>


	<a href="https://liberapay.com/ARhackintosh/donate"><img alt="Donate using Liberapay" src="/../img/donate.svg" style="height: 40px !important;width: 110px !important;" ></a>

هنا اهم الخطوات بعد تثبيت الماك, طبعا هناك خطوات اضافيه مثل تصليح خدمات ابل و تصليح السليب لكن هنا الخطوات الاساسية فقط.

???+ tip "ملحوظة"
	اذا كان معك كرت **انفيديا** [ هنا شرح تثبيت التعريف](https://forum.xn--mgbg4a8cpdl.com/threads/kif-tthbt-tyrifat-anfidia-yl-xai-siira.27)

## نسخ الاوبن كور من ال USB

هذه الخطوه ضروريه حتى يمكنك الاقلاع بدون الحاجه الى USB خارجي (يستحسن دائما ابقاء نسخه احتياطيه من ملف ال EFI على usb في حاله حدوث اي مشكله في الاقلاع من الهاردسك)

سنستخدم سكربت [MountEFI](https://github.com/corpnewt/MountEFI)(تنزله بستخدام زر code) لاظهار اقسام ال EFI في ال usb والهاردسك الداخلي.

لتشغيل السكربت قم بفتح تيرمنال داخل ملف السكربت ثم اكتب:

```
chmod +x MountEFI.command

./MountEFI.command
```
اولا نختار اظهار ال USB
مثلا `install macOS Catalina`
![usb mount](https://dortania.github.io/OpenCore-Post-Install/assets/img/usb-mount.bec53b4c.png)

تاكد من نسخ ملف ال **EFI** كامل لصطح المكتب, ثم بعد ذلك قم بعمل اخراج لقسم ال EFI.

نرجع للسكربت ثم هذه المره نقوم بختيرا الهاردسك الداخلي بدلا عن الUSB.

بعد اظهار قسم ال EFI الخاص بالهاردسك الداخلي, قد تلاحظ وجود ملف APPLE وهو مخصص لتحديث تعريفات الفريم وير.

قم بحذف ملف الEFI الموجود سابقا واستبدله بالخاص بالاوبن كور.

## اخفاء نصوص الاقلاع و تسريع عمليه الاقلاع

### استبدال نسخه اوبن كور DEBUG ب RELEASE

نسخه ال RELEASE هي الافضل للاستخدام اليومي, بينما DEBUG مخصصه لحل المشاكل.

من اجل تحويل النسخ كل الذي عليك هو تنزيل نسخه ال RELEASE ثم استبدل الملفات الاتيه:

- EFI/BOOT/
	- `BOOTx64.efi`
- EFI/OC/Bootstrap/
	- `Bootstrap.efi`
- EFI/OC/Drivers/
	- `OpenRuntime.efi`
- EFI/OC/
	- `OpenCore.efi`

???+ Tip "ملحوظة"
	**اذا نجحت في تثبيت الماك فضلا قم بتفح موضوع في قسم [تم التثبيت](https://forum.هاكنتوش.com/forums/success/) داخل المجتمع واكتب في العنوان نوع الجهاز واصدار الماك, ثم ضع رابط ملف ال EFI, هذا سيساعد الناس التي تمتلك نفس الجهاز وتسرع من عمليه التثبيت, في حاله وجود اي مشكله يرجى كتابتها في الموضوع**

	<p><a class="center-me md-button md-button--primary" href="https://forum.هاكنتوش.com/forums/success/post-thread" style="margin: auto;">اكتب موضوع في قسم تم التثبيت</a></p> 
	
### تعطيل نصوص الاقلاع

لتعطيل النصوص المخصصه لحل المشاكل و تحسين دقه اوبن كور علي تعديل الاتي في **الكونفق**:

![](/img/post-install/nvram.jpg#zoom)

**`NVRAM -> Add -> 7C436110-AB2A-4BBB-A880-FE41995C9F82`**:

- حذف `-v` من الBoot-args

**`NVRAM -> Add -> 4D1EDE05-38C7-4A6A-9CC6-4BCCA8B38C14`**:

- UIScale
	- `01`: دقه عاديه
	- `02`: لتفعيل دقه HIDPI و ضروري لعمل FireVault على الشاشات الصغيرة

![](/img/post-install/misc-debug.jpg#zoom)

**تحت `Misc -> Debug`**

- قم بتعطيل `AppleDebug` لتعطيل وضع حل المشاكل في الاقلاع.

- `Misc -> Debug -> Target`: 3
	- يستخدم لتحديد درجه تسجيل الاخطاء في اوبن كور [خيارات اكثر هنا](https://dortania.github.io/OpenCore-Install-Guide/troubleshooting/debug.html)

![](/img/post-install/uefi.jpg#zoom)

**`UEFI -> Output`**:

- `TextRenderer`:  عدلها الى `BuiltinGraphics`
- `Resolution`: عدلها الى `Max` لتحصل على افضل دقه
  - ايضا يمكنك وضع الدقه بصيغه WxH مثلا 1920x1080

## الاقلاع المباشر للماك

للاقلاع المباشر للماك بدون الحاجه لضغط اي زر, توجه لاعدادت النظام ثم قرص بدء التشغيل او Startup Disk

![](/img/post-install/settingsmenu.jpg#zoom)

ثم بعدها قم بختيار الهاردسك الصحيح للاقلاع

???+ info "ملحوظة"
	في حاله عدم القدرة عمل تعديلات قم الضغط على علامه القفل ثم ضع كلمه مرور الحساب
![](/img/post-install/selectdrive.png#zoom)

## اخفاء قائمه الاقلاع في الاوبن كور

هناك قائمه تظهر في الاوبن كور لاختيار النظام, حتى لو تم اختيار نظام افتراضي تظهر لعده ثواني ثم تختفي.

اذا كنت تريد اخفائها بشكل كامل هنا الطريقه:

قم بالتعديل على الكونفق

ثم عطل **Misc -> Boot -> ShowPicker**

![](/img/post-install/disable-picker.png)

وسيتم اختيار النظام الافتراضي الذي تم اختياره في [الخطوة السابقة](#_4)

## كيفيه تحديث اوبن كور و الكيكستات

لتحديث الكيكستات هناك عده برامج منها سكربت [Lilu-and-Friends](https://github.com/corpnewt/Lilu-and-Friends) وهو يقوم بتحديث 50 كيكست.

اما الاوبن الكور فالتحديثات تصدر **اول اثنين من كل شهر** ويجب عليك استبدال الملفات الاتيه:

- `EFI/BOOT/BOOTx64.efi`
	- `EFI/OC/OpenCore.efi`
	- `EFI/OC/Drivers/OpenRuntime`
 يستحسن ايضا اعاده بناء الكونفق بنائا على السامبل الجديد, نعمل ان نحدث كونفقات هاكنتوش بالعربي والشرح شهريا ايضا.

## نصائح عامه في الهاكنتوش

- دائما قبل التحديث يرجى التأكد من ان الاوبن كور والكيكستات تم تحديثها الى اخر اصدار, وان التحديث الجديد لن يسبب مشاكل.
- قبل عمل اي تعديل على ال `EFI` تاكد من وجود usb احتياطي في حاله عدم اقلاع الجهاز.
- عالم الهاكنتوش اصبح يتغير اسرع ما يمكن, خاصه مع دوره التحديثات الكبيره الخاصه بالشرح و الاوبن كور, لذلك تاكد من متابعه [المجتمع](https://forum.هاكنتوش.com) [وحسابنا على تويتر](https://twitter.com/arhackintosh) للحصول على اخر الاخبار في عالم الهاكنتوش.



