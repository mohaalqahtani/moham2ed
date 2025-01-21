---
title: "CTFLearn : Up For A Little Challenge?"
date: 2025-01-21T06:44:00+03:00
categories:
  - CTFLearn
tags:
  - Forensics
---

ستستلم صورة بأمتداد jpg [Begin Hack][Begin-Hack]


بإمكانك استخدام اداة `strings` , أو موقع [aperisolve][aperi-solve]


ومن ثم تظهر لك عدة بيانات منها 
```ruby
`- https://mega.nz/#!z8hACJbb!vQB569ptyQjNEoxIwHrUhwWu5WCj1JWmU-OFjf90Prg -N17hGnFBfJliykJxXu8 -" ,
"Mp real_unlock_key: Nothing Is As It SeemsU" ,
"password: Really? Again" ,
"flag{Not_So_Simple...} .
```


المطلوب من هذه البيانات (الرابط , والعبارة الاولى ) نقوم بالدخول على الرابط , يظهر لنا ملف مضغوط بأسم "Up For A Little Challenge
.zip" , بعد تحميله وفك الضغط عنه 

سيظهر لك مجلد "Did I Forget Again?" , بعد الدخول عليه 

سيظهر ملفين ".Processing.cerb4" , "Loo Nothing Becomes Useless ack.jpg" , 

صورة وملف آخر , عند المحاولة فك ضغط الملف يتطلب رمز سري , الصورة عديمة فائدة بعد الفحص , المهم الان الملف والمهمة التالية (فك الضغط عن الملف والعثور على الرمز السري)

بعد المحاولة بفك الضغط عن الملف بالعبارات التي سبق واستخرجناها ولكن بالبداية فشلت , حاولت بالتلاعب بالجمل مثلا مسافة زائدة مسح حرف الى ان وصلت للرمز السري النهائي `Nothing Is As It Seems` , بدون حرف `U` 

استخرجنا الصورة التي بالملف بأسم `skycoder.jpg` بعد الفحص يظهر العلم بزاوية الصورة اليمنى 

`FLAG : flag{hack_complete}`


[Begin-Hack]: https://mega.nz/file/LoABFK5K#0sEKbsU3sBUG8zWxpBfD1bQx_JY_MuYEWQvLrFIqWZ0
[aperi-solve]: https://www.aperisolve.com