# <i class="fa fa-desktop"></i> الترتيب

---

#### 1. كيف يمكنني رؤية معلومات حول أرقام المنفذ `dcrd` المستخدم؟

يمكنك الحصول على أرقام المنافذ [^ 8929] من متغير العوامل `-h` أو` --help` التي تم تمريرها إلى `dcrd`:

```no-highlight
dcrd -h
```

ابحث عن السطر التالي:

```no-highlight
--rpclisten=  Add an interface/port to listen for RPC connections (default port: 9109, testnet: 19109)
```

يتم تسجيلها أيضا عند بدء `dcrd`:

```no-highlight
12:01:46 2016-02-08 [INF] RPCS: RPC server listening on [::1]:9109
12:01:46 2016-02-08 [INF] RPCS: RPC server listening on 127.0.0.1:9109
```

---

#### 2. ماذا تقصد بملفات التكوين ل `dcrd`،` dcrwallet`، و `dcrctl`؟

يمكن أن يكون لكل تطبيق (`dcrd`،` dcrwallet`، `dcrctl`) ملفات التكوين الخاصة به [^ 9055]. استخدم `-h` وابحث في المسار بين قوسين من خيار ملف التكوين (` -C`، `--configfile`) لمشاهدة المسار الافتراضي. وإنشاء ملف نصي على المسار واسمه وفقا لهذا المسار الذي نظرت للتو.

ثم يمكنك استخدام `dcrd` [نموذج ملف التكوين] (https://github.com/decred/dcrd/blob/master/sample-dcrd.conf) و` dcrwallet` [نموذج ملف التكوين] (هتبس: // github.com/decred/dcrwallet/blob/master/sample-dcrwallet.conf) لتعيين أي خيارات تريدها. يمكنك أن تفعل الشيء نفسه ل `dcrctl` أيضا. التنسيق هو نفسه. يمكن تحديد كل خيار سطر الأوامر المدرجة من قبل `-h` في ملفات التكوين (فقط استخدم اسم الخيار الطويل).

مرة واحدة يتم إنشاءها في مكان، لم يكن لديك لإضافة كل شيء خيارات سطر الأوامر طوال الوقت. على سبيل المثال، يمكنك تشغيل `dcrctl` دون المرور على أي من المعاملات على سطر الأوامر:

```no-highlight
dcrctl getnetworkhashps
2547036949350
```

---

#### 3. يمكنني تشغيل الاختبار الرئيسي والمحفظة المستخدمة  والمحافظ في نفس الوقت وعلى نفس الجهاز؟

نعم [^ 9264]، فقط أضف `--testnet` إلى النقاط المناسبة (` dcrd`، `dcrwallet`،` dcrctl`) وكل شيء سيعمل. هذا هو السبب في أنها تستخدم الموانئ المختلفة والبيانات / سجل الدلائل!

---

#### 4. ما هي الآثار الأمنية لاستخدام نفس كلمات مرور مصادقة خادم ريك مع `dcrd` و` dcrwallet`؟

هناك الكثير أقل يمكنك القيام به مع الوصول إليه `dcrd` مما يمكنك مع الوصول إلى` dcrwallet`. الأهم من ذلك، الوصول ريك [^ 11480] إلى `dcrwallet`، عندما تكون المحفظة غير مقفلة، يمكن استخدامها لقضاء النقود.

عندما `dcrd` و` dcrwallet` على حد سواء على نفس الجهاز، فإنه على الأرجح لا يهم كل ذلك بكثير، ولكن عندما كنت تقوم بتشغيل الاجهزة أكثر أمنا حيث المحفظة على جهاز منفصل من `dcrd`، كنت من الواضح جدا لا تريد استخدام نفس بيانات الاعتماد لكليهما. تذكر أن `dcrd` يجب أن يكون على جهاز مواجه للإنترنت من أجل البقاء متزامنا مع الشبكة (تنزيل البيانات سلسلة كتلة، والمعاملات البث،).

من ناحية أخرى، فإن `dcrwallet` التي تحتوي على أموالك، لتوفر أفضل الأمن، يجب حقا لا يكون على نظام لديه الوصول إلى الإنترنت كما هو أكثر صعوبة بكثير لشخص ما لسرقة القطع النقدية الخاصة بك إذا كانت المحفظة التي تحتوي عليها ليست حتى على جهاز يمكن الوصول إليه عبر الإنترنت. من الواضح، إذا كنت عمادا القطع النقدية الخاصة بك، سوف تحتاج إلى واحد على الأقل `تواجه dcrwallet` الإنترنت. وبالتالي، فإن الإعداد الأكثر أمانا ينطوي على وجود واحدة "الباردة" `المثال dcrwallet` التي هي على الجهاز الذي لا يمكن الوصول إلى الإنترنت، والثانية" الساخنة "` المثال dcrwallet` باستخدام البذور المختلفة بالطبع) التي البرد يقوم مندوبه درواليت بالتصويت من خلال المعلمة `--ticketaddress`، وكلاهما يستخدم بيانات اعتماد مختلفة.

---

#### 5. لماذا يمكنني التواصل مع 8 أقران فقط؟

هناك حد غير مقصود مقصود من 8 أقرانهم الخارجيين [^ 15399]. أكثر من أقران الصادرة من ذلك لا يساعدك بأي شكل من الأشكال، هو في الواقع أسوأ لك وللشبكة. وقد تم اختبار هذا بشكل دقيق للغاية في Bitcoin، بما في ذلك بتسويت (مشروع المنبع للمدمرة). كل ما عليك القيام به عن طريق أوبينغ الاتصالات الصادرة الخاص بك هو النفايات فتحات قيمة من أقرانهم قليلة نسبيا هناك (هناك دائما عدد أكبر بكثير من "leechers" من هناك "البذور").

من ناحية أخرى، زيادة الحد الأقصى للاتصالات، الذي يزيد فقط على عدد الاتصالات الواردة المسموح بها، يساعد الشبكة من خلال ضمان وجود المزيد من فتحات المتاحة لعقد جديدة وعملاء SPV.

---

## <i class="fa fa-book"></i> المصادر

[^8929]: ديكرد، [بوست 8،929شكل ] (https://forum.decred.org/threads/600/#post-8929)
[^9055]: ديكرد ، [بوست 9،062شكل] (https://forum.decred.org/threads/472/page-12#post-9062)
[^9264]: ديكرد، [بوست 9،264شكل] (https://forum.decred.org/threads/626/#post-9264)
[^11480]: ديكرد، [بوست 11،480شكل] (https://forum.decred.org/threads/428/#post-11480)
[^15399]: ديكرد ، [بوست 15،399شكل] (https://forum.decred.org/threads/1371/page-2#post-15399)
