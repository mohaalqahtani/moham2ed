---
title: "CTFLearn : Digital Camouflage"
date: 2025-01-21T10:23:00+03:00
categories:
  - CTFLearn
tags:
  - Forensics
---
<img src="https://img.shields.io/badge/CTF%20Learn-232323?style=for-the-badge"> <img src="https://img.shields.io/badge/Forensics-0083C3?style=for-the-badge"> <img src="https://img.shields.io/badge/Medium-FF9800?style=for-the-badge">


ستستلم ملف بأمتداد pcap [data][data]


أستخدم اداة  [wireshark][wireshark] لكي يمكنك تحليل الملف


ستظهر عدة بيانات واتصالات سنرجع للتحدي والتلميحات ,
حسنا نرغب بالحصول على الرمز السري الذي تم نقله بواسطة الشبكة .
**التلميح الاول : يوجد شخص سجل دخول باستخدام كلمة المرور الخاصة به في وقت سابق , أين توجد بيانات تسجيل الدخول ؟**
**التلميح الثاني : العلم عندما تجده قد يكون غير صحيح , من الممكن انه يكون مشفر .**

الحل الان : 
بعد البحث البسيط عن الاتصال الناجح مع الصفحة أو الموقع , البروتكول (HTTP) يظهر لنا رقم (47) 
بيانات الصفحة منها النموذج (الفورم الخاص بالتسجيل ) 
```html
    <form name="login" class="contentstuff" method="post" action="pages/main.html" onsubmit="modifyPass()">
              <td>Username</td>
              <td><input type="text" name="userid"/></td>
              <td>Password</td>
              <td><input type="password" name="pswrd"/></td>
```
الان لدينا اكثر من طريقة : 
1- البحث بواسطة اسم الادخال (INPUT) , سواء للرمز السري او اسم المستخدم
2- فلتره البحث لـ (HTTP)
3- البحث اليدوي عن الطريقة (Method) في هذه الحالة بتكون POST

أختر الطريقة التي تناسبك 

في هذه الحالة وجدنا البكت رقم (105) يوجد به اسم المستخدم والرمز السري
```html
"userid" = "hardawayn"
"pswrd" = "UEFwZHNqUlRhZQ=="
```

كما هو واضح بإن الرمز السري مشفر 
أستخدم أي اداة تناسبك 
في حالتي بستخدم سايبر شيف [Cyber Chef][cyberchef]

بمجرد ان تضع الرمز المشفر في خانة الادخال سيقترح عليك سايبر شيف بإن يفك الشفرة بواسطة Base64
وعند فكها ستظهر لك (PApdsjRTae)

وهي بالفعل العلم !.


`FLAG : PApdsjRTae`


[data]: https://mega.nz/file/XDBDRAQD#4jRcJvAhMkaVaZCOT3z3zkyHre2KHfmkbCN5lYpiEoY
[wireshark]: https://www.wireshark.org/
[cyberchef]: https://gchq.github.io/CyberChef/