---
description: اهم التعريفات (كيكستات) في عالم الهاكنتوش لتعريف كرت الشبكه و كرت الشاشه وغيرها من الاجزاء الاساسيه في الكمبيوتر.
---

# Kext | اختيار التعريفات

???+ Warning "تنبيه"
	توضع ملفات `.kext` فقط في الاوبن كور.
	ملفات اخرى مثل `.app` او `.kest.dysm` يجب حذفها

???+ info "معلومة"
	**في حاله وجود عده نسخ من الكيكست دائما قم بتنزيل ملف ال RELEASE ولا تحمل ملفات ال source** 

## ماهي التعريفات (Kext) الضروريه لجهازي ؟

الكيكستات(تعريفات) تعتمد على مواصفات الجهاز بالكامل ولا يوجد كيكست واحد يقوم بكامل المهام

في هذا القسم اظهرنا فيه اهم الكيكستات للهاكنتوش

## كيكستات اساسية
هذه كيكستات **اساسية لكل هاكنتوش** وبدونها لن يعمل النظام بشكل صحيح.

* [Virtualsmc.kext](https://هاكنتوش.com/virtualsmc-kext/) 
	* يقوم هذا الكيكست بمحاكاه قطعه ال ==SMC== في اجهزه الماك **بدونه لن يقلع النظام**
	- قم بنسخ Virtualsmc.kext فقط, بقيه الملفات هي [اضافات اختيارية](#virtualsmc)
	* هناك بديل وهو Fakesmc بشكل عام هو كيكست اقدم وبتقنيات اقل, ينصح باستخدامه على **الاجهزه القديمه فقط**.
	
* [Lilu.kext](https://هاكنتوش.com/lilu-kext/)
	* كيكست مسؤول عن عمل باتشات في النظام, العديد من الكيكستات تعتمد عليه مثل virtualsmc,AppleALC,WhateverGreen وغيرها, بدونه لن تعمل.

## اضافات VirtualSMC

عند تنزيلك ل virtualsmc من Github ستلاحظ وجود كيكستات اخرى, هذه عباره عن اضافات هي **ليست ضروريه** لكنه تضيف ميزات مثل اظهار حاله الجهاز. **يستحسن اضافتها بعد الانتهاء من تنزيل النظام** لقليل نسبه حدوث مشاكل.

- SMCProcessor.kext 
	- مخصص لاظهار حراره المعالج **لايعمل على معالجات AMD**
- SMCSuperIO.kext
	- مخصص لاظهار سرعه المراوح **لايعمل على معالجات AMD**
- SMCLightSensor.kext 
	- يستخدم لتعريف حساس الاضائه في الابتوبات **احذفه على الكمبيوتر المكتبي**
	- اذا لم يكن لديك حساس اضائه احذفه, لانه قد يسبب مشاكل في الاقلاع
- SMCBatteryManager.kext
	- مخصص لاظهار حاله البطاريه على الابتوبات **احذفه على الكمبيوتر المكتبي**
	- يرجى عدم استخدامه اذا لم تقم بعمل باتش صحيح لدعم البطاريه, لانه قد يسبب مشاكل بدون باتش.
- SMCDellSensors.kext
	- يسمح بدعم افضل للتحكم بسرعه المراوح على اجهزه ديل
	- **لاتستخدمه اذا لم يكن لديك جهاز ديل**
	
## الايثرنت | Ethernet

???+ Warning "تنبيه"
	يجب تضمين تعريف واحد فقط وعدم اضافه عده تعريفات بنفس الوقت.

الان بشكل اساسي سنستخدم ال Ethernet (السلك) للانترنت لان ال Wi-Fi لايعمل دائما.

يجب ان تعرف نوع كرت Ethernet الخاص بك حتى تعرف تثبت اي تعريف. يمكنك ان تعرف نوع الكرت اما من برنامج [hwinfo](https://www.hwinfo.com/) او من موقع الشركه المصنعه للجهاز او المذبورد.

- [IntelMausi.kext](https://هاكنتوش.com/intelmausiethernet-kext/)
	- مطلوب لمعظم كروت شبكه انتل الحديثه, يدعم  82578, 82579, i217, i218 و intel i219.

- [SmallTreeIntel82576.kext](https://هاكنتوش.com/smalltree-i211-at-patch-kext/)
	- كيكست مخصص لتعريف كروت انتل i211 وهو مبني على كيكست smalltree مع باتش لاضافه دعم i211
	- معظم مذربوردات  ryzen التي تستخدم كروت انتل تحتاج هذا الكيكست
	- لماك هاي سييرا وموهافي(10.13-10.14) استخدم اصدار `v1.2.5` اما كاتلينا(10.15+) فما احدث استخدام `v1.3.0`

- [AtherosE2200Ethernet](https://هاكنتوش.com/atherose2200ethernet-kext/)

	- كيكست مخصص لتعريف كروت Atheros و Killer
	- كرت `Atheros E2500` هو عبارة عن كرت Realtek بشكل اساسي لذلك استخدم تعريف [RealteakRTL8111.kext](https://هاكنتوش.com/realtekrtl8111-kext/)

- [LucyRTL8125Ethernet](https://هاكنتوش.com/lucyrtl8125ethernet-kext/)
	- مخصص للعمل مع كروت Realtek الحديثه التي تعمل بسرعه 2.5gbit/s
	- يحتاج الى اصدار كاتلينا(10.15) او احدث

	
- [RealteakRTL8111.kext](https://هاكنتوش.com/realtekrtl8111-kext/)
	- مخصص لكروت Realtek التي تعمل بسرعه Gigabit
	- لماك 10.12-10.13 استخدم اصدار 2.2.0 اما موهافي(10.14+) فاستخدم 2.3.0

- [RealtekRTL8100.kext](https://هاكنتوش.com/realtekrtl8100-kext/)
	- يعمل مع كروت Realtek بسرعه 10mbit/s-100mbit/s.

## USB

- [USBinjectAll.kext](https://هاكنتوش.com/usbinjectall-kext/)
	-  يستخدم لتفعيل وحدات تحكم(controllers) ال USB من انتل بدون الحاجه لتحديدها في ال acpi.
	- ليس ضروري على الجيل السادس فما فوق(**مذربوردات asrock مازالت تحتاجه**)
	- **لا يعمل على معالجات AMD**
- [XHCI-unsupported.kext](https://هاكنتوش.com/usbinjectall-kext/)
	- ضروري لوحدات التحكم(controllers) الغير مدعومه من النظام بشكل مباشر
	- معالجات AMD لاتحتاج هذا الكيكست
	- طريقه تنزيل الكيكست هي ضغط على code ثم download zip ثم داخل المف ستجد ملف الكيكست 
	- مذربوردات تحتاج هذا الكيكست:
		- H370
		- B360
		- H310
		- Z390(غير ضروري لموهافي او احدث)
		- X79
		- X99
		- مذربوردات AsRock(مذربوردات انتل, **بستثناء Z490**)

## كروت الشاشة | GPUs

- [WhateverGreen](https://هاكنتوش.com/whatevergreen-kext/)
	- يقوم بعمل مهام الباتش لل DRM و تفعيل الاصلاحات في Freamebuffer الخ, كل كروت الشاشه تستفيد من هذا الكيكست. **ويجب تنزيله للمساعده بتعريف الكروت**

???+ tip "ملحوظه"
	[**رابط تعريفات انفيديا (هاي سييرا)**](https://www.tonymacx86.com/nvidia-drivers/)


## الصوت | Sound

???+ Warning "تنبيه"
	يرجى استخدام تعريف واحد فقط.

- [Applealc.Kext](https://هاكنتوش.com/applealc-kext/)
	- يستخدم لعمل باتش ل AppleHDA وهو المسؤول عن تفعيل كرت الصوت داخل الجهاز, اجهزه رايزن قد لايعمل معها المايكروفون
	- يجب ان يكون كرت الصوت الخاص بك موجود في هذه [القائمه](https://github.com/acidanthera/applealc/wiki/supported-codecs)

- [VoodoHDA](https://هاكنتوش.com/voodoohda-kext/)
	- هذا تعريف بديل وهو ليس كيكست بل برنامج تثبته بعد تثبيت النظام, يقدم دعم اوسع, اذا كان كرتك لايعمل مع AppleALC استخدم هذا. يجب حذف Applealc قبل استخدامه وجودته اسوء بفرق كبير عن applealc
	- قد يحل مشكله المايكروفون على معالجات Ryzen 
	
## كيكستات اضافيه
- AppleMCEReporterDisabler(مرفق مع كونفق AMD)
	- كيكست يحل مشكله التوقف عن  AppleMCEReporter في كاتلينا وما بعد.
	- يؤثر على Smbios الاتيه:
		- MacPro6,1
		- MacPRO7,1
		- iMacPro1,1
- [NVMeFix](https://هاكنتوش.com/nvmefix-kext/)
	- يقوم بحل مشاكل تحكم بالطاقه و التهيئة على nvme لم يتم تصنيعها من ابل.
	- يحتاج ماك موهاي(10.14) او احدث حتى يعمل.

## كيكستات مخصصه للابتوبات
حتى تعرف نوع الكيبورد او التراك باد الذي يحتويه لابتوبك اذهب الى مدير الاجهزه (device manger) في ويندوز او `dmesg |grep input` في لينكس

- [VoodooPS2.kext](https://هاكنتوش.com/voodoops2-kext/)
	- يستخدم في الاجهزه التي تحتوي على كيبورد و تراك باد تستخدم PS2
	- اذا كنت تريد تعريف التراك باد ستحتاج [VoodooInput.kext](https://هاكنتوش.com/voodooinput-kext/) (يجب ان يكون بعد voodoops2 في الكونفق)
	
- [VoodooI2C.kext](https://هاكنتوش.com/voodooi2c-kext/)
	-  يستخدم لتشغيل الاجهزه التي تستحدم i2c,عادتا موجوده في الابتوبات من الفئه العليا و لابتوبات بشاشه لمس
	- هذا الكيكست له الاضفات الاتيه:
		- VoodooI2CHID اضافه دعه جهاز Microsoft HID
		- VoodooI2CElan اضافه دعم احهزه Elan التي تستخدم تعريفاتهم الخاصه(**لايعمل على ELAN1200+ استخدم التعريف السابق**)
		- VoodooI2CSynaptics اضافه دعم اجهزه Synaptic
		- VoodooI2CFTE اضافه دعم تراك باد FTE1001
		- VoodooI2CUPDDEngine اضافه دعم تعريفات Touchbase 

## واي فاي | Wi-Fi

ابل دعمها لكروت **الواي فاي ضعيف جدا بحيث كروت RealTek** غير مدعومه بشكل كامل أما **Atheros و انتل** مدعومه جزئيا بينما كروت **Broadcom** هي الكروت الأكثر دعما بحيت فيها من يتعرف تلقائي **OOB** ومنها من تحتاج بعض الكيكست.

### قائمة الكروت المدعومه والغير مدعومة

??? info "الكروت المدعومة"

	* BCM94360CD
	* BCM94331CD
	* BCM94360CS2
	* BCM94352Z
	* BCM94350ZAE

	**High Sierra :**

	* BCM943224
	* AR9285
	* AR9287
	* AR9280
	* AR9380

??? info "الكروت الغير مدعومة"

	**Wireless AC**

	- Intel® Wireless-AC 9560
	- Intel® Dual Band Wireless-AC 8260
	- Intel® Dual Band Wireless-AC 7260

	**Wireless N**

	- Intel® Dual Band Wireless-N 7265
	- Intel® Wireless-N 7265
	- Intel® Dual Band Wireless-N 7260
	- Intel® Wireless-N 7260
	- Intel® Centrino® Advanced-N 6230
	- Intel® Centrino® Wireless-N 1030
	- Intel® Centrino® Wireless-N 130
	- Intel® Centrino® Advanced-N 6235
	- Intel® Centrino® Wireless-N 135
	- Intel® Centrino® Wireless-N 105
	- Intel® Centrino® Wireless-N 2200
	- Intel® Centrino® Wireless-N 2230
	- Intel® Centrino® Wireless-N 1000
	- Intel® Centrino® Advanced-N 6205
	- Intel® Centrino® Wireless-N 100
	- Intel® Centrino® Wireless-N + WiMAX 6150
	- Intel® Centrino® Advanced-N + WiMAX 6250
	- Intel® Centrino® Ultimate-N 6300
	- Intel® Centrino® Advanced-N 6200
	- Intel® Wireless WiFi Link 5100AGN

???+ Warning "تنبية"
	اذا كنت تفكر بتغير كرت الواي فاي الخاص بك على جهاز من تصنيع oem (لابتوبات وكمبيوترات مبنية مسبقا) **انتبه** من **BIOS** جهازك  بحيث هناك احتمال وجود **Whitelist** لسماح لكروت معينه فقط بالعمل, اشهر  الشركات التي تستخدم هذا الطريقه  هي **HP** و **Lenovo** **مقال يشرحها [هنا](https://www.thewindowsclub.com/bios-whitelist)**

### تعريفات كروت الواي فاي

- **تعريف [Itwlm](https://github.com/OpenIntelWireless/itlwm/releases)**

	تعريف مخصص لكروت انتل الحديث وهو اول تعريف يفتح الطريقه لدعم كروت واي فاي انتل على الماك

	???+ Tip "ملحوظة"
		 حتى تعرف اذا كان كرتك مدعوم ام لا قم بتنزيل برنامج hwinfo, من داخله ستعرف ال device id الخاص بالكرت واذا كان مدعوم من التعريف

	??? info "قائمة الكروت المدعومة(itwlm.kext)" 
		
		
		|PCI ID|اسم الكرت|
		|------|-------|
		|0x08b1|AC 7260|
		|0x08b2|AC 7260|
		|0x08b3|AC 3160|
		|0x08b4|AC 3160|
		|0x095a|AC 7265|
		|0x095b|AC 7265|
		|0x3165|AC 3165|
		|0x3165|AC 3165|
		|0x3166|AC 3165|
		|0x24f3|AC 8260|
		|0x24f4|AC 8260|
		|0x24f5|AC 4165|
		|0x24f6|AC 4165|
		|0x24fb|AC 3168|
		|0x24fd|AC 8265|
		|0x2526|AC 9260|
		|0x9df0|AC 9560|
		|0xa370|AC 9560|
		|0x31DC|AC 9560|
		|0x30DC|AC 9560|
		|0x271C|AC 9560|
		|0x271B|AC 9560|
		|0x42a4|AC 9462|
		|0x00a0|AC 9462|
		|0x00a4|AC 9462|
		|0x02a0|AC 9462|
		|0x02a4|AC 9462|
		|0x40a4|AC 9462|
		|0x0060|AC 9461|
		|0x0064|AC 9461|
		|0x0260|AC 9461|
		|0x0264|AC 9461|
		|0x2723|AX200|
		|0x2720|AX201|
		|0x43F0|AX201|
		|0xA0F0|AX201|
		|0x34F0|AX201|
		|0x02F0|AC 9462|
		|0x3DF0|AC 9462|
		|0x06F0|AX201|

- **برنامج [Heliport](https://github.com/OpenIntelWireless/HeliPort/releases)**
	برنامج مرافق لتعريف [itwlm](#itwlm) وهو عبارة عن واجهه للتحكم بالكرت للاتصال بشبكات الواي فاي الظاهره

- **تعريف [AirportBrcmFixup](https://هاكنتوش.com/airportbrcmfixup-kext/)**

	هذا ضروري لإصلاح **WIFI** على العديد من بطاقات **Broadcom** ، بينما لا تحتاجه جميع الكروت ، هو مطلوب بشكل عام عند استخدام بطاقات لاسلكية غير مصنوعة من **Apple** . لديه وظيفة إضافية لتشغيل تعريفات كروت **Broadcom** القديمة في إصدارات أحدث من الماك

- **تعريف [BrcmPatchRAM](https://هاكنتوش.com/brcmpatchram-kext/)**

	مطلوب لجميع البطاقات اللاسلكية غير المصنوعة من **Apple**

- **تعريف [BrcmBluetoothInjector](https://هاكنتوش.com/brcmpatchram-kext/)**

	يستخدم لتشغيل كرت **BCM20702**

- **تعريف [AirPortAtheros40](https://هاكنتوش.com/airportatheros40-kext/)**

	هدا الكيكست مطلوب **لكل كروت Atheros** التي تم **رفع الدعم عنها في اصدار \(Mojave 10.14\)**

	* AR9285
	* AR9287
	* AR9280
	* AR9380

	لتنصيبه يجب نسخه على هذا المسار : **Library/Extensions** لا تلصقه هنا ~~**System/Library/Extensions**~~

	تم انسخ هدا الامر على **Terminal**

	```text
	sudo chown -R root:wheel /L*/E*; sudo chmod -R 755 /L*/E*; sudo kextcache -i /
	```

بشكل عام **افضل حل للواي فاي والبلوتوث هو كرت خارجي** مع تعريف من الشركه مثل **TP-Link** وغيرها من الشركات التي تعطي USB واي فاي **تاكد من وجود دعم للماك** و سوف تعمل معك.

### لواقط WI-FI خارجية (USB)

يبقى هذا هو الحل الاخير أمام العديد من مستخدمي الهاكنتوش لتشغيل **WIFI**, على أجهزتهم نظرا لاستحالة تغيير الكرت الداخلي أو لفقدان الضمان من أجهزتهم.

#### نقاط مهمة عليك معرفتها

* لن تعمل ميزات مثل **AirDrop** و **Handoff** وما إلى ذلك من مزايا
* غير مضمون أنها تشتغل **%100**
* تحتاج لاقط منفصل **للبلوتوث**
* تستخدم معظم البطاقات تعريف **32bit**  لتشغيل **WIFI ( تبقى رهين الشركة المصنعة  حتى  تصدر تحديث لتطبيقاتها الخاصة لاصدارات  Catalina فما فوق )**

ومع كل هذه المشكلات يبقى من الصعب للغاية التوصية بلاقط لاسلكي USB ولكن لا يزال هناك أمل :

???+ Warning "تنبيه"
	هذه التعريفات ليست ملف KEXT بل هي ملف pkg (شبيه بملف exe على ويندوز) تستخدمها بعد التثيبت فقط ولا تضعها في الكلوفر ابدا

#### اليكم تعريف بعض لواقط WIFI المعروفة ذات شرائح Realtek

- تعريف(برنامج) [Wireless-USB-OC-Big-Sur-Adapter](https://github.com/chris1111/Wireless-USB-OC-Big-Sur-Adapter/releases)

	??? Info "قائمة اشهر الكروت المدعومة"

		<table>
		  <thead>
		    <tr>
		      <th style="text-align:center"><b>&#x627;&#x644;&#x643;&#x631;&#x648;&#x62A; &#x627;&#x644;&#x644;&#x64A; &#x64A;&#x62F;&#x639;&#x645;&#x647;&#x627; &#x627;&#x644;&#x62A;&#x639;&#x631;&#x64A;&#x641;</b>
		      </th>
		    </tr>
		  </thead>
		  <tbody>
		    <tr>
		      <td style="text-align:center">
			<p>ASUS_USB-N10E_92CU</p>
			<p>ASUS_USB-N13_92CU</p>
			<p>ASUS_USB-N10_92CU</p>
			<p>ASUS_1870_8812BU</p>
			<p>ASUS_USB-N10E_92CU</p>
			<p>ASUS_USB-N10_92CU</p>
			<p>ASUS_USB-N13_92CU</p>
			<p>ASUS_USB-AC53_8812BU</p>
			<p>ASUS_USB-AC55B1_8812BU</p>
			<p>ASUS_USB-AC56_8812AU</p>
			<p>ASUS_USB-AC55_8812BU</p>
			<p>ASUS_USB-AC68ALL_8814AU</p>
			<p>ASUS_USB-AC68CE_8814AU</p>
			<p>ASUS_USB-AC68FCC_8814AU</p>
			<p>AboCom_8178_92CU</p>
			<p>AboCom_0811_8811AU</p>
			<p>AboCom_8189_92CU</p>
			<p>AboCom_92EU</p>
			<p>AboCom_88EU</p>
			<p>AboCom_AC_8812AU</p>
			<p>AboCom_AC_8812AU</p>
			<p>Actiontec_8811AU</p>
			<p>AirTies_Air2520_8811AU</p>
			<p>AirTies_Air2525_8811AU</p>
			<p>AboCom_8178_92CU</p>
			<p>AboCom_8189_92CU</p>
			<p>Actiontec_8105_SingleBand_8811AU</p>
			<p>Actiontec_8108_DualBand_8811AU</p>
			<p>Amigo_92CU</p>
			<p>Amigo_92CU</p>
			<p>AzureWave_92CU</p>
			<p>Belkin_1004_92CU</p>
			<p>Belkin_1102_92CU</p>
			<p>Belkin_2102_92CU</p>
			<p>Belkin_2103_92CU</p>
			<p>Belkin_92DUVS_1105</p>
			<p>Belkin_92DUVS_110A</p>
			<p>Belkin_92DUVS_120A</p>
			<p>Belkin_F9L1106_v2_8812AU</p>
			<p>Belkin_F9L1106v2_8812AU</p>
			<p>Buffallo_25D_8812AU</p>
			<p>Buffallo_433DM_8811AU</p>
			<p>Buffallo_WI_U2_433DHP_8811AU</p>
			<p>Buffallo_WLP_U2_433DHP_8811AU</p>
			<p>Compare-8010_92CU</p>
			<p>Compare-8011_92CU</p>
			<p>Corega_92CU</p>
			<p>DLink_DWA121_92CU</p>
			<p>DLink_DWA123_92CU</p>
			<p>DLink_DWA131B1_92CU</p>
			<p>DLink_DWA132_92CU</p>
			<p>DLink_DWA133_92CU</p>
			<p>DLink_DWA123_88EU</p>
			<p>DLink_DWA125_88EU</p>
			<p>DLink_DWA131C1_92EU</p>
			<p>DLink_DWA131E_92EU</p>
			<p>DLink_DWA171_8812AU</p>
			<p>DLink_DWA182B1_8812AU</p>
			<p>DLink_DWA182_8812AU</p>
			<p>DLink_DWA192_8814AU</p>
			<p>DLink_GO_USB_N150_88EU</p>
			<p>ELECOM_WDC300SU2S_92CU</p>
			<p>ELECOM_8811AU</p>
			<p>ELECOM_WDB433SU2M_8811AU</p>
			<p>ELECOM_WDC1300DU3_8814AU</p>
			<p>ELECOM_WDC1300SU3_8814AU</p>
			<p>ELECOM_WDC150SU2M_88EU</p>
			<p>ELECOM_WDC433DU2_8812AU</p>
			<p>ELECOM_WDC433SU2M2_8811AU</p>
			<p>EDIMAX- EW-7722UTn V2</p>
			<p>EDIMAX N300</p>
			<p>EDIMAX EW-7811Un</p>
			<p>Edimax_AC1750_8814AU</p>
			<p>Edimax_AC1750_A834_8814AU</p>
			<p>Edimax_AC600_8812AU</p>
			<p>Edimax_EW-7611ULB_8723BU</p>
			<p>Edimax_EW-7811UAC_8812AU</p>
			<p>Edimax_EW-7822UAC_8812AU</p>
			<p>Edimax_EW-7822ULC_8812AU</p>
			<p>Edimax_GLP_8812AU</p>
			<p>Edimax_7811_92CU</p>
			<p>Edimax_7822_92CU</p>
			<p>Feixun_90_92CU</p>
			<p>Feixun_91_92CU</p>
			<p>EnGenius_AC_8812AU</p>
			<p>HP_92CU</p>
			<p>Hawking_HWDN3_92CU</p>
			<p>Hawking_HWUN4_92CU</p>
			<p>Hercules_HWUm300_92CU</p>
			<p>Hercules_HWUp150_92CU</p>
			<p>Hawking_8812AU</p>
			<p>Hawking_HW7ACU_8812AU</p>
			<p>IO_DATA_AC433UM_8812AU</p>
			<p>O_DATA_WN-AC867U_8812AU</p>
			<p>Infocus_INA-LCKEY_8812AU</p>
			<p>IO_DATA_92CU</p>
			<p>Linksys_WUSB6300_8812AU</p>
			<p>Logitec_92CU</p>
			<p>Loopcomm_ACA1_8812AU</p>
			<p>Netgear_A7000</p>
			<p>Netgear_N300MA_92CU</p>
			<p>Netgear_WNA1000M_92CU</p>
			<p>Netgear_WNA3100M_92CU</p>
			<p>Netgear_A6100_8812AU</p>
			<p>Netgear_A6200v2_8812AU</p>
			<p>PCI_BT-Micro3H2X_92CU</p>
			<p>PCI_GW_USEco300_92CU</p>
			<p>PCI_GW_USLight_92CU</p>
			<p>PCI_GW_USNano2_92CU</p>
			<p>PCI_GW_USValue_EZ_92CU</p>
			<p>PCI_SW_WF02-AD15_92CU</p>
			<p>PCI_GW-300S_92EU</p>
			<p>PCI_GW-450S_8812AU</p>
			<p>PCI_GW-900D_8812AU</p>
			<p>Proxim_USB-9100_8812AU</p>
			<p>RTL8188CTV</p>
			<p>RTL8188CTV_0A8A</p>
			<p>RTL8188CTV_8011</p>
			<p>RTL8188CU</p>
			<p>RTL8188CUS_1E1E</p>
			<p>RTL8188CUS_2E2E</p>
			<p>RTL8188CUS_5088</p>
			<p>RTL8188CUS_Combo</p>
			<p>RTL8188CUS_Combo_AFF8</p>
			<p>RTL8188CUS_Combo_AFFB</p>
			<p>RTL8188CUS_Combo_AFFC</p>
			<p>RTL8188CUS_Solo</p>
			<p>RTL8188CUS_VL</p>
			<p>RTL8188CUS_solo_AFF7</p>
			<p>RTL8188CUS_solo_AFF9</p>
			<p>RTL8188CUS_solo_AFFA</p>
			<p>RTL8188RU</p>
			<p>RTL8188RU_Netcore</p>
			<p>RTL8192CU</p>
			<p>RTL8192CU_8177</p>
			<p>RTL8192CU_8178</p>
			<p>RTL8192DU_VS</p>
			<p>RTL8188EU</p>
			<p>RTL8188EU_ETV</p>
			<p>RTL8188EU_VAU</p>
			<p>RTL8192EU</p>
			<p>RTL8192EU-2</p>
			<p>RTL8811AU</p>
			<p>RTL8812AU</p>
			<p>RTL8812AU-VL</p>
			<p>RTL8812AU-VN</p>
			<p>RTL8812AU-VS</p>
			<p>RTL8814AU</p>
			<p>Sitecom_WL365_92CU</p>
			<p>Sitecom_WLA1001v1_92CU</p>
			<p>Sitecom_WLA2102_92CU</p>
			<p>Sitecom_WLA4001_92CU</p>
			<p>Sitecom_WLA1100_88EU</p>
			<p>Sitecom_WLA2104_8812AU</p>
			<p>Sitecom_WLA7100_8812AU</p>
			<p>Sitecom_WLA8100_8814AU</p>
			<p>TPLink-Archer_T2U_NANO</p>
			<p>TL-WN823Nv3</p>
			<p>TL-WN725Nv3</p>
			<p>TL-WN723Nv3</p>
			<p>TL-WN722Nv3</p>
			<p>TL-WN821Nv6</p>
			<p>TPLink_92CU</p>
			<p>TPLink_821v5_92EU</p>
			<p>TPLink_822v4_92EU</p>
			<p>TPLink_823v2_92EU</p>
			<p>TPLink_8812AU_1</p>
			<p>TPLink_8812AU_2</p>
			<p>TPLink_8812AU_3</p>
			<p>TPLink_88EUSU</p>
			<p>TPLink_T4UH_8812AU</p>
			<p>TPLink_T4U_8812AU</p>
			<p>TPLink_T9UH_8814AU</p>
			<p>TRENDnet N150 Micro</p>
			<p>Trendnet_624D_92CU</p>
			<p>Trendnet_648B_92CU</p>
			<p>Trendnet_92DUVS</p>
			<p>TrendNet_TEW804B_8812AU</p>
			<p>TrendNet_TEW805B_8812AU</p>
			<p>TrendNet_TEW809UB_8814AU</p>
			<p>Western_AC_8812AU</p>
			<p>ZyXEL_AC_8812AU</p>
			<p>ZyXEL_92CU</p>
		      </td>
		    </tr>
		  </tbody>
		</table>

- تعريف(برنامج) [Wireless-Ralink-Panel-Utility](https://github.com/chris1111/Wireless-Ralink-Panel-Utility/releases)

	تماما مثل التعريف السابق ، يدعم هاذا التعريف عدد لا بأس به من بطاقات **Dlink /** **Mediatek / Ralink** و يشتغل من  اصدار ماك **10.6.8** الى **كاتالينا** **10.15.4** **لم يتم اختباره على بيج سر**

	??? Info "قائمة الكروت المدعومة"

		  **RT3572 , RT3072 , RT3070 , RT3573 , MT7610 , MT7610 , MT7610**

		  **RT5370 , RT2870 , RT3071 , RT2770 , RT3573 , RT5572 , RT3573**

		  **RT3573 , RT5572 , RT3572**

## بقية الكيكست :

هناك الكثير من الكيكستات وتعتمد على حسب الجهاز مثل الابتوبات هناك كيكستات للبطارية واضائه الكيبورد و العديد من الكيكستات الاخرى التي تعتمد على جهازك هنا في هاكنتوش بالعربي نحاول ارشفة جميع الكيكستات[ **في ارشيف الكيكست**](https://kextarchive.هاكنتوش.com/) وما وظيفتها مع رابط التنزيل لكن تحتاج بحث كبير منك لتعرف اي كيكست تحتاج
