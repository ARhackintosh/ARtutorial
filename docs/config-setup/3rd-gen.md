# الجيل الثالث مكتبي
- يدعم اوبن كور 0.6.1
- دعم بيج سر غير مؤكد للكرت المدمج


إذا كنت تريد طريقه انشاء الكونفق يدويا ولك معرفه باللغه الانجليزي [هنا ](https://dortania.github.io/OpenCore-Install-Guide/config.plist/ivy-bridge.html#starting-point)رابط يشرح كيفيه انشاء الكونفق للجيل الثالث

**هذه الصفحة معدة على اساس انك تستخدم كونفقات هاكنتوش بالعربي**

## DeviceProperties

### Add

![](/img/config-setup/3rd-gen/6-series-mobo.png)

???+ info "PciRoot(0x0)/Pci(0x16,0x0)"

	اذا كانت لديك مذربورد من الفئة السادسة(H61, B65, Q65, P67, H67, Q67, Z68) ستحتاج الى تغيير رقم جهاز ال IMEI حتى يكون مدعوم,
	قم باضافه الاتي تحت Add
	
	| Value | Type | Key |
	| :--- | :--- | :--- |
	| 3A1E0000 | Data | device-id |


