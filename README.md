# IRON — Gym Tracker (PWA + Google Sheets Backend)

A mobile-first fitness tracker for muscle gain. Stores everything in **your own Google Sheet** via Google Apps Script. 100% free to deploy. Installable as a real app on your phone.

---

## Files in this project

| File | Purpose |
|---|---|
| `Code.gs` | Google Apps Script backend (paste into script.google.com) |
| `index.html` | The PWA frontend — single file, no build step |
| `manifest.json` | PWA manifest (makes it installable) |
| `sw.js` | Service worker (offline support) |
| `icon-192.png`, `icon-512.png` | App icons |

---

## Part 1 — Set up the backend (Google Apps Script + Sheet)

This takes ~5 minutes.

1. **Create the script project**
   - Go to <https://script.google.com> → click **New project**
   - Delete the default `function myFunction() {}` code
   - Open `Code.gs` from this folder, copy ALL its contents, paste into the editor
   - Click the floppy-disk **Save** icon (or Ctrl/Cmd-S). Name it `IRON Backend`.

2. **Initialize the sheet**
   - At the top of the editor, in the function dropdown next to ▶ Run, select `setupSheet`
   - Click **▶ Run**
   - Google will ask for permissions — click **Review permissions** → choose your account → **Advanced** → **Go to IRON Backend (unsafe)** → **Allow**. (It says "unsafe" only because it's your own unverified script — it has no access outside your own Drive.)
   - You should see "Execution completed" in the log. A new Google Sheet named **IRON Gym Tracker** has been created in your Drive with three tabs: `DailyLogs`, `Profile`, `Workouts`.

3. **Deploy as a web app**
   - Click **Deploy** (top right) → **New deployment**
   - Click the gear ⚙ icon next to "Select type" → choose **Web app**
   - Fill in:
     - **Description:** `IRON v1`
     - **Execute as:** `Me (your@email)`
     - **Who has access:** `Anyone` (this is required so your phone can call it; nobody can guess the random URL)
   - Click **Deploy**
   - **Copy the Web app URL** that appears (looks like `https://script.google.com/macros/s/AKfy.../exec`)

> **If you ever update `Code.gs`:** click Deploy → Manage deployments → pencil ✏ → Version: New version → Deploy. The URL stays the same.

---

## Part 2 — Host the frontend (free)

Pick any one option:

### Option A — GitHub Pages (free, recommended)
1. Create a new GitHub repo (e.g. `iron-tracker`)
2. Upload `index.html`, `manifest.json`, `sw.js`, `icon-192.png`, `icon-512.png` to the repo root
3. Settings → Pages → Source: `main` branch → root → Save
4. Your app is live at `https://YOUR-USERNAME.github.io/iron-tracker/`

### Option B — Netlify Drop (literally drag-and-drop, free)
1. Go to <https://app.netlify.com/drop>
2. Drag the entire `gym-tracker` folder onto the page
3. You get an instant URL like `https://amazing-iron-12345.netlify.app`

### Option C — Vercel (free)
1. Go to <https://vercel.com/new>, import or drag the folder
2. Deploy. Done.

### Option D — Local test
Just open `index.html` in your phone's browser via a local server. The simplest way:
```bash
cd gym-tracker
python3 -m http.server 8080
```
Then on your phone (same WiFi): `http://YOUR-COMPUTER-IP:8080`

---

## Part 3 — Connect the app

1. Open the deployed URL on your **phone**
2. The setup screen appears asking for the Web App URL
3. Paste the Apps Script URL from Part 1, step 3
4. Tap **Connect & Launch**

You're in. Your data lives in your Google Sheet.

---

## Part 4 — Install as a mobile app

### Android (Chrome)
- Tap the ⋮ menu → **Add to Home screen** → Install
- Or wait for the install prompt and tap "Install"

### iPhone (Safari)
- Tap the **Share** button (square with arrow)
- Scroll down → **Add to Home Screen**

The app now lives on your home screen with a real icon, opens fullscreen (no browser bar), and works offline for cached pages.

---

## Features

**Home dashboard**
- Calorie progress with target comparison & status badge
- Protein progress
- Today's planned workout with one-tap "Mark Done"
- Current weight + progress to 60 kg goal
- AI-style coach insights (rule-based) reacting to your data

**Track tab**
- Quick daily log: weight, workout, calories, protein, meals, sleep, notes
- Auto-saves to your Google Sheet
- Updates dashboard immediately

**Plan tab**
- Mon: Chest+Triceps · Tue: Back+Biceps · Wed: Legs · Thu: Shoulders · Fri: Full Body · Sat: Volleyball · Sun: Rest
- Visual completion status per day
- Full structured Indian diet plan (chana, oats, eggs, dal, paneer, etc.)

**Stats tab**
- 30-day weight trend (line chart)
- 30-day calorie & protein bars vs target
- Workout consistency %

**Profile tab**
- Edit targets (weight, calories, protein, weekly gain)
- Install to home screen shortcut
- Open Google Sheet shortcut

**Smart coaching rules built in:**
- Calories < 80% target → "Add a banana shake"
- Calories > 115% target → "Trim carbs"
- Protein low → "Add eggs/paneer/whey"
- Workout missed by 9 PM → "Reschedule"
- Weight gain too slow → "Add 200 kcal"
- Weight gain too fast → "Cut 200 kcal"
- Volleyball Saturday → carb-load reminder
- Sunday → recovery focus

---

## Troubleshooting

| Issue | Fix |
|---|---|
| "Save failed" in app | Apps Script URL wrong, or deployment access not set to "Anyone". Redo Part 1 step 3. |
| Sync pill says OFFLINE | App can't reach Apps Script. Check internet. The app keeps working with cached data. |
| Changes to `Code.gs` not reflected | You must redeploy: Deploy → Manage deployments → ✏ → Version: New → Deploy. |
| iOS doesn't show install prompt | Use Safari → Share → Add to Home Screen. iOS doesn't auto-prompt. |
| Want to start over | Profile tab → "Reset Connection". Or delete the IRON Gym Tracker sheet from Drive. |

---

## Privacy

- Your data lives in **your** Google Sheet, in **your** Drive.
- The Apps Script runs as you, so only you can read/write the sheet.
- The "Anyone" access on the web app means anyone with the URL can post data to your sheet — but the URL is a long random string, treat it like a password. Don't share it publicly.
- The frontend is static HTML; nothing is sent to any server other than your own Apps Script.

---

Built for one purpose: get to 60 kg. Lift heavy, eat consistent, log daily. 🏋️
