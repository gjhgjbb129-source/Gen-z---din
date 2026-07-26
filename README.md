# Gen Z Din — App banane ke steps (sab kuch phone se ho jayega)

Isme 4 files hain: `index.html`, `manifest.json`, `sw.js`, `icon-192.png`, `icon-512.png`, `apple-touch-icon.png`.
Yeh sab ek saath, ek hi folder mein rakhni hain.

---

## STEP 1 — Live link banao (GitHub Pages, free)

1. Phone browser mein **github.com** kholo, free account banao.
2. Top-right "+" > **New repository** > naam do jaise `genz-din` > **Public** rakho > Create.
3. Us repo ke andar **"Add file" > "Upload files"** dabao.
4. In sabhi files ko upload karo: `index.html`, `manifest.json`, `sw.js`, `icon-192.png`, `icon-512.png`, `apple-touch-icon.png`. Commit karo.
5. Repo ke **Settings > Pages** mein jao. "Branch" mein `main` select karo, Save.
6. 1-2 minute baad ek link milega jaisa: `https://tumhara-username.github.io/genz-din/`
   — yehi tumhara live app link hai, isse koi bhi khol sakta hai, kahin bhi.

---

## STEP 2 — Petition wall ko chalu karo (Firebase, free)

`window.storage` sirf Claude ke andar chalta hai — bahar host karne ke liye maine Firebase laga diya hai. Bas config bharni hai:

1. **console.firebase.google.com** kholo, Google account se login karo.
2. **"Add project"** > naam do (jaise `genz-din`) > baaki default rakh ke Create.
3. Left menu mein **Build > Firestore Database** > **Create database** > **Test mode** select karo (start mein) > enable.
4. Project ke gear icon (⚙️) > **Project settings** > neeche scroll karo **"Your apps"** > `</>` (Web) icon dabao > app ka naam do > Register.
5. Ab ek code dikhega jismein `firebaseConfig = {...}` hoga. Usme se yeh values copy karo: `apiKey`, `authDomain`, `projectId`, `storageBucket`, `messagingSenderId`, `appId`.
6. `index.html` file kholo (GitHub par edit — pencil icon ✏️), aur file ke neeche `firebaseConfig` wale hisse mein apni values paste karo (jahan `YOUR_API_KEY` waghera likha hai). Save/commit karo.

Bas — ab petition wall sabke liye live/shared ho jayega.

**Zaroori:** Firestore "test mode" 30 din baad khud-ba-khud lock ho jaata hai. Usse pehle **Firestore > Rules** mein jaake yeh likh dena (sirf naya data add ho sake, purana delete na ho):

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /signers/{doc} {
      allow read, create: if true;
      allow update, delete: if false;
    }
    match /petition/{doc} {
      allow read, write: if true;
    }
  }
}
```

---

## STEP 3 — Log "download" kaise karenge

Yeh ek **PWA** (Progressive Web App) hai — App Store ki zaroorat nahi. Jab koi tumhara GitHub Pages link kholega:

- **iPhone (Safari):** neeche Share button (⬆️) > **"Add to Home Screen"** > ab unke phone par ek app icon hoga, bilkul normal app jaisa (full screen, apna icon).
- **Android (Chrome):** ऊपर "Install App" ka banner khud aayega, ya 3-dot menu > "Install app".

Yehi aajkal "app download karna" jaisa hi experience hai — bina App Store ke, bina coding ke.

---

## Baad mein agar chaho

- Real App Store app banana ho to Mac + Xcode + Apple Developer account ($99/saal) chahiye hoga — agar interested ho to bata dena, alag se guide bana dunga.
- Change karna ho (text, colors, timeline) to `index.html` file GitHub par seedha edit kar sakte ho (pencil icon), koi coding tool nahi chahiye.
