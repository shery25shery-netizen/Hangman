# بناء التطبيق على GitHub (من غير Android Studio)

## 1) ارفعي المشروع
1. اعملي حساب على github.com (مجاني)، وبعدين **New repository** باسم `hangman`.
2. افتحي الريبو الفاضي واضغطي **uploading an existing file**.
3. فكّي ملف الـ zip، وادخلي جوه فولدر **hangman-app**، واسحبي **كل اللي جواه** (مش الفولدر نفسه) على صفحة الرفع. مهم تتأكدي إن فولدر **.github** اتسحب معاهم.
   - لو مش ظاهر عندك: على ويندوز فعّلي View ← Hidden items.
   - أو بديل: اعملي ملف جديد من **Add file ← Create new file**، واكتبي اسمه `.github/workflows/build-apk.yml` وانسخي جواه محتوى الملف.
4. اضغطي **Commit changes**.

## 2) خدي ملف التطبيق
1. ادخلي تبويب **Actions**. هتلاقي بناء اسمه **Build APK** شغّال لوحده (ياخد 5 إلى 10 دقايق).
2. لما يبقى علامة ✅ خضرا، افتحيه ونزّلي **hangman-apk** من آخر الصفحة (Artifacts).
3. فكّي الملف، وابعتي **app-debug.apk** لموبايلك وثبّتيه.

## 3) للنشر على Google Play (ملف AAB موقّع)
1. اعملي مفتاح مرة واحدة (محتاجة Java على جهازك)، أو اطلبي مني أشرحلك بدائل:
   keytool -genkey -v -keystore release.jks -alias hangman -keyalg RSA -keysize 2048 -validity 10000
2. حوّلي المفتاح لنص: على ماك/لينكس `base64 -i release.jks`، وعلى ويندوز `certutil -encode release.jks key.txt`.
3. في GitHub: **Settings ← Secrets and variables ← Actions ← New repository secret**، وأضيفي 4 أسرار:
   KEYSTORE_BASE64 (نص المفتاح) / KEYSTORE_PASSWORD / KEY_ALIAS (hangman) / KEY_PASSWORD
4. من تبويب **Actions** اختاري **Build AAB for Google Play** ثم **Run workflow**، ونزّلي **hangman-aab**.
5. **احفظي ملف release.jks وكلمات السر في مكان آمن**، لأن من غيرهم مش هتقدري تحدّثي اللعبة.
