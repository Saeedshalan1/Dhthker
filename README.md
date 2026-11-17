# ذِكْر — تطبيق التسبيح والاستغفار (Flutter)

تطبيق Flutter واحد يعمل على **Android وiPhone**، جاهز للنشر في Google Play وApp Store.

## المزايا
- دائرة خضراء مضيئة تتحرك بهدوء، وكل ضغطة = ذكر، مع صوت هادئ واهتزاز وتوهّج وعبارة تطفو للأعلى. زر «ثبات» لإيقاف الحركة وثلاث سرعات.
- 6 أنواع: الاستغفار، التسبيح، التهليل، التكبير، التحميد، وأذكار متنوعة تتناوب.
- هدف يومي (100 / 300 / 500 / 1000 أو مخصص)، سلسلة أيام، 7 مستويات، 11 شارة، وتحديات شخصية.
- إحصائيات أسبوعية وشهرية وحسب نوع الذكر.
- تنبيهات: الصباح، المساء، الاستغفار في ساعات تختارها، وتذكير الورد غير المكتمل (يُلغى تلقائياً عند إتمامه).
- واجهة عربية من اليمين لليسار بخطّي أميري وتجوّل، والبيانات محفوظة على الجهاز فقط.

## التشغيل لأول مرة (مرة واحدة فقط)
يتطلب Flutter 3.27 أو أحدث (`flutter --version`).

```bash
cd dhikr_flutter
flutter create . --org com.swalaf --project-name dhikr --platforms android,ios
flutter pub get
dart run tool/setup.dart                 # يضبط الإشعارات والاسم العربي في Android وiOS
dart run flutter_launcher_icons          # يولّد أيقونة التطبيق
dart run flutter_native_splash:create    # يولّد شاشة البداية
flutter run
```

## البناء للنشر
**Android (Google Play):**
```bash
flutter build appbundle --release
```
الملف الناتج: `build/app/outputs/bundle/release/app-release.aab`
(قبل الرفع أنشئ مفتاح توقيع واتبع: https://docs.flutter.dev/deployment/android)

**iPhone (App Store):** يحتاج جهاز Mac وXcode وحساب Apple Developer:
```bash
flutter build ipa --release
```
ثم ارفع الملف عبر تطبيق Transporter أو Xcode.

## هيكل المشروع
```
lib/main.dart                     الجذر والتبويبات
lib/theme.dart                    الألوان والخطوط
lib/data/                         الأذكار، نموذج البيانات، الشارات والمستويات
lib/state/app_state.dart          الحالة والحفظ المحلي
lib/services/notifications.dart   التنبيهات المحلية
lib/services/feedback.dart        الصوت والاهتزاز
lib/screens/                      الذكر، الإحصائيات، الإنجازات، الإعدادات، الترحيب
tool/setup.dart                   تجهيز ملفات Android/iOS
assets/                           الخطوط، الأصوات، الأيقونات
```

معرّف التطبيق: `com.swalaf.dhikr` — غيّره في أمر `flutter create` قبل أول نشر إن أردت.
