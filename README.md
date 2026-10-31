# HikariManga - مستودع كود أندرويد الأصلي المستنسخ (Kotlin + Jetpack Compose)

هذا المستودع يمثل إعادة بناء شاملة وعالية الكفاءة لتطبيق **HikariManga (v1.4.3)** مع استخراج كامل للبنية المعمارية وقواعد البيانات ومحرك القراءة.

---

## 1. البنية المعمارية (Architecture Overview)

- **نمط التصميم**: Clean Architecture + MVVM + StateFlow.
- **واجهة المستخدم (UI)**: Jetpack Compose مع Material Design 3، ودعم كامل للوضع الليلي (Dark Mode) والاتجاه من اليمين لليسار (RTL).
- **محرك القراءة (Reader Engine)**:
  - نمط التمرير العمودي المستمر (Webtoon Mode) باستخدام `LazyColumn`.
  - نمط تقليب الصفحات يمين-يسار (Japanese Manga RTL) ويسار-يمين (LTR) باستخدام `HorizontalPager`.
  - إيماءات التكبير والتصغير (Pinch-to-zoom) حتى 300%، والنقر في المنتصف لإظهار/إخفاء أشرطة التحكم.
  - طبقة OCR الذكية لمحاكاة ترجمة فقاعات الحوار (Bounding Boxes).
- **قاعدة البيانات المحلية (Room Database)**:
  - مطابقة تامة للجداول المستخرجة من الـ APK:
    - `continue_reading`: متابعة القراءة، رقم الفصل، رقم الصفحة، ونسبة الإنجاز.
    - `favorites`: قائمة المفضلة المحلية مع علم المزامنة السحابية `isSynced`.
    - `chapter_ocr_cache`: تخزين إحداثيات فقاعات النصوص والنصوص المترجمة.
- **جسر الكشط البرمجي (Scraper Engine)**:
  - محاكاة دقيقة لـ `window.HikariBridge` لتنفيذ كود الجافاسكريبت داخل الـ WebView واستخراج الفصول والصفحات.

---

## 2. متطلبات التشغيل (Prerequisites)

- **Android Studio**: إصدار Ladybug أو Koala (2024.1+) أو أحدث.
- **JDK**: Java Development Kit 17 أو 21.
- **Android SDK**: Compile SDK 35, Min SDK 26 (Android 8.0 Oreo فما فوق).
- **المحاكي (Emulator)**: أي جهاز افتراضي (AVD) مثل Pixel 8 يعمل بنظام Android 13 أو 14.

---

## 3. خطوات التشغيل على المحاكي المحلي (Step-by-Step Run)

1. **فك ضغط المستودع**:
   ```bash
   unzip HikariManga_Android_Project.zip -d HikariManga
   ```
2. **فتح المشروع في Android Studio**:
   - افتح **Android Studio**.
   - اختر **Open** ثم حدد مجلد `HikariManga`.
   - انتظر حتى يكتمل فحص ومزامنة Gradle (Gradle Sync).
3. **تشغيل المحاكي (AVD)**:
   - افتح **Device Manager** في Android Studio وشغل محاكي Pixel 8.
4. **بناء وتشغيل التطبيق**:
   - اضغط على زر **Run 'app'** (أو Shift + F10) في شريط الأدوات العلوي.
   - أو عبر سطر الأوامر:
     ```bash
     ./gradlew installDebug
     ```
