# 🪖 Platoon Control

> Web app for daily operational management of a platoon, built as a personal project by a Brazilian Army officer studying Software Engineering.

![HTML](https://img.shields.io/badge/HTML5-single--file-c8922a?style=flat-square&logo=html5&logoColor=white)
![CSS](https://img.shields.io/badge/CSS3-dark--theme-3a4230?style=flat-square&logo=css3)
![JavaScript](https://img.shields.io/badge/JavaScript-vanilla-e8b84a?style=flat-square&logo=javascript&logoColor=black)
![PWA](https://img.shields.io/badge/PWA-installable-5a9040?style=flat-square)
![localStorage](https://img.shields.io/badge/storage-localStorage-4a82b0?style=flat-square)

---

## About the project

A progressive web app (PWA) built to replace Excel spreadsheets in the daily control of a Brazilian Army rifle platoon. The goal was to create a lightweight, offline-capable tool that installs like a mobile app, with no server, database, or external framework dependencies.

The entire project lives in **a single HTML file**, which makes it easy to distribute and use in environments with limited connectivity.

**Privacy note:** this app has no backend, all data entered stays only in the user's device `localStorage` and is never sent to any server. The sample data included in the code is fictional, generated only to demonstrate the interface.

---

## Features

| Module                 | Description                                                                                                                     |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| **Dashboard**          | Real-time KPIs, accumulated delays, medical visits, punishments, and monthly performance notes. Automatic rankings by category. |
| **Personnel Registry** | Complete enlisted records with functional and profile data.                                                                     |
| **Delays**             | Occurrence log with a running count per soldier.                                                                                |
| **Punishments**        | Formal record with type, period, and issuing authority.                                                                         |
| **Medical Leave**      | Tracking of medical visits and absences, with or without service exemption.                                                     |
| **Performance Notes**  | Positive (FO+) and negative (FO−) observed facts for performance evaluation.                                                    |
| **Birthdays**          | Platoon calendar organized by month, with a countdown to the next one.                                                          |

---

## Tech stack

The project was intentionally built without frameworks to reinforce core web development fundamentals:

- **Semantic HTML** — SPA structure with multiple "pages" via `display: none / block`
- **Pure CSS** — custom properties, responsive grid, dark military theme
- **Vanilla JavaScript** — DOM manipulation, array methods (`.map()`, `.filter()`, `.reduce()`), template literals
- **localStorage** — session persistence with no backend
- **PWA** — manifest, service worker, and offline cache generated inline via `Blob` + `URL.createObjectURL()`
- **Mobile-first** — bottom nav bar navigation, 16px font-size inputs to avoid iOS zoom

---

## Architecture

The app follows a simple, deliberate **data → render → action** pattern:

```
State (in-memory arrays)
    ↓  saved to
localStorage
    ↓  read by
renderX()  →  injects HTML via innerHTML
    ↑
addX() / rm()  ←  user events (onclick)
```

There's no two-way binding, virtual DOM, or external state management. Every data change directly calls the corresponding render function.

---

## How to use

### Option 1 — Straight in the browser

```bash
# Clone the repository
git clone https://github.com/Pontxs/platoon-control.git

# Open the file
open index.html
```

### Option 2 — Deploy as a PWA (recommended)

1. Upload `index.html` to any static host (Netlify, GitHub Pages, Vercel)
2. Access it from your phone
3. **Android:** Chrome shows an automatic install banner
4. **iOS:** Safari → Share → "Add to Home Screen"

Once installed, it works **offline** and data stays in the device's localStorage.

---

## File structure

```
index.html
├── <head>
│   ├── PWA meta tags (viewport, theme-color, apple-mobile-web-app)
│   └── Google Fonts (Rajdhani, IBM Plex Mono, Inter)
│
├── <style>          Full CSS (~200 lines)
│   ├── Color variables (:root)
│   ├── Layout (header, bottom-nav, main)
│   ├── Components (card, form-grid, table, badge, toast)
│   └── Responsiveness (@media max-width: 480px)
│
├── <main>           7 pages as divs
│   ├── #page-dash   Dashboard with KPIs and rankings
│   ├── #page-cad    Personnel registry
│   ├── #page-at     Delays
│   ├── #page-pun    Punishments
│   ├── #page-disp   Medical leave and visits
│   ├── #page-dest   Performance notes (FO+ / FO−)
│   └── #page-aniv   Birthdays
│
├── <nav>            Bottom navigation bar (7 buttons)
│
└── <script>         Full logic (~300 lines)
    ├── Default data (seed arrays, fictional)
    ├── Persistence functions (ld / sv / svAll)
    ├── Helpers (fmt, daysUntil, nextId, toast)
    ├── Navigation (showPage, showTab)
    ├── Renders (renderDash, renderCad, renderAt...)
    ├── Actions (addCad, addAt, addPun, addDisp, addFO, rm)
    └── PWA setup (manifest, service worker, install banner)
```

---

## Design decisions

**Why single-file?** The app needs to work in military environments with unstable connectivity. A single HTML file is trivial to share via WhatsApp, USB drive, or QR code, with no install process and no npm dependency.

**Why no framework?** The project also serves as a hands-on exercise in JS and DOM fundamentals, alongside a Software Engineering degree. Frameworks would be an unnecessary layer of abstraction for this scope.

**Why localStorage instead of a database?** Zero infrastructure. The app is for the platoon commander's personal use — there's no need for sync across multiple users. For a multi-user scenario, the natural next step would be replacing localStorage with calls to a REST API backed by SQLite or PostgreSQL.

---

## Author

**Bruno Pontes da Rosa**

2nd Lieutenant, Brazilian Army

Software Engineering (PUCRS)

[![GitHub](https://img.shields.io/badge/GitHub-@Pontxs-181717?style=flat-square&logo=github)](https://github.com/Pontxs)

---

> _Built for real operational use. The seed data included in the repository is fictional and only serves to demonstrate the interface._
