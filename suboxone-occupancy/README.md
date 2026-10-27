# Taper Tracker

A single-file web app that estimates buprenorphine (Suboxone) mu-opioid receptor occupancy from your dose history and shows it live.

- `index.html`: open it in any browser (no install, works offline after the fonts load once).
- `app.html`: the same page without the HTML wrapper (the version used for the hosted page).

## What it shows
- Current estimated occupancy, updated every second, plus time since your last dose and a countdown to the next milestone.
- A curve of past doses (solid) and planned doses (dashed).
- The dates occupancy should drop below 80/70/…/1%, both if you follow your plan and if you stop now.
- Steady-state occupancy for common daily doses.
- Daily symptom check-ins (0–10 plus common withdrawal symptoms), plotted on the curve and averaged by occupancy band so you can see where your own symptoms start.

## Model
Each dose is absorbed and eliminated with one compartment (absorption ~1.2/h, half-life 37 h by default). The doses are summed, then put through a saturating curve: occupancy = Omax · A / (A + EC50). Defaults (Omax 95%, EC50 7 mg-eq) match PET results from Greenwald et al.: about 41%, 80%, and 84–88% occupancy at 2, 16, and 32 mg/day.

This is an estimate for motivation only, not medical advice.

## Where data is saved
- Opened as a Claude artifact while signed in: a private per-user area of the artifact's database (`data/users/<id>/tracker` and `/checkins`), synced across devices.
- Opened as a plain file: that browser's localStorage only. Use the backup section to copy your data out.
