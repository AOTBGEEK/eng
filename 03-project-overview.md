# 03 - نظرة عامة على المشروع | Project Overview

## وصف شامل للمشروع 🏠

### ما سنبنيه؟

سنقوم ببناء **نموذج منزل ذكي بيئي** من طابقين باستخدام منهجية مرحلية:

**🎮 المرحلة 1: محاكاة Tinkercad (3 أسابيع)**
- تصميم ثلاثي الأبعاد للمنزل
- محاكاة جميع الدوائر الإلكترونية
- برمجة بالبلوكات المرئية
- اختبار شامل للنظام

**🏗️ المرحلة 2: التطبيق الفعلي (5 أسابيع)**
- 🧱 قطع الليغو كهيكل أساسي
- 📟 لوحة ESP32 كدماغ المنزل
- 🔌 حساسات متنوعة للمراقبة
- 💡 مصابيح LED للإضاءة الذكية
- 🔧 محركات صغيرة للحركة

## مكونات المنزل الذكي 🏗️

### الطابق الأول: المنطقة العامة
🛋️ **غرفة المعيشة**:
- حساس حركة للإضاءة التلقائية
- حساس درجة حرارة للتحكم في التهوية
- مصابيح LED ذكية

🍳 **المطبخ**:
- حساس رطوبة للتحكم في التهوية
- نظام إنذار للدخان (محاكاة)
- إضاءة تحت الخزائن

### الطابق الثاني: المنطقة الخاصة
🛏️ **غرفة النوم**:
- حساس ضوء للتحكم في الستائر
- نظام تكييف ذكي
- إضاءة ليلية ناعمة

🚿 **الحمام**:
- حساس حركة للإضاءة
- نظام توفير المياه
- مروحة تهوية تلقائية

### الأنظمة الذكية المدمجة 🤖

#### 0. نظام الطاقة الشمسية المتجددة ☀️🔋
- ☀️ **الألواح الشمسية**: تحويل الطاقة الشمسية إلى كهرباء نظيفة
- 🔋 **إدارة البطاريات**: مراقبة مستوى الشحن والتفريغ التلقائي
- ⚡ **نظام التحويل**: تحويل وتوزيع الطاقة بكفاءة عالية
- 📊 **مراقبة الأداء**: تتبع كمية الطاقة المولدة والمستهلكة
- 🔄 **التحكم الذكي**: تبديل تلقائي بين الطاقة الشمسية والبطارية
- 💡 **مؤشرات LED**: عرض حالة النظام (شحن/بطارية/طوارئ)
- 📈 **توفير الطاقة**: وضع اقتصادي عند انخفاض مستوى البطارية

#### 1. نظام إدارة الطاقة المطور
- 🌞 **استشعار الضوء الطبيعي**: تعديل الإضاءة حسب ضوء النهار والطاقة الشمسية المتاحة
- ⚡ **مراقبة الاستهلاك**: قياس كمية الطاقة المستخدمة وتحسين الكفاءة
- 🔋 **توفير الطاقة الذكي**: إيقاف الأجهزة غير المستخدمة تلقائياً حسب مستوى البطارية
- 📊 **تحليل البيانات**: تسجيل أنماط الاستهلاك اليومية وتحسين الأداء

#### 2. نظام التحكم في المناخ
- 🌡️ **حساس درجة الحرارة**: مراقبة مستمرة لدرجة الحرارة
- 💨 **التهوية الذكية**: تشغيل المراوح عند الحاجة
- 🏠 **العزل الحراري**: تصميم يقلل فقدان الطاقة

#### 3. نظام الأمان والمراقبة
- 👥 **كشف الحركة**: إنذار عند دخول أشخاص غير مصرح لهم
- 🚨 **إنذار الحريق**: تحذيرات فورية عند كشف الدخان
- 🔒 **قفل ذكي**: نظام دخول آمن

#### 4. نظام إدارة المياه
- 💧 **مراقبة الاستهلاك**: قياس كمية المياه المستخدمة
- 🚿 **توفير المياه**: تقليل الهدر في الصنابير
- ☔ **جمع مياه الأمطار**: نظام بسيط لإعادة الاستخدام

## المراحل الزمنية للمشروع 📅

### المرحلة 1: محاكاة Tinkercad (الأسبوع 1-3)
- **الأسبوع 1**: تعلم أساسيات Tinkercad والبرمجة المرئية
- **الأسبوع 2**: تصميم المنزل ثلاثي الأبعاد ووضع المكونات
- **الأسبوع 3**: برمجة المنطق الذكي واختبار جميع السيناريوهات

### المرحلة 2: التحضير للتطبيق (الأسبوع 4)
- تصدير التصميم من Tinkercad
- إعداد قائمة المكونات المطلوبة
- تشكيل الفرق وتوزيع الأدوار للمرحلة الفعلية
- شراء وتجهيز المواد

### المرحلة 3: البناء الفعلي (الأسبوع 5-6)
- بناء هيكل المنزل بالليغو حسب تصميم Tinkercad
- تركيب الأسلاك والمكونات الحقيقية
- نقل البرمجة من البلوكات إلى كود ESP32
- اختبار المكونات الفردية

### المرحلة 4: الدمج والتحسين (الأسبوع 7-8)
- دمج جميع الأنظمة والتأكد من تطابقها مع المحاكاة
- اختبار شامل ومقارنة النتائج مع Tinkercad
- تحسين الأداء وإضافة تحسينات
- إعداد العروض التقديمية وتوثيق الرحلة

## المخرجات المتوقعة 🎯

### منتج نهائي
- ✅ نموذج منزل ذكي يعمل بكامل طاقته
- ✅ كود برمجي موثق ومعلق
- ✅ دليل مستخدم مبسط
- ✅ عرض تقديمي للمشروع

### تعلم الطلاب
- 🧠 فهم عملي للتكنولوجيا الذكية
- 🌱 وعي بأهمية الاستدامة البيئية
- 🤝 مهارات العمل الجماعي
- 🗣️ قدرات التواصل والعرض

## التحديات المتوقعة ⚠️

| التحدي | الحل المقترح |
|--------|--------------|
| صعوبة في البرمجة | ورش تدريبية مكثفة ودعم فردي |
| مشاكل في التوصيلات | رسوم توضيحية ومراجعة دورية |
| عدم عمل الحساسات | قطع احتياطية وخطط بديلة |
| صراعات في الفريق | جلسات حوار وإعادة توزيع الأدوار |
| ضيق الوقت | جدولة مرنة وأولويات واضحة |

## معايير التقييم 📋

### تقييم المنتج (60%)
- **الوظائف (25%)**: هل يعمل المنزل كما هو مطلوب؟
- **التصميم (20%)**: هل المنزل جذاب ومنظم؟
- **الإبداع (15%)**: هل توجد إضافات مبتكرة؟

### تقييم العملية (40%)
- **العمل الجماعي (15%)**: مدى التعاون الفعال
- **المشاركة (15%)**: نشاط الطلاب في الأنشطة
- **العرض التقديمي (10%)**: جودة الشرح والتواصل

هذا المشروع سيكون رحلة تعليمية ممتعة تجمع بين العلم والتكنولوجيا والإبداع! 🚀 