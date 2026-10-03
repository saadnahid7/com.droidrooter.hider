<div align="center" dir="rtl">

# Android ID and Emulator Hider

**انتحال هوية الجهاز. إخفاء الروت و Xposed. اجتياز الفحص.**

وحدة Xposed/LSPosed من [DroidRooter](https://droidrooter.com).

[![Release](https://img.shields.io/github/v/release/saadnahid7/com.droidrooter.hider?style=for-the-badge&color=teal)](https://github.com/saadnahid7/com.droidrooter.hider/releases/latest)
[![Downloads](https://img.shields.io/github/downloads/saadnahid7/com.droidrooter.hider/total?style=for-the-badge&color=violet)](https://github.com/saadnahid7/com.droidrooter.hider/releases)
[![Android](https://img.shields.io/badge/Android-8%20to%2016-3DDC84?style=for-the-badge&logo=android&logoColor=white)](#التوافق)
[![Xposed API](https://img.shields.io/badge/libxposed%20API-102-orange?style=for-the-badge)](https://github.com/libxposed/api)

[![DroidRooter](https://img.shields.io/badge/DroidRooter-droidrooter.com-2F6BFF?style=for-the-badge)](https://droidrooter.com)
[![Telegram](https://img.shields.io/badge/Telegram-@DroidRooter-2CA5E0?style=for-the-badge&logo=telegram&logoColor=white)](https://t.me/DroidRooter)
[![Facebook](https://img.shields.io/badge/Facebook-DroidRooter-1877F2?style=for-the-badge&logo=facebook&logoColor=white)](https://www.facebook.com/droidrooter)

**اقرأ بلغات أخرى:** [English](README.md) · [Español](README.es.md) · [Deutsch](README.de.md) · [日本語](README.ja.md) · [简体中文](README.zh-hans.md) · [Français](README.fr.md) · [Italiano](README.it.md)

</div>

---

<div dir="rtl">

## لماذا Android ID and Emulator Hider

كثير من التطبيقات ترفض العمل، أو تحدّ من نفسها بصمت، بمجرد أن تظن أن الجهاز
محاكٍ (emulator) أو مُروَّت (rooted) أو يعمل بإطار اختراق (hook framework).
تغيّر هذه الوحدة ما تراه تلك الفحوصات — على مستوى Java والمستوى الأصلي
(native) معًا — بحيث يتصرف التطبيق كما لو كان يعمل على هاتف أصلي غير معدّل.

- اختر من بين **12 ملف تعريف جهاز حقيقي** (Pixel، Galaxy، POCO، OnePlus،
  Redmi، Nothing)، كل منها مبني على تخصيص IMEI موثّق من GSMA وبصمة بناء
  مصنعية حقيقية — وليست قيمًا مختلقة.
- فعّل كل حماية بشكل مستقل، لكل تطبيق، من شاشة واحدة.
- شغّل **Device Check** لترى مباشرة وبدقة ما سيقرأه تطبيق فاحص من جهازك الآن.

الإخفاء الأساسي مجاني دائمًا. يتيح الشراء لمرة واحدة ملفات تعريف مخصصة، والوضع
الآمن، وبعض المعرّفات الإضافية — راجع **Unlock Pro** داخل التطبيق.

## ما الذي تغطيه

| الحماية | ما الذي تغيّره |
|---|---|
| هوية الجهاز | الطراز، العلامة التجارية، الشركة المصنعة، البصمة (fingerprint)، خصائص البناء، معرّف Android ID، الرقم التسلسلي |
| آثار المحاكي | خصائص qemu/goldfish، الملفات، أسماء تعريفات النواة، `/proc/mounts` |
| المعالج | قائمة ABI، `os.arch`، والنص الخام لبائع/طراز المعالج في `/proc/cpuinfo` (أجهزة x86) |
| الرسوميات | الشركة المصنعة لوحدة معالجة الرسومات ونص العرض |
| المستشعرات | أسماء المستشعرات والشركات المصنعة لها |
| البطارية | المستوى، الحالة الصحية، الحالة، السعة، قيم sysfs |
| أجهزة الإدخال | أسماء الأجهزة، `/proc/bus/input/devices` |
| راديو الهاتف | IMEI، IMSI، مشغل/بلد الشريحة، رقم الخط، إصدار النطاق الأساسي |
| الكاميرا | عدد الكاميرات واتجاهها (أمامية/خلفية)، لكل معرّف كاميرا |
| الموقع | استجابة بديلة للتطبيقات التي تطلب آخر موقع معروف ولا تحصل على شيء |
| الروت | `su`، Magisk، KernelSU والملفات التنفيذية/المسارات المرتبطة بها؛ `ro.debuggable`/`ro.secure` |
| Xposed | آثار LSPosed/Vector في `/proc/self/maps`، مدير الحزم، logcat |

## المتطلبات

- جهاز مروَّت (rooted) مزوّد بإطار متوافق مع LSPosed يدعم **libxposed API
  102** الحديثة، مثل [LSPosed](https://github.com/LSPosed/LSPosed) أو
  [Vector](https://github.com/JingMatrix/Vector).
- Android 8.0 أو أحدث.

> [!IMPORTANT]
> هذه الوحدة مبنية على libxposed API الحديثة. لا يُدعم Xposed الكلاسيكي ولا
> EdXposed.

## التثبيت

1. حمّل أحدث ملف APK من [Releases](../../releases/latest) وثبّته.
2. افتح مدير Xposed الخاص بك، فعّل **Android ID and Emulator Hider**، وأضفه
   إلى النطاق (scope) — **يحتاج إلى تضمين نفسه في النطاق** لحماية شاشة
   Device Check الخاصة به، بالإضافة إلى أي تطبيق تريد حمايته.
3. أوقف قسريًا وأعد فتح كل تطبيق أضفته إلى النطاق.

## الاستخدام

1. افتح التطبيق. تُظهر بطاقة الحالة في الأعلى **Protected** بمجرد أن يقوم
   الإطار باختراق (hook) العملية.
2. اختر ملف تعريف جهاز — Pixel 8، Galaxy S24، POCO X3 Pro، وتسعة أخرى.
3. فعّل أو عطّل كل حماية على حدة ضمن **Protection**.
4. اضغط على **Device Check** لترى مباشرة بالضبط ما سيقرأه تطبيق فاحص —
   خصائص البناء، البصمة، المعالج، المستشعرات، البطارية — مقارنة بالملف
   الشخصي النشط.

## التوافق

| إصدار Android | API | الحالة |
|---|---|---|
| 16 | 36 | تم التحقق على جهاز حقيقي |
| 15 | 35 | تم التحقق على جهاز حقيقي |
| 14 | 34 | تم التحقق على جهاز حقيقي ومحاكي |
| 13 | 33 | تم التحقق على جهاز حقيقي |
| 12 وأقل | 31 وأقل | مدعوم (الحد الأدنى minSdk 26)، لم يتم التحقق بشكل مستقل |

تعني كلمة "تم التحقق" أن الوحدة ثُبّتت، وأُضيفت إلى النطاق، وتم تأكيد عملها
(تُفعَّل الاختراقات دون أعطال) على ذلك الإصدار من Android أثناء التطوير.

## الأسئلة الشائعة

**هل يجعل هذا جهازًا حقيقيًا يبدو كمحاكٍ، أم محاكيًا يبدو كجهاز حقيقي؟**
كلاهما. الإخفاء قائم على الهوية وليس على البيئة — فهو يغيّر ما تُبلغ عنه
واجهات برمجة التطبيقات (APIs) في Java والمستوى الأصلي، بغض النظر عمّا يعمل
فعليًا تحتها.

**هل يتجاوز هذا Play Integrity أو SafetyNet؟**
لا. التصديق على الأجهزة (hardware attestation) مدعوم بوحدة TEE/StrongBox
في الجهاز وهو خارج نطاق وصول اختراق Xposed في مساحة المستخدم — يحتاج ذلك إلى
نهج منفصل ومخصص تمامًا.

**لماذا أحتاج إلى تضمين التطبيق في نطاقه الخاص؟**
بدون ذلك، لن تُختَرق عملية التطبيق نفسها أبدًا، لذا ستعرض شاشة Device Check
الخاصة به القيم الحقيقية لجهازك بدلاً من قيم الملف الشخصي النشط — مما يجعل
الميزة الوحيدة المخصصة للتحقق من الإخفاء تعطي قراءة خاطئة.

**هل يمكنني استخدام ملف تعريف لا يطابق أجهزة هاتفي الحقيقية (مثل ملف تعريف
ARM على محاكي x86)؟**
نعم — كل ملف تعريف يخفي المعالج، لذا يتحول Build.SUPPORTED_ABIS و `os.arch`
والنص الخام لبائع المعالج في `/proc/cpuinfo` جميعها لمطابقة الملف الشخصي،
وليس الجهاز المضيف.

## القيود

- أي شيء لا يمر عبر واجهة برمجة Java/أصلية مُخترَقة — المقابس الخام (raw
  sockets)، الفحوصات من جانب الخادم، التصديق على الأجهزة — يرى الجهاز
  الحقيقي.
- تُطبَّق التغييرات في المرة التالية التي يُشغَّل فيها تطبيق محمي؛ التطبيق
  الذي يعمل بالفعل يحتاج إلى إعادة تشغيل.
- يستضيف هذا المستودع الإصدارات (releases) فقط. الكود المصدري مغلق.

## إخلاء المسؤولية

هذه الوحدة مخصصة للخصوصية، والاختبار، والتوافق مع تطبيقاتك الخاصة. أنت
مسؤول عن كيفية استخدامها. لا تستخدمها لخرق شروط أي تطبيق، أو تجاوز الخدمات
المدفوعة، أو خداع أي شخص. البرنامج مقدَّم كما هو، دون أي ضمان.

## شكر وتقدير

- [libxposed](https://github.com/libxposed) على واجهة Xposed API الحديثة
  ومكتبة الخدمة.
- [LSPosed](https://github.com/LSPosed/LSPosed) و
  [Vector](https://github.com/JingMatrix/Vector) على الأطر التي يعمل عليها.

## من DroidRooter

Android ID and Emulator Hider هو مشروع من **DroidRooter**، فريق صغير يبني
أدوات لأجهزة Android المروَّتة.

- **الموقع الإلكتروني:** [droidrooter.com](https://droidrooter.com)
- **تيليجرام:** [@DroidRooter](https://t.me/DroidRooter)
- **فيسبوك:** [facebook.com/droidrooter](https://www.facebook.com/droidrooter)
- **DRVCAM، الكاميرا الافتراضية من DroidRooter:**
  [droidrooter.com/drvcam](https://www.droidrooter.com/drvcam/) يرسل الفيديو
  أو الصور الخاصة بك إلى التطبيقات بدلاً من الكاميرا.
- **VirtualNet، أداة انتحال الشبكة لكل تطبيق من DroidRooter:**
  تغيّر ما تعرفه التطبيقات عن اتصالك بالواي فاي/البيانات الخلوية، مفتوحة
  المصدر.
- **Smali Patcher Reborn:** يُصلح ملف `services.jar` في نظام التشغيل الخاص
  بك مباشرة على الجهاز (Magisk/KernelSU/APatch) لمحاكاة الموقع والنوافذ
  الآمنة، لأنظمة Android من 10 إلى 17 — خليفة Smali Patcher / SmaliPatcherEx.

إذا أعجبك هذا التطبيق، تابع DroidRooter للمزيد.

## الترخيص

ملكية خاصة — جميع الحقوق محفوظة. التوزيع كملف ثنائي فقط؛ الكود المصدري غير
منشور.

</div>
