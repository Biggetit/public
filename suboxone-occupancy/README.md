# Taper Tracker

A single-file web app that estimates buprenorphine (Suboxone) mu-opioid receptor occupancy from your dose history and shows it live.

> This is an estimate to help you see your progress. It is not medical advice. Make dose changes with your prescriber.

## Getting started (no GitHub experience needed)

You don't need an account, any installs or any coding. The whole app is one file, `index.html`, that runs in your web browser. Pick the option that fits how you want to use it.

### Option 1: Download it to your computer

1. **Download the app.** Use either link:
   - **[⬇ Download Taper Tracker (ZIP file)](https://github.com/Biggetit/public/archive/refs/heads/claude/suboxone-occupancy-timer-sds4cl.zip)**: downloads right away. Unzip it (on Linux or Windows, right-click it and choose **Extract**; on a Mac, double-click it), then open the `suboxone-occupancy` folder inside. The app is `index.html`.
   - **[⬇ Download just the app file (index.html)](https://raw.githubusercontent.com/Biggetit/public/claude/suboxone-occupancy-timer-sds4cl/suboxone-occupancy/index.html)**: **right-click** the link and choose **Save link as…** (on a phone, long-press it and choose **Download link**). If you click it normally, your browser shows the page's code instead. That's expected: go back and use Save link as.
2. **Move it to a permanent folder.** For example, make a folder called `Taper Tracker` in `Documents` and put `index.html` there. Don't leave it in Downloads, where it's easy to delete by accident.
3. **Open it.** Double-click `index.html`. It opens in your default browser (Firefox, Chrome, Edge or Safari).
4. **Bookmark it** (Ctrl+D, or ⌘+D on a Mac) so you always open the same copy.

### Option 2: Put it online for free with GitHub Pages (works on phones)

Use this to open the tracker on your phone, or to get a normal web address. It needs a free [GitHub account](https://github.com/signup).

1. **[Fork this repository](https://github.com/Biggetit/public/fork)** to make your own copy, then click **Create fork**.
2. In your copy, go to **Settings → Pages**.
3. Under **Build and deployment**, set **Source** to **Deploy from a branch**. Choose the branch that has the `suboxone-occupancy` folder, choose the **/ (root)** folder, and click **Save**.
4. Wait a minute or two, then refresh the page. GitHub shows your site's address. Add `suboxone-occupancy/` to the end, for example:
   `https://YOUR-USERNAME.github.io/public/suboxone-occupancy/`
5. Open that address on your phone and add it to your home screen:
   - **Android (Chrome):** tap **⋮**, then **Add to Home screen**.
   - **iPhone (Safari):** tap **Share**, then **Add to Home Screen**.

Your dose history is never uploaded to GitHub. Each person's data stays in their own browser, even on a public site.

## Keeping your data when the app is closed

The tracker saves every change automatically in your browser's storage. When you close it and open it again, your doses and check-ins are still there, as long as you follow these rules:

- **Use the same browser every time.** Data saved in Firefox doesn't show up in Chrome, and data on your laptop doesn't show up on your phone.
- **Open the same copy.** Use your bookmark or home screen icon. If you move, rename or re-download `index.html`, the browser may treat it as a new app and show it empty. (Option 2 doesn't have this problem, because the web address stays the same.)
- **Don't use a private or incognito window.** Those forget everything when you close them.
- **Don't clear your browser's site data.** Clearing "cookies and site data" or "browsing data" erases the tracker's history too. Some cleanup apps and phone storage cleaners do this on their own.

### Back up your history

Even with those rules, keep a backup. It takes 10 seconds:

1. Scroll to the bottom of the app and open **Back up or move your data**.
2. Tap **Show my backup**, then **Copy**.
3. Paste the text somewhere safe, like a note, an email to yourself, or a Notion or Google Docs page.

To restore it, or to move your history to another browser or device, paste that text into the same box and tap **Restore from text**.

## First steps in the app

1. The app opens with a made-up **example history** so you can see how it works. Tap **Clear example**.
2. Enter your past doses under **Add doses**. **Daily dose range** is the fastest way to enter weeks of the same dose.
3. If you have a taper schedule, add it under **Taper plan**. Future doses show as a dashed line.
4. Log how you feel once or twice a day under **How are you feeling?**
5. Open **Help: what the terms mean** at the top of the app for an explanation of every label.

---

## Technical notes

- [`index.html`](https://raw.githubusercontent.com/Biggetit/public/claude/suboxone-occupancy-timer-sds4cl/suboxone-occupancy/index.html): the complete page, ready to open.
- `app.html`: the same page without the outer HTML wrapper (the version used for the hosted Claude page).

### What it shows
- Current estimated occupancy, updated every second, with a trend arrow (rising, steady or falling), time since your last dose, a countdown to the next milestone, and the expected peak from your latest dose.
- A curve of past doses (solid) and planned doses (dashed).
- The dates occupancy should drop below 80/70/…/1%, both if you follow your plan and if you stop now.
- Steady-state occupancy for common daily doses.
- Daily symptom check-ins (0–10 plus common withdrawal symptoms), plotted on the curve and averaged by occupancy band so you can see where your own symptoms start.

### Model
Each dose is absorbed and eliminated with one compartment (absorption ~1.2/h, half-life 37 h by default). The doses are summed, then put through a saturating curve: occupancy = Omax · A / (A + EC50). Defaults (Omax 95%, EC50 7 mg-eq) match PET results from Greenwald et al.: about 41%, 80%, and 84–88% occupancy at 2, 16, and 32 mg/day.

### Where data is saved
- Opened as a Claude artifact while signed in: a private per-user area of the artifact's database (`data/users/<id>/tracker` and `/checkins`), synced across devices.
- Opened as a plain file: that browser's localStorage only. Use the backup section to copy your data out.
