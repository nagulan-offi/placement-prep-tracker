# PrepTrack — Placement Preparation Tracker

<div align="center">

![PrepTrack](https://img.shields.io/badge/PrepTrack-Placement%202026-6C7FFF?style=for-the-badge&logo=firebase&logoColor=white)
![Status](https://img.shields.io/badge/Status-Live-00E887?style=for-the-badge)
![Firebase](https://img.shields.io/badge/Firebase-Firestore-FFB830?style=for-the-badge&logo=firebase&logoColor=black)
![Hosted](https://img.shields.io/badge/Hosted-Firebase%20Hosting-FF6B6B?style=for-the-badge&logo=firebase)

**A full-stack personal placement preparation tracker — built to track DSA, LeetCode, Apna College modules, CS fundamentals, and daily routines across all devices in real time.**

### [Live App](https://prep-tracker-2026-d315e.web.app)

</div>

---

## Why I Built This

I am a 3rd year CS student targeting placements in August 2026. I needed a system to track:
- Daily preparation across a 3-hour commute + night coding schedule
- Apna College DSA course progress (52 modules, starting from Module 19)
- LeetCode problems solved with difficulty and topic tagging
- CS fundamentals study — DBMS, OS, Networks, OOPs
- Full calendar history showing every day I studied

No existing app matched my exact schedule and roadmap. So I built one — with a real database that syncs across my phone on the morning bus and my laptop at night.

---

## Tech Stack

| Layer | Technology | Purpose |
|-------|-----------|---------|
| Frontend | HTML + CSS + Vanilla JS | Single file, no build tools, instant deploy |
| Auth | Firebase Authentication | Email/password login with secure JWT tokens |
| Database | Cloud Firestore | Real-time sync across all devices |
| Hosting | Firebase Hosting | Free global CDN, custom domain ready |

**Zero frameworks. Zero npm dependencies. One HTML file. 74KB total.**

---

## Features

**Daily Tracker**
- Time-slot schedule matching my real day: morning bus, college, evening bus, internship, night coding
- Every task stored by actual date — Week 1 data never overwrites Week 2
- Add, edit, delete, reorder tasks in any slot
- Per-day notes field

**LeetCode Log**
- Log every problem: name, difficulty, topic
- Filter by Easy / Medium / Hard / solved / unsolved
- Running totals updating in real time

**Apna College Module Tracker**
- All 34 modules (19–52) with critical / important / skim labels
- Mark modules complete, navigate forward and back
- Overall progress bar

**Calendar History**
- Full monthly calendar with colour-coded study history
- Green = all tasks done, Amber = partial, Empty = not started
- Click any past date to see exactly what you did

**Streak System**
- Current streak and all-time best streak
- Calculated from real Firestore history across all devices

**Cross-Device Sync**
- Tick a task on phone — shows done on laptop instantly
- Same data everywhere, same account

---

## Architecture

```
Browser (any device)
    |
    |-- Firebase Auth SDK       (verifies user on every request)
    |-- Firestore SDK           (reads and writes user data)
    |-- Firebase Hosting        (serves the HTML globally)

Firestore data structure:
users/
  {userId}/
    tasks/{dateKey}       -- task completion per day
    notes/{dateKey}       -- day notes
    lc/{problemId}        -- LeetCode problems
    modules/progress      -- current module + done state
    slots/{type}          -- customised task templates
    slotOpen/{key}        -- slot open state per day
```

---

## Security Rules

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /users/{userId}/{document=**} {
      allow read, write: if request.auth != null
        && request.auth.uid == userId;
    }
  }
}
```

Every user can only access their own data. Unauthenticated requests are rejected at the database level before reaching any document.

---

## Run Your Own Instance

```bash
git clone https://github.com/yourusername/prep-tracker.git
cd prep-tracker

# No build step — open directly
open public/index.html
```

To deploy:
1. Create Firebase project at console.firebase.google.com
2. Enable Email/Password Authentication
3. Create Firestore database
4. Replace `firebaseConfig` in `index.html` with your config
5. `firebase deploy`

---

## My Placement Roadmap

| Phase | Timeline | Focus |
|-------|----------|-------|
| Phase 1 | March – July 2026 | DSA 250 problems + CS Fundamentals + 2 Projects |
| On-Campus | August 2026 | TCS, Infosys, LTIMindtree, Hexaware |
| Phase 2 | Sep – Dec 2026 | Docker, Terraform, Kubernetes, AWS SAA, CI/CD, MLOps |
| Off-Campus | Jan – Mar 2027 | Product companies, 10–18 LPA target |

---

## Future Plans

- [ ] Weekly progress chart — problems solved per week graph
- [ ] Export monthly report as PDF
- [ ] Daily reminder push notifications
- [ ] GitHub contribution-style yearly heatmap

---

<div align="center">
<sub>Built by Nagulan | 3rd Year CS | Graduating 2027 | Cloud + AI/ML</sub>
</div>
