# (Kext) اختيار التعريفات

## ماهي التعريفات (Kext) الضروريه لجهازي ؟

الكيكستات(تعريفات) تعتمد على مواصفات الجهاز بالكامل ولا يوجد كيكست واحد يقوم بكامل المهام

في هذا القسم اظهرنا فيه اهم الكيكستات للهاكنتوش

## كيكستات اساسية

* [Virtualsmc.kext](https://github.com/acidanthera/VirtualSMC/releases) 
	* يقوم هذا الكيكست بمحاكاه قطعه ال ==SMC== في اجهزه الماك **بدونه لن يقلع النظام**
	* هناك بديل وهو Fakesmc بشكل عام هو كيكست اقدم وبتقنيات اقل, ينصح باستخدامه على **الاجهزه القديمه فقط**.
	
* [Lilu.kext](https://github.com/acidanthera/Lilu/releases)
	* كيكست مسؤول عن عمل باتشات في النظام, العديد من الكيكستات تعتمد عليه مثل virtualsmc,AppleALC,WhateverGreen وغيرها, بدونه لن تعمل.

## اضافات VirtualSMC

عند تنزيلك ل virtualsmc من Github ستلاحظ وجود كيكستات اخرى, هذه عباره عن اضافات هي ليست ضروريه لاكنه تضيف ميزات مثل اظهار حاله الجهاز.

- SMCProcessor.kext 
	- مخصص لاظهار حراره المعالج **لايعمل على معالجات AMD**
- SMCSuperIO.kext
	- مخصص لاظهار سرعه المراوح **لايعمل على معالجات AMD**
- SMCLightSensor.kext 
	- يستخدم لتعريف حساس الاضائه في الابتوبات **احذفه على الكمبيوتر المكتبي**
	- اذا لم يكن لديك حساس اضائه احذفه, لانه قد يسبب مشاكل في الاقلاع
- SMCBatteryManager.kext
	- مخصص لاظهار حاله البطاريه على الابتوبات **احذفه على الكمبيوتر المكتبي**
	- يرجع عدم استخدامه اذا لم تقم بعمل باتش صحيح لدعم البطاريه, لانه قد يسبب مشاكل بدون باتش.
- SMCDellSensors.kext
	- يسمح بدعم افضل للتحكم بسرعه المراوح على اجهزه ديل
	- **لاتستخدمه اذا لم يكن لديك جهاز ديل**
	
## الايثرنت Ethernet :

???+ info "معلومة"
	**في حاله وجود عده نسخ من الكيكست دائما قم بتنزيل ملف ال RELEASE ولا تحمل ملفات ال source** 


الان بشكل اساسي سنستخدم ال Ethernet (السلك) للانترنت لان ال Wi-Fi لايعمل دائما.

يجب ان تعرف نوع كرت Ethernet الخاص بك حتى تعرف تثبت اي تعريف. يمكنك ان تعرف نوع الكرت اما من برنامج [hwinfo](https://www.hwinfo.com/) او من موقع الشركه المصنعه للجهاز او المذبورد.

- [IntelMausi.kext](https://github.com/acidanthera/IntelMausi/releases)
	- مطلوب لمعظم كروت شبكه انتل الحديثه, يدعم  82578, 82579, i217, i218 و intel i219.

- [SmallTreeIntel82576.kext](https://github.com/khronokernel/SmallTree-I211-AT-patch/releases)
	- كيكست مخصص لتعريف كروت انتل i211 وهو مبني على كيكست smalltree مع باتش لاضافه دعم i211
	- معظم مذربوردات  ryzen التي تستخدم كروت انتل تحتاج هذا الكيكست

- [AtherosE2200Ethernet](https://github.com/Mieze/AtherosE2200Ethernet/releases)

	- كيكست مخصص لتعريف كروت Atheros و Killer

- [LucyRTL8125Ethernet](https://github.com/Mieze/LucyRTL8125Ethernet) [**التحميل من هنا**](https://onedrive.live.com/?authkey=%21APjCyRpzoAKp4xs&id=FE4038DA929BFB23%21493866&cid=FE4038DA929BFB23)

	- مخصص للعمل مع كروت Realtek الحديثه التي تعمل بسرعه 2.5gbit/s

	
- [RealteakRTL8111.kext](https://github.com/Mieze/RTL8111_driver_for_OS_X/releases)
	- مخصص لكروت Realtek التي تعمل بسرعه Gigabit

- [RealtekRTL8100.kext](https://github.com/Mieze/RealtekRTL8100) [**التحميل من هنا**](https://onedrive.live.com/?authkey=%21APjCyRpzoAKp4xs&id=FE4038DA929BFB23%21455140&cid=FE4038DA929BFB23)
	- يعمل مع كروت Realtek بسرعه 10mbit/s-100mbit/s.

## USB

- [USBinjectAll.kext](https://github.com/Sniki/OS-X-USB-Inject-All/releases)
	-  يستخدم لتفعيل وحدات تحكم مداخل ال USB من انتل بدون الحاجه لتحديدها في ال acpi.
	- ليس ضروري على الجيل السادس فما فوق(**مذربوردات asrock مازالت تحتاجه**)
	- **لا يعمل على معالجات AMD**
- [XHCI-unsupported.kext](https://github.com/RehabMan/OS-X-USB-Inject-All)
	- ضروري لوحدات التحكم الغير مدعومه من النظام بشكل مباشر
	- معالجات AMD لاتحتاج هذا الكيكست
	- طريقه تحميل الكيكست هي ضغط على code ثم download zip ثم داخل المف ستجد ملف الكيكست 
	- مذربوردات تحتاج هذا الكيكست:
		- H370
		- B360
		- H310
		- Z390(غير ضروري لموهافي او احدث)
		- X79
		- X99
		- مذربوردات AsRock(مذربوردات انتل, **بستثناء Z490**)

## كرت الشاشة \(GPU\) :

بالنسبه **لكرت الشاشة** راح تحتاج تعريف [Whatevergreen.kext](https://github.com/acidanthera/WhateverGreen/releases) و هو اضافه لكيكست[ Lilu.kext](https://github.com/vit9696/Lilu/releases) بحيث استبدلو عدة **kexts** منها **Shiki** و **NvidiaGraphicsFixup** **وغيرها**

{% hint style="info" %}
\*\*\*\*[**رابط تعريفات انفيديا \(هاي سييرا\)**](https://www.tonymacx86.com/nvidia-drivers/)\*\*\*\*
{% endhint %}

## الصوت \(Sound\) :

بالنسبه **للصوت** راح تحتاج تعريف [Applealc.Kext](https://github.com/acidanthera/AppleALC/releases) و وهو اضافه اخرى لكيكست [Lilu.kext](https://github.com/acidanthera/lilu/releases) \(تحتاجهم الاثنين\) اذا كان كرت الصوت عندك موجود في هاذه [القائمه](https://github.com/acidanthera/applealc/wiki/supported-codecs)   
اذا كان كرتك غير موجود هناك تعريف بديل [VoodoHDA.Kext](https://github.com/chris1111/VoodooHDA-2.9.2-Clover-V14/releases) مع دعم اوسع

## واي فاي وبلوتوث Wi-Fi / Bluetooth :

ابل دعمها لكروت **الواي فاي والبلوتوث** ضعيف جدا بحيث كروت **Intel و RealTek** غير مدعومه بشكل كامل أما **Atheros** مدعومه جزئيا بينما كروت **Broadcom** هي الكروت الأكثر دعما بحيت فيها من يتعرف تلقائي **OOB** ومنها من تحتاج بعض الكيكست.

### كروت مدعومة :

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

### كروت غير مدعومة :

**Wireless AX**

* Intel® Wi-Fi 6 AX201
* Intel® Wi-Fi 6 AX200

**Wireless AC**

* Intel® Wireless-AC 9560
* Intel® Wireless-AC 9462
* Intel® Wireless-AC 9461
* Intel® Wireless-AC 9260
* Intel® Dual Band Wireless-AC 3168
* Intel® Dual Band Wireless-AC 8265
* Intel® Dual Band Wireless-AC 8260
* Intel® Dual Band Wireless-AC 3165
* Intel® Dual Band Wireless-AC 7265
* Intel® Dual Band Wireless-AC 7260
* Intel® Dual Band Wireless-AC 3160
* Intel® Dual Band Wireless-AC 7260

**Wireless N**

* Intel® Dual Band Wireless-N 7265
* Intel® Wireless-N 7265
* Intel® Dual Band Wireless-N 7260
* Intel® Wireless-N 7260
* Intel® Centrino® Advanced-N 6230
* Intel® Centrino® Wireless-N 1030
* Intel® Centrino® Wireless-N 130
* Intel® Centrino® Advanced-N 6235
* Intel® Centrino® Wireless-N 135
* Intel® Centrino® Wireless-N 105
* Intel® Centrino® Wireless-N 2200
* Intel® Centrino® Wireless-N 2230
* Intel® Centrino® Wireless-N 1000
* Intel® Centrino® Advanced-N 6205
* Intel® Centrino® Wireless-N 100
* Intel® Centrino® Wireless-N + WiMAX 6150
* Intel® Centrino® Advanced-N + WiMAX 6250
* Intel® Centrino® Ultimate-N 6300
* Intel® Centrino® Advanced-N 6200
* Intel® Wireless WiFi Link 5100AGN
* Intel® Wireless WiFi Link 5300AGN
* Intel® Wireless WiFi Link 5350AGN
* Intel® Wireless WiFi Link 5150AGN

{% hint style="danger" %}
اذا كنت ناوي تغير كرت الواي فاي **انتبه** من **BIOS** جهازك هل به **Whitelist** تعمله شركات مثل **HP** و **Lenovo** مقال يشرح ما هي [هنا](https://www.thewindowsclub.com/bios-whitelist)
{% endhint %}

### تعريفات تحتاجها لتعريف الكروت المدعومة :

#### **تعريف** [**AirportBrcmFixup**](https://github.com/acidanthera/AirportBrcmFixup/releases) **:**

هذا ضروري لإصلاح **WIFI** على العديد من بطاقات **Broadcom** ، بينما لا تحتاجه جميع الكروت ، هو مطلوب بشكل عام عند استخدام بطاقات لاسلكية غير مصنوعة من **Apple** . لديه وظيفة إضافية لتشغيل تعريفات كروت **Broadcom** القديمة في إصدارات أحدث من الماك

#### **تعريف** [**BrcmPatchRAM**](https://github.com/the-darkvoid/BrcmPatchRAM/releases) **:**

مطلوب لجميع البطاقات اللاسلكية غير المصنوعة من **Apple**

#### **تعريف** [**BrcmBluetoothInjector**](https://github.com/RehabMan/OS-X-BrcmPatchRAM) **:**

يستخدم لتشغيل كرت **BCM20702** ، [**التحميل من هنا**](https://bitbucket.org/RehabMan/os-x-brcmpatchram/downloads/)\*\*\*\*

#### **تعريف** [**BT4LEContinuityFixup**](https://github.com/acidanthera/BT4LEContinuityFixup/releases) **:**

يستعمل لحل مشاكل **التزامن \(Continuity\)** التي تسمح بتشغيل :

* Handoff
* Instant Hotspot
* New Airdrop
* Apple Watch Unlock

**عامة غير ضروري تجنبو استخدامه ان لاحظتم وجود مشكل مع الكرت**

#### **تعريف** [**AirPortAtheros40**](https://github.com/khronokernel/Wifi-Buyers-Guide/blob/master/AirPortAtheros40.kext.zip) **:**

هدا الكيكست مطلوب **لكل كروت Atheros** التي تم **رفع الدعم عنها في اصدار \(Mojave 10.14\)**

* AR9285
* AR9287
* AR9280
* AR9380

لتنصيبه يجب نسخه على هذا المسار : **Library/Extensions** لا تلصقه هنا **\*\***~~**System/Library/Extensions**~~\*\*

تم انسخ هدا الامر على **Terminal**

```text
sudo chown -R root:wheel /L*/E*; sudo chmod -R 755 /L*/E*; sudo kextcache -i /
```

بشكل عام **افضل حل للواي فاي والبلوتوث هو كرت خارجي** مع تعريف من الشركه مثل **TP-Link** وغيرها من الشركات التي تعطي USB واي فاي **تاكد من وجود دعم للماك** و سوف تعمل معك.

## لواقط WI-FI خارجية \(USB\) :

يبقى هادا هو الحل الاخير أمام العديد من مستخدمي الهاكنتوش لتشغيل **WIFI** على أجهزتهم نظرا لاستحالة تغيير الكرت الداخلي أو لفقدان الضمان من أجهزتهم.

#### نقاط مهمة عليك معرفتها :

* لن تعمل ميزات مثل **AirDrop** و **Handoff** وما إلى ذلك من مزايا
* غير مضمون أنها تشتغل **%100**
* تحتاج لاقط منفصل **للبلوتوث**
* تستخدم معظم البطاقات تعريف **32bit**  لتشغيل **WIFI \( تبقى رهين الشركة المصنعة  حتى  تصدر تحديث لتطبيقاتها الخاصة على اصدار Catalina \)**

ومع كل هذه المشكلات يبقى من الصعب للغاية التوصية بلاقط لاسلكي USB ولكن لا يزال هناك أمل :

{% hint style="warning" %}
هذه التعريفات ليست ملف KEXT بل هي ملف pkg \(شبيه بملف exe على ويندوز\) تستخدمها بعد التثيبت فقط ولا تضعها في الكلوفر ابدا
{% endhint %}

### اليكم تعريف بعض لواقط **WIFI** المعروفة ذات شرائح **Realtek :**

#### تعريف\(برنامج\) [Wireless-USB-Adapter-Clover](https://github.com/chris1111/Wireless-USB-Adapter-Clover/releases)

#### يعمل على العديد من اللواقط منها :

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

{% hint style="warning" %}
#### لا تنسى عمل هذه الخطوة على ملف config.plist حتى يشتغل معك التعريف
{% endhint %}

![config.plist](.gitbook/assets/image%20%28139%29.png)

#### تعريف\(برنامج\) [Wireless-Ralink-Panel-Utility](https://github.com/chris1111/Wireless-Ralink-Panel-Utility/releases)

تماما مثل التعريف السابق ، يدعم هاذا التعريف عدد لا بأس به من بطاقات **Dlink /** **Mediatek / Ralink** و يشتغل من  اصدار ماك **10.6.8** الى أحدت نظام **كاتالينا** **10.15.4** 

* **RT3572 , RT3072 , RT3070 , RT3573 , MT7610 , MT7610 , MT7610**

  **RT5370 , RT2870 , RT3071 , RT2770 , RT3573 , RT5572 , RT3573**

  **RT3573 , RT5572 , RT3572**

## بقية الكيكست :

هناك الكثير من الكيكستات وتعتمد على حسب الجهاز مثل الابتوبات هناك كيكستات للبطارية واضائه الكيبورد و العديد من الكيكستات الاخرى التي تعتمد على جهازك هنا في هاكنتوش بالعربي نحاول ارشفة جميع الكيكستات[ **في ارشيف الكيكست**](https://kextarchive.هاكنتوش.com/) وما وظيفتها مع رابط التحميل لاكن تحتاج بحث كبير منك لتعرف اي كيكست تحتاج
