# 📰 المسار الأسبوعي — نظام النشرة المدرسية
## Hessa Bent Mohammed School — Weekly Newsletter System

---

## 🚀 نشر الموقع على Firebase + GitHub (خطوة بخطوة)

### المتطلبات
- حساب Google (لـ Firebase)
- حساب GitHub
- Node.js مثبت على جهازك ([nodejs.org](https://nodejs.org))

---

### الخطوة 1 — إنشاء مشروع Firebase

1. اذهب إلى [console.firebase.google.com](https://console.firebase.google.com)
2. اضغط **Add project** → اختر اسماً (مثل: `hessa-newsletter`)
3. أوقف Google Analytics (اختياري) → **Create project**
4. من القائمة الجانبية اختر **Hosting** → **Get started**

---

### الخطوة 2 — تثبيت Firebase CLI

```bash
npm install -g firebase-tools
firebase login
```

---

### الخطوة 3 — تعديل Project ID

في ملف `.firebaserc`، استبدل `YOUR_FIREBASE_PROJECT_ID` بـ ID مشروعك:

```json
{
  "projects": {
    "default": "hessa-newsletter"
  }
}
```

وكذلك في `.github/workflows/firebase-deploy.yml`:
```yaml
projectId: hessa-newsletter
```

---

### الخطوة 4 — رفع الكود على GitHub

```bash
git init
git add .
git commit -m "Initial newsletter system"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPO_NAME.git
git push -u origin main
```

---

### الخطوة 5 — ربط GitHub بـ Firebase (Auto-Deploy)

1. اذهب إلى مشروعك في Firebase Console → **Hosting**
2. اضغط **GitHub** → اربط الـ repository
3. Firebase سيضيف تلقائياً `FIREBASE_SERVICE_ACCOUNT` كـ GitHub Secret

أو يدوياً:
- اذهب إلى GitHub repo → **Settings** → **Secrets and variables** → **Actions**
- أضف secret باسم `FIREBASE_SERVICE_ACCOUNT` والقيمة من Firebase

---

### الخطوة 6 — نشر يدوي (بدون GitHub Actions)

```bash
firebase deploy --only hosting
```

---

### ✅ النتيجة

بعد كل `git push` على فرع `main`، سيُنشر الموقع تلقائياً على:
```
https://YOUR_PROJECT_ID.web.app
```

---

### 📁 هيكل المشروع

```
newsletter-deploy/
├── public/
│   └── index.html          ← ملف النظام الرئيسي
├── .github/
│   └── workflows/
│       └── firebase-deploy.yml  ← Auto-deploy عند كل push
├── firebase.json            ← إعدادات Firebase Hosting
├── .firebaserc              ← Project ID
├── .gitignore
└── README.md
```

---

### ⚠️ ملاحظة مهمة

البيانات محفوظة في `localStorage` في المتصفح — كل جهاز له بياناته المستقلة.  
لمشاركة البيانات بين الأجهزة (معلمون مختلفون) يُنصح بإضافة **Firebase Realtime Database** لاحقاً.
