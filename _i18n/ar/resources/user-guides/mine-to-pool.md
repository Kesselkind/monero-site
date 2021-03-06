{% assign version = '1.1.0' | split: '.' %}
{% include disclaimer.html translated="true" version=page.version %}
# إختيار حقل (تجمّع للتعدين)

هُناك العديد من الحقول يمكنك الإختيار منها , قائمه بالحقول المتاحه موجوده بـ [moneropools.com](https://moneropools.com).
التعدين في حقل كبير قد يعني دفعات أكثر تواتراً. ولكن التعدين في حقل أصغر يساعد في الحفاظ علي لامركزيه الشبكه.

# إختيار برنامج تعدين لوحده المعالجه المركزيه (CPU)

تماماً كحقول التعدين هُناك العديد من برامج التعدين. يجب عليك إختيار المُناسب للجهاز الذي تريد التعدين عليه. هذا الدليل سيُغطي التعدين عن طريق وحده المعالجه المركزيه فقط, وسنقوم بإستخدام برنامج
[xmr-stak-cpu](https://github.com/fireice-uk/xmr-stak-cpu). من البدائل برنامج
[wolf's CPUMiner](https://github.com/wolf9466/cpuminer-multi) و برنامج
[sgminer-gm](https://github.com/genesismining/sgminer-gm). إعدادات هذه البرامج تختلف قليلاً ولن يتم تغطيتها في هذا الدليل.

## لأنظمه ويندوز

إذا كنت تستخدم نظام ويندوز يوفر مطور برنامج (xmr-stak-cpu) ملفات التنزيل علي
[GitHub release page](https://github.com/fireice-uk/xmr-stak-cpu/releases).

حمّل `xmr-stak-cpu-win64.zip` وفك ضغطه في مكان سهل الوصول إليه.

## لأنظمه التشغيل الأخري

إذا كنت لا تستخدم نظام ويندوز فسيتعين عليك تجميع xmr-stak-cpu بنفسك ولحسن الحظ لأمر ليس بهذه الصعوبه. قبل أن تتمكن من تجميع برنامج التعدين ستحتاج إلى تثبيت بعض المتطلبات الأساسية الخاصة به.

توزيعات Debian:

    sudo apt-get install libmicrohttpd-dev libssl-dev cmake build-essential

توزيعات Red Hat:

	sudo yum install openssl-devel cmake gcc-c++ libmicrohttpd-devel

<!-- TODO: Add dependencies for other operating systems? -->

بعد ذلك ستحتاج لإستخدام (cmake) لإنشاء ملفات الإنشاء شغل البرنامج وقم بنسخ ملف الإعدادات :

    mkdir build-$(gcc -dumpmachine)
	cd $_
	cmake ../
	make -j$(nproc)
	cp ../config.txt bin/
	cd bin

لا تحتفل بعد حيث يحتاج برنامج التعدين إلى التهيئة. تشغيل البرنامج الآن يجب أن يعطيك كتلة من النص لنسخها ولصقها:

![image1](png/mine_to_pool/1.png)

إفتح `config.txt` وقم *بتبديل* سطرين `"cpu_threads_conf"`بالنص الذي قمت بنسخه, سيبدو كذلك بعدها :

![image2](png/mine_to_pool/2.png)

إنزل للأسفل في الملف إلي أن تجد سطر يحتوي علي `"pool_address"`. *بدّل* المحتوي بين علامات الإقتباس لعنوان ومنفذ حقل التعدين الذي إخترته سابقاً , ستجد هذه البيانات في موقع حقل التعدين.

ضع عنوان محفظتك بين علامات الاقتباس في عنوان المحفظة. يمكنك ترك كلمة المرور فارغة ما لم يحدد حقل التعدين خلاف ذلك.

بعد ذلك ، يجب أن يبدو ملف الإعدادات الخاص بك كما يلي:

![image3](png/mine_to_pool/3.png)

# تشغيل برنامج التعدين

إحفظ ملف *الإعدادات* وشغل برنامج التعدين

![image4](png/mine_to_pool/4.png)

بعض الحقول تسمح لك بمتابعه قوه التعدين الخاصه بعنوانك عن طريق لصق عنوانك في موقعهم. يمكنك أيضاً متابعه قوه التعدين الخاصه بك عن طريق ضغط مفتاح `h`

# ضبط برنامج التعدين

ربما تري رسائل مثل :

	[2017-07-09 12:04:02] : MEMORY ALLOC FAILED: mmap failed

وهذا يعني أنه يمكنك الحصول على زيادة بنسبة 20٪ من قوه التعدين من خلال تمكين الصفحات الكبيرة.

## الصفحات الكبيره علي ليُنكس

أولاً إغلق برنامج التعدين ( إذا كان مازال يعمل ), وقم بتشغيل الأمر التالي لتفعيل الصفحات الكبيره وإبدأ برنامج التعدين كـROOT:

	sudo sysctl -w vm.nr_hugepages=128
	sudo ./xmr-stak-cpu

## الصفحات الكبيره علي ويندوز

مأخوذ من `config.txt`:

>إفتراضياً سنحاول تخصيص الصفحات الكبيره ويعني ذلك أنك تحتاج الشتغيل بصلاحيات المدير علي ويندوز
يجب أن تُعدل سياسات المجموعات علي نظامك لتمكين الصفحات الكبيره. وهذه هي الخطوات
1. في القائمة "ابدأ" ، انقر فوق "تشغيل". في المربع فتح ، اكتب gpedit.msc.
2. في وحده تحكم مُحرر سياسات المجموعات قم بتوسيع إعدادات الحاسوب وبعد ذلك توسيع إعدادات الويندوز
3. وسّع إعدادات الحمايه وبعد ذلك وسّع إعدادات السياسات المحليه.
4. حدد مجلد تعيين حقوق المستخدم
5. سيتم عرض السياسات في نافذه التفاصيل.
6. في النافذه انقر نقراً مزدوجاً فوق تأمين الصفحات في الذاكرة.
7. في إعدادات الأمان المحلية - قفل الصفحات في الذاكره ، انقر فوق إضافة مستخدم أو مجموعة.
8. في مربع حوار إختيار المُستخدمين أو حساب الخدمات أو الجماعات قم بإضافه حساب لتقوم بتشغيل برنامج التعدين عليه
9. إعادة تشغيل لتثبيت التغييرات
