[README.md](https://github.com/user-attachments/files/27583174/README.md)
# 🦢 The Migrating Crane's Trading Journey

A personal trading journal and dashboard — single HTML file, runs entirely in the browser.

## Features

- 📊 **Trading Ground** — log trades, track open & closed positions
- 📖 **A Crane's Diary** — accountability buddy with share link & per-trade comments
- 📈 **The Migration's Journey** — full statistics, P&L curve, Long/Short donut
- 📅 **Calendar** — daily P&L calendar view (green = profit, red = loss)
- 🔒 **PIN login** — private access screen
- ☁️ **Firebase sync** — cloud backup across devices (optional)
- 🤖 **AI screenshot scanning** — drop a TradingView screenshot, Claude Vision fills in Entry/SL/TP automatically

---

## Quick start

1. Open `index.html` in any browser
2. Set your PIN on first login (min 4 digits)
3. Start logging trades!

No server needed. Everything runs locally.

---

## Firebase setup (optional cloud sync)

Without Firebase your trades are saved in browser `localStorage` only.  
To enable cloud sync across devices:

1. Go to [console.firebase.google.com](https://console.firebase.google.com)
2. Create a new project
3. Add a **Web app** — copy the config object
4. Enable **Firestore Database** (start in test mode)
5. Open `index.html`, find `FIREBASE_CONFIG` near the top of the `<script>` block and replace the placeholder values:

```js
var FIREBASE_CONFIG = {
  apiKey:            "AIza...",
  authDomain:        "your-project.firebaseapp.com",
  projectId:         "your-project-id",
  storageBucket:     "your-project.appspot.com",
  messagingSenderId: "123456789",
  appId:             "1:123456789:web:abc123"
};
```

6. Save and reload — the sync badge in the bottom-right corner turns green ✓

> **Firestore rules** — for personal use, set rules to allow read/write:
> ```
> rules_version = '2';
> service cloud.firestore {
>   match /databases/{database}/documents {
>     match /{document=**} {
>       allow read, write: if true;
>     }
>   }
> }
> ```
> For production, lock this down with proper auth rules.

---

## AI screenshot scanning

The app uses Claude Vision (Anthropic API) to read TradingView screenshots.  
This only works when the file is served through **claude.ai** — the API key is handled automatically.

If you host the file yourself, the OCR field will fall back to manual entry (all other features still work).

---

## Changing your PIN

1. Open browser DevTools (F12)
2. Go to **Application → Local Storage**
3. Delete the key `crane_pin`
4. Reload and set a new PIN

---

## Deploy to GitHub Pages

```bash
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/crane-trading.git
git push -u origin main
```

Then in your repo: **Settings → Pages → Source: main branch / root**

Your journal will be live at `https://YOUR_USERNAME.github.io/crane-trading/`

---

## File structure

```
crane-trading/
├── index.html        ← The entire app (single file)
├── README.md         ← This file
└── .gitignore        ← Ignores sensitive files
```
