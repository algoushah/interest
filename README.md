# 🌐 Interest Form — ayoub.pw

موقع لتسجيل الاهتمامات والتواصل — أي شخص مهتم بنفس المجالات يقدر يتواصل معي مباشرةً.

---

## ✨ ما يفعله الموقع

- 📋 يعرض نموذج تواصل (اسم، بريد، مدينة، اهتمامات)
- 👁️ يُظهر الـ JSON payload قبل الإرسال في الوقت الحقيقي
- 🚀 يرسل البيانات مباشرةً إلى n8n webhook
- 📊 يعرض عداد للطلبات الناجحة والفاشلة

---

## 📁 هيكل المشروع

```
interest-form/
├── index.html        ← الموقع كاملاً (ملف واحد)
└── README.md
```

---

## 🛠️ الاستخدام

### 1. تشغيل الموقع محلياً

```bash
open index.html

# أو عبر سيرفر محلي
npx serve .
```

### 2. الربط بـ n8n ⚡

الـ workflow على `n8n.ayoub.pw`:

```
Webhook  →  Code node  →  Google Sheets / Telegram / Email
```

**⚙️ إعدادات نود الـ Webhook:**

| الحقل | القيمة |
|---|---|
| Method | POST |
| Path | `interests` |
| Response mode | Immediately |

```
https://n8n.ayoub.pw/webhook/interests
```

### 3. 🧩 Code node في n8n

```javascript
const body = $input.first().json;

const name      = body.name;
const interests = body.interests;
const city      = body.city;
const timestamp = body.timestamp;

return [{
  json: {
    name,
    interests,
    city,
    timestamp,
    message: `مرحبا ${name}، تم استلام بياناتك!`
  }
}];
```

---

## 📦 البيانات المُرسلة (JSON Payload)

```json
{
  "name": "Ayoub",
  "email": "info@ayoub.pw",
  "city": "Vienna",
  "interests": ["automation", "ai", "selfhosted"],
  "timestamp": "2026-04-18T10:30:00.000Z",
  "source": "ayoub.pw"
}
```

---

## 🔌 كيف يعمل الإرسال

```javascript
const payload = { name, email, city, interests, timestamp };

const res = await fetch('https://n8n.ayoub.pw/webhook/interests', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify(payload)
});

if (res.ok) console.log('تم الإرسال! ✅');
```

---

## 🚀 النشر

### GitHub Pages

```bash
git init
git add .
git commit -m "init"
git remote add origin https://github.com/algoushah/interest-form.git
git push -u origin main
```

فعّل GitHub Pages من `Settings → Pages → Branch: main`.

### ☁️ Cloudflare Pages

اربط الـ repo من لوحة Cloudflare Pages:
- Build command: _(فارغ)_
- Output directory: `.`

---

## 📬 التواصل

- 🌍 الموقع: [ayoub.pw](https://ayoub.pw)
- 📧 البريد: info@ayoub.pw

---

## 🧰 التقنيات

| الجانب | التقنية |
|---|---|
| 🎨 Frontend | HTML · CSS · Vanilla JavaScript |
| ⚙️ Backend | n8n (self-hosted) |
| 🔗 Protocol | HTTP POST · JSON |
| ☁️ Deploy | GitHub Pages / Cloudflare Pages |

---

*✦ ayoub.pw*
