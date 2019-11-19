# usb تجهيز ال

اول نبدا مع سكربت  نذهب الى ملف الذي تم تحميله ثم ننسخ سكربت packappwin.py الى ملف تنزيل الماك والذي سيكون في نفس ملف الموجود فيه اداه gibmacos ثم `macOS Downloads/publicrelase` ثم بعدها اذهب الى ملف الماك الذي نزلته وضع سكربت packappwin.py في نفس الملف 

![](../.gitbook/assets/image%20%2842%29.png)



ثم نفتح السكربت اذا قال لك اختار البرنامج الذي سوف تستخدمه لفتح السكربت اختار اظهر زياده من البرامج ثم البحث عن البرنامج في هذا الكمبيوتر

![](../.gitbook/assets/image%20%2850%29.png)

ثم بعدها اذهب الى هاذا المكان `C:\Users\USERNAME\AppData\Local\Programs\Python` استبدل USERNAME باسم حسابك على الويندوز ستجد ملف داخله افتح الملف وستجد البرنامج python.exe ثم اختار open او فتح



![](../.gitbook/assets/image%20%2864%29.png)

بعد ما يفتح ال cmd نختار p

![](../.gitbook/assets/image%20%2869%29.png)

بعد انتهاء السكربت سوف تلاحظ وجود ملف جديد يسمى SharedSupport

## BootDisk Utility

ننتقل لbdu

نذهب الى option/configuration/checknow للبحث عن اخر اصدار عن الكلوفر

ثم بعدها اختار ال usb الخاص فيك ثم اضغط format **\(سوف نفرمت الفلاش تاكد من نسخ جميع الملفات!!\)**

![](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-Le58xqzAwHioaNemfml%2F-LhVhPnzA4e86uCEV81a%2F-LhViriAJ70BK5y8gFUm%2Fezgif-4-b59bb851e67a.gif?alt=media&token=0acc35ae-1161-44d2-921d-42b730c204fa)

1. ثم اذهب الى **tools/Extract HFS from dmg file**

![](../.gitbook/assets/image%20%2834%29.png)

2.اختار ملف BaseSystem.dmg من ملف تنزيلات الماك من برنامج gibmacos ثم اختار فتح او open

![](../.gitbook/assets/image%20%2860%29.png)

ثم اختار سطح المكتب كمكان لحفظ الملف

![](../.gitbook/assets/image%20%2828%29.png)

بعد ذلك البرنامج سيتسخدم 7zip لاستخراج الملف

![](../.gitbook/assets/image%20%2854%29.png)

بعدها سوف تجد ملف 

4.hfs  على سطح المكتب

الان نرجع الى bdu ثم اضغط على علامه الزائد بجانب ال usb   
ثم اختار part 2 

![](../.gitbook/assets/image%20%2866%29.png)

  
ثم اضغط على زر restore   
بعدها نختار ملف الذي تم استخراجه \(4.hfs\)   
ثم اضغط ok وانتظر حتى يتم نقل الملفات  


## Paragon Partion Manger 

الان سوف نحتاج الى تغير حجم قسم الماك 

نفتح البرنامج ثم بعدها اختار القسم الثاني من الفلاش الذي حجمه 1.87gb 

![](../.gitbook/assets/image%20%2845%29.png)

ثم بعدها اجعل حجم ال newvolume اكبر ما يمكن وثم اضغط change now 

![](../.gitbook/assets/image%20%2865%29.png)



## transmac

الان ياتي دور برنامج Transmac افتح البرنامج كمشرف \(adminstartor\) 

ثم نقوم بسحب ملف SharedSupport من ملف الماك الى Transmac

![](../.gitbook/assets/image%20%285%29.png)





