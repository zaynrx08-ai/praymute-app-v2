# Pray Mute — Android App (Ready Project)

## 🚀 Sabse Aasan Tareeka — Bina Kuch Install Kiye APK Kaise Milegi

Agar aapke paas Android Studio nahi hai / install nahi karna chahte, to
GitHub ka free robot (Actions) aapke liye APK khud bana dega — sirf browser
chahiye.

1. https://github.com par free account banayein (agar nahi hai).
2. Naya repository banayein (koi bhi naam, e.g. `praymute-app`) — **Public**
   rakhein taaki free build mile.
3. Repository ke andar "Add file" > "Upload files" par click karke is poore
   `PrayMute` folder ke andar ka **sara content** (jitni bhi files/folders
   hain, sab ek saath) drag-and-drop kar dein. "Commit changes" dabayein.
4. Upar "Actions" tab par jaayein — ek build apne aap start ho jaayega
   (2-5 minute lagte hain). Green tick ✅ ka wait karein.
5. Us build entry ke andar "Artifacts" section mein **PrayMute-app** naam
   ki file milegi — usse download karein, andar `app-debug.apk` hoga.
6. Ye `.apk` file apne Android phone mein bhejein (WhatsApp/Drive/USB se) —
   phone mein "Unknown apps install" allow karke install kar lein. Bas, app
   chalu ho jaayegi aapke phone par.

Ye APK **testing ke liye** hai (debug build). Play Store par daalne ke liye
uske baad "signed release build" banana hoga — us step par bhi help kar
dunga jab test ho jaaye.

---

## ⚠️ Sabse Zaroori Baat — Firebase Config Abhi Khaali Hai!

Aapki HTML file mein `firebaseConfig` object abhi bhi placeholder values pe hai
(`YAHAN_APNI_API_KEY_DALEIN` waghera). Iska matlab:

- **Masjid Add karna, Masjid ka time change karna, Admin login** — ye sab
  features Firebase se connect hote hain. Jab tak aap apna khud ka Firebase
  project bana kar real config nahi daalenge, ye kaam NAHI karenge.
- Location: `app/src/main/assets/index.html` file mein dhundo `firebaseConfig`
  (search karein "YAHAN_APNA").

### Firebase set karne ke steps:
1. https://console.firebase.google.com par jaake naya project banayein.
2. Project ke andar "Firestore Database" enable karein.
3. "Authentication" mein "Email/Password" sign-in method enable karein
   (admin login ke liye).
4. Project Settings > General > "Your apps" mein "Web app" add karein —
   wahan se aapko config object milega (apiKey, projectId, waghera).
5. Wo config copy karke `firebaseConfig` object mein paste kar dein.
6. Firestore > Rules tab mein wahi rules paste karein jo HTML file ke
   comments mein already likhi hui hain (upar dekhein).

Iske bina app khulega, UI dikhega, lekin masjid add/edit/admin panel kaam
nahi karega — sirf isi wajah se.

---

## Naya Kya Add Kiya Gaya Hai (Real Native Features)

Original HTML sirf ek website/PWA ki tarah kaam karta tha jisme comment mein
khud likha tha: *"browser phone ko actual Silent/DND mode mein nahi daal
sakta"*. Isliye maine iska native Android wrapper banaya aur ek asli feature
add kiya:

- **Real Auto-Silent (DND) toggle** — Ab jab app Android ke andar chalti
  hai, to "Phone Silent Kar Diya" button dabane par phone **sach mein**
  Silent/Vibrate mode (aur Do Not Disturb) mein chala jaata hai, aur set kiye
  gaye time ke baad khud-ba-khud wapas Normal mode mein aa jaata hai. Ye sirf
  ek naya "Settings" screen mein button se ek baar permission maangega
  ("Allow Auto-Silent Permission") — Android ka niyam hai ki ye permission
  user ko khud allow karni padti hai (koi bhi app chhup ke nahi le sakti).
- App icon, splash screen (loading screen), aur launcher name "Pray Mute"
  set kar diya gaya hai.
- Location, Notification, aur Do-Not-Disturb — teeno zaroori Android
  permissions manifest mein add kar di gayi hain.

## Kya Kaam Nahi Kiya Gaya (Scope se bahar, agar chahiye to bata dena)

- **Background scheduling**: Abhi reminders tabhi trigger honge jab app
  khuli hui hai (foreground mein). Agar app band/kill kiya jaaye to bhi
  automatically reminder aaye — iske liye alag se AlarmManager/WorkManager
  wala background system banana padega. Bata dena agar ye bhi chahiye,
  agle step mein bana dunga.

---

## APK/AAB Kaise Banayein (Play Store ke liye)

Ye ek standard Android Studio Gradle project hai.

1. **Android Studio** install karein (free): https://developer.android.com/studio
2. Is poore `PrayMute` folder ko Android Studio mein **Open** karein
   (File > Open > PrayMute folder select karein).
3. Gradle sync hone dein (pehli baar internet chahiye, dependencies download
   hongi).
4. **Testing ke liye**: Build > Build APK(s) — banaa hua APK apne phone mein
   daal kar test kar sakte hain.
5. **Play Store ke liye (AAB)**:
   - Build > Generate Signed Bundle / APK > **Android App Bundle** choose
     karein.
   - Naya keystore banayein (ye file sambhal kar rakhein — future updates ke
     liye zaroori hai, kho gayi to app update nahi kar paayenge).
   - `.aab` file generate hogi — yahi file Play Console pe upload karni hai.
6. https://play.google.com/console par jaake ($25 one-time registration fee)
   naya app banaye, store listing (screenshots, description, privacy policy
   link) bharein, aur `.aab` upload karke submit kar dein.

---

## Project Structure
```
PrayMute/
├── app/
│   ├── src/main/
│   │   ├── assets/index.html      ← aapki original app (thoda modified)
│   │   ├── java/.../MainActivity.kt ← WebView + real Silent/DND bridge
│   │   ├── res/                   ← icon, colors, splash theme
│   │   └── AndroidManifest.xml    ← permissions
│   └── build.gradle
├── build.gradle
└── settings.gradle
```

Package name: `com.praymute.app` (chahen to build.gradle + AndroidManifest
mein badal sakte hain, launch ke baad ye badalna mushkil hota hai isliye
abhi hi final kar lein).
