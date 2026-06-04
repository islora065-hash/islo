# 🛍️ سوق بلس — متجر إلكتروني بـ Next.js

متجر إلكتروني كامل مع الدفع عند الاستلام، مبني بـ Next.js وجاهز للنشر على Vercel.

---

## 🚀 الميزات

- صفحة رئيسية بأقسام وبطاقات المنتجات
- صفحة تفصيلية لكل منتج مع استمارة الطلب السريع
- API Route يحفظ الطلبات في **Google Sheets**
- إشعار فوري عبر **Telegram Bot**
- تتبع **Meta Pixel** (PageView + Purchase + ViewContent)
- بيانات منتجات في ملف `data/products.json` (سهل التعديل)
- متوافق مع الهاتف بالكامل
- جاهز للنشر على Vercel

---

## 📁 هيكل الملفات

```
souqplus/
├── components/
│   ├── Navbar.js
│   ├── ProductCard.js
│   └── OrderForm.js
├── data/
│   └── products.json        ← أضف/عدّل المنتجات هنا
├── lib/
│   ├── sheets.js            ← Google Sheets helper
│   ├── telegram.js          ← Telegram helper
│   └── pixel.js             ← Meta Pixel helpers
├── pages/
│   ├── _app.js              ← Meta Pixel base code
│   ├── index.js             ← الصفحة الرئيسية
│   ├── api/
│   │   ├── order.js         ← API route لاستقبال الطلبات
│   │   └── products.js      ← API route للمنتجات
│   ├── product/
│   │   └── [slug].js        ← صفحة المنتج
│   └── category/
│       └── [id].js          ← صفحة القسم
├── styles/
│   └── globals.css
├── .env.local               ← متغيرات البيئة (لا ترفع على GitHub)
├── .env.example             ← نموذج المتغيرات (ارفع هذا)
└── next.config.js
```

---

## ⚙️ خطوات الإعداد

### 1. تثبيت المشروع

```bash
npm install
```

### 2. إعداد Google Sheets

1. اذهب إلى [console.cloud.google.com](https://console.cloud.google.com)
2. أنشئ مشروعاً جديداً
3. فعّل **Google Sheets API**
4. أنشئ **Service Account** من قسم IAM
5. حمّل ملف JSON للمفتاح
6. افتح Google Sheets جديد وأنشئ **ورقة باسم `الطلبات`**
7. أضف رؤوس الأعمدة في السطر الأول:
   ```
   التاريخ | الاسم | الهاتف | الولاية | المنتج | السعر | الحالة
   ```
8. شارك الـ Sheet مع `client_email` الموجود في ملف JSON (صلاحية Editor)
9. انسخ `client_email` و `private_key` و `spreadsheet ID` (من رابط الـ Sheet) إلى `.env.local`

### 3. إعداد Telegram Bot (اختياري)

1. ابحث عن **@BotFather** في تيليجرام
2. أرسل `/newbot` وأنشئ بوت جديد
3. احتفظ بـ `BOT_TOKEN`
4. أرسل رسالة للبوت، ثم اذهب إلى:
   `https://api.telegram.org/bot<TOKEN>/getUpdates`
5. انسخ `chat_id` من الرد
6. أضف القيمتين إلى `.env.local`

### 4. إعداد Meta Pixel

1. اذهب إلى [Meta Events Manager](https://www.facebook.com/events_manager)
2. أنشئ Pixel جديد
3. انسخ Pixel ID وأضفه إلى `.env.local` كـ `NEXT_PUBLIC_META_PIXEL_ID`

### 5. تشغيل محلي

```bash
npm run dev
```

افتح [http://localhost:3000](http://localhost:3000)

---

## 🌐 النشر على Vercel

```bash
# 1. ارفع المشروع على GitHub
git init
git add .
git commit -m "first commit"
git remote add origin https://github.com/username/souqplus.git
git push -u origin main

# 2. اذهب إلى vercel.com وربط المستودع
# 3. أضف متغيرات البيئة في Vercel Dashboard:
#    Settings > Environment Variables
#    أضف جميع القيم من .env.local
```

> **مهم:** لا ترفع ملف `.env.local` أبداً على GitHub.
> ملف `.gitignore` يمنع ذلك تلقائياً.

---

## ➕ إضافة منتج جديد

افتح `data/products.json` وأضف كائن JSON بهذا الشكل:

```json
{
  "id": "7",
  "name": "اسم المنتج",
  "slug": "product-slug",
  "category": "electronics",
  "price": 5000,
  "badge": "جديد",
  "emoji": "📦",
  "color": "#1a1a2e",
  "description": "وصف المنتج...",
  "features": ["ميزة 1", "ميزة 2"],
  "images": [],
  "inStock": true,
  "rating": 4.5,
  "reviews": 0
}
```

الأقسام المتاحة: `electronics` | `clothing` | `home` | `beauty`

---

## 📊 هيكل Google Sheet

| التاريخ | الاسم | الهاتف | الولاية | المنتج | السعر | الحالة |
|---------|-------|--------|---------|--------|-------|--------|
| 01/01/24 | أحمد | 0551234567 | الجزائر | سماعات | 4500 دج | جديد |

---

## 🛠 التقنيات المستخدمة

- [Next.js 14](https://nextjs.org)
- [Google Sheets API](https://developers.google.com/sheets)
- [Meta Pixel](https://developers.facebook.com/docs/meta-pixel)
- [Vercel](https://vercel.com) للاستضافة
