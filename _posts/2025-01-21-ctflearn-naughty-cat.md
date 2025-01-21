---
title: "CTFLearn : Digital Camouflage"
date: 2025-01-21T11:11:11+03:00
categories:
  - CTFLearn
tags:
  - Forensics
---
<img src="https://img.shields.io/badge/CTF%20Learn-232323?style=for-the-badge"> <img src="https://img.shields.io/badge/Forensics-0083C3?style=for-the-badge"> <img src="https://img.shields.io/badge/Medium-FF9800?style=for-the-badge">


ستستلم صورة بأمتداد png [cut3_c4t][data]


بعد استخدام اداة `Strings` يظهر لنا عدة بيانات وملفات مدموجة

```html
y0u_4r3_cl0s3.rar
Cat!
f1n4lly.txt0
K_Vk
 gY 
purrr_2.mp3
```

نقوم باستخراج الملفات المدموجة عن طريق اداة `Binwalk` 

```html
28E4B.rar
29
29.zlib
purrr_2.mp3
y0u_4r3_cl0s3.rar
```

بعد تفحص كل ملف باستخدام أمر `file` يظهر لنا التالي : 

```html
28E4B.rar: RAR archive data, v5
29: empty
29.zlib: zlib compressed data
purrr_2.mp3: Audio file with ID3 version 2.3.0, contains: MPEG ADTS, layer III, v1, 128 kbps, 44.1 kHz, JntStereo
y0u_4r3_cl0s3.rar: data

```

نعود بأستخدام أمر `Strings` على كل من الملفات المستخرجة لكي نتأكد منها

المخرجات : 

**28E4B.rar**
```html
yW<UL
y0u_4r3_cl0s3.rar
Cat!
f1n4lly.txt0
K_Vk
 gY 
purrr_2.mp3
```

**29**
```html
empty - فارغ
```

**29.zlib**
```html
y0u_4r3_cl0s3.rar
Cat!
f1n4lly.txt0
K_Vk
 gY 
purrr_2.mp3
```

**purrr_2.mp3**
```html
 -TPE1
is a password here?
Xing
!#&'*,/147:<?BEHJLNQSVY\^adgilopsuxz
PLAME3.99r
```

**y0u_4r3_cl0s3.rar**
```html
Cat!
f1n4lly.txt0
K_Vk
```

نلاحظ ان أخر مخرجين هم الاهم 
الملف الصوتي يظهر به تلميحه بأن (هل الرمز السري متواجد هنا ؟) 
الملف المضغوط يظهر به ملف بعنوان النهاية وغالبا يوجد به العلم .


يظهر لنا بملف `y0u_4r3_cl0s3.rar` بانه ملف بيانات وليس RAR

سنحتاج لأصلاحه لكي يعمل الملف المضغوط 

الاصلاح بيتم عن طريق الـ HEX 

يتواجد اكثر من موقع و تطبيق لعرض الهيكس وتعديله سأستخدم [Hexed IT][hexed-it]

نحتاج صفحة في ويكيبيديا لكي نتأكد من تواقيع الهيكس لكل ملف [الصفحة][wikipedia]

نبحث عن RAR في الصفحة حتى نجد الاصدار 5 والتوقيع الخاص به 

نفتح الملف المضغوط في موقع تعديل الهيكس ونلاحظ بانه غير مطابق للتوقيع الافتراضي للRAR 

نقوم بتعديله 

```html
التالف :
43 61 74 21 1A 07 01 00
الاصلي :
52 61 72 21 1A 07 01 00
```

بعد التعديل نقوم بتحميل الملف من جديد ومن ثم فتحه 

سيتطلب رمز سري لفتح الملف المضغوط بعد تعديله

تبقى لدينا الملف الصوتي بحكم اننا حصلنا على تلميحه بداخله 

بعد فتح الملف الصوتي لايظهر لنا شيء مفيد به 

سنستخدم الـ Spectrogram على الملف الصوتي 

توجد تطبيقات ومواقع عدة لعمل الخاصية هذه منها الموقع [ING Now][ing-now] تطبيق [Audacity][audacity]

بعد ان نطبق الخاصية على الملف الصوتي يظهر لنا نص 

`sp3ctrum_1s_y0ur_fr13nd`

نقوم بتجربته على الملف المضغوط 

قام بالفتح بعد فتح الملف النصي داخل الملف المضغوط يظهر لنا التالي : 

```html
            __/| 
            \o.O|
       _____(___)______ 
      |       U        |________    __
      |ZjByM241MWNzX21h|        |__|  |_________
      |________________|NXQzcg==|::|  |        /
      |                \._______|::|__|       <
      |                         \::/  \._______\
      |	
      |	
```

النص التالي : `ZjByM241MWNzX21hNXQzcg==` مشفر بتشفير Base64 

نضعه في موقع سايبر شيف [Cyber Chef][cyberchef] ونختار فك التشفير التلقائي سيظهر لنا العلم النهائي : `f0r3n51cs_ma5t3r`


`FLAG : f0r3n51cs_ma5t3r`


[data]: https://ctflearn.com/challenge/download/890
[hexed-it]: https://hexed.it/
[wikipedia]: https://en.wikipedia.org/wiki/List_of_file_signatures
[ing-now]: https://convert.ing-now.com/audio-spectrogram-creator/
[audacity]: https://www.audacityteam.org/
[cyberchef]: https://gchq.github.io/CyberChef/