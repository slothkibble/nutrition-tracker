NUTRITION & WEIGHT TRACKER — TURNING IT INTO A REAL ANDROID APP
==============================================================

What's in this folder
---------------------
index.html               The tracker itself (same one you already use,
                         now app-ready, with the saved-item recall built in)
manifest.webmanifest     The app's identity: name, icon, colors
sw.js                    The offline engine — caches the app on the phone
icons/                   App icons

This package becomes a real, installable Android app in 4 steps.
The only hands-on part happens on your laptop. Your logged data is NOT
part of this package and never leaves your phone (see the data note below).


STEP 1 — Put the app shell on the web (free, ~10 minutes)
---------------------------------------------------------
The app packager needs the tracker at a real web address first.
GitHub Pages gives you one for free:

  1. Go to github.com and sign up / sign in.
  2. Click "New repository". Name it:  nutrition-tracker
     Set it to Public, then "Create repository".
  3. On the repo page, click "uploading an existing file" and upload
     EVERYTHING in this folder, keeping the icons folder as a folder:
     index.html, manifest.webmanifest, sw.js, icons/ (all 3 icon files).
     (You can drag the files in; to keep the icons folder intact, use
     "Add file > Upload files" and drag the whole icons folder in too,
     or upload the three icons and rename them to icons/icon-192.png etc.
     if your browser flattens them.)
  4. Click "Commit changes".
  5. Go to Settings > Pages. Under "Build and deployment", choose
     "Deploy from a branch", branch: main, folder: / (root). Save.
  6. After a minute or two, your address appears on that Pages screen:
       https://YOUR-USERNAME.github.io/nutrition-tracker/
     Open that address on your phone to confirm the tracker loads.


STEP 2 — Package it as an Android app (pwabuilder.com)
------------------------------------------------------
On your laptop:

  1. Go to pwabuilder.com and enter your address from Step 1.
  2. Click through to "Package For Stores" and choose Android.
  3. Use the default options and click "Generate" / "Download".
     You get a zip containing the app files, including an .apk you can
     install directly and a signing key.
  4. KEEP THE SIGNING KEY FILE somewhere safe (it comes in the download).
     You need the same key to release updates later; it can't be recreated.


STEP 3 — Install on your Pixel
------------------------------
  1. Copy the .apk file to your phone (USB, or send it to yourself).
  2. Tap it and allow the install when Android asks (this is normal for
     apps installed outside the Play Store — it's your own app).
  3. Done: "Nutrition" is now in your app drawer with its own icon,
     opens full-screen, and works completely offline.


STEP 4 — Full-screen polish (optional, 2 minutes)
-------------------------------------------------
So the app opens with no browser address bar, Android checks one small
file on your site. PWABuilder includes the contents (asset links) in
your Step 2 download / instructions:

  1. In your GitHub repo, add an empty file named exactly:  .nojekyll
     (Add file > Create new file). This tells GitHub Pages to serve
     the next step's folder as-is.
  2. Create a folder named:  .well-known
     and inside it a file named:  assetlinks.json
     with the contents PWABuilder gave you.
  3. Wait a few minutes, then reinstall or reopen the app. Without this
     step the app still works fine — it just shows a small address bar.


DATA NOTE — carrying your logs over
-----------------------------------
Your entries live on your phone, in the tracker's own storage, so they
don't travel with this package. To move them into the app:

  1. In your current tracker file, open the Backup tab > Export.
  2. Once the app is installed, open it, Backup tab > Import, and pick
     that exported file.
  3. Going forward, the app keeps everything on the phone, same as now.


UPDATES
-------
If we change the tracker later, I give you a fresh index.html, you
re-upload it to the same GitHub repo (replacing the old one), and the
installed app picks it up automatically — no reinstall needed.


FOOD LIBRARY (new)
------------------
The tracker now has a "Foods" tab. Add a food or meal there once —
name, food/drink type, quantity, and all its nutrients — and it stays
in your personal food library on the device.

On the Daily Log, the "Add entry" form has a "From food library"
dropdown above the Name field. Pick a saved food and the whole form
fills in instantly: name, quantity, type, and every nutrient field.
The old type-to-recall from past logs still works the same way.

Saved foods are included in Backup exports and imports, and old
backup files (from before the library existed) still import cleanly.


CALORIES + FIBER (new)
----------------------
Calories (kcal) and Fiber (g) are now first-class fields. They appear in
the Daily Log entry form, in each entry's macro line
("605 kcal  ·  P 55g  ·  C 66g  ·  F 19.4g"), in the daily totals strip,
and in the Foods tab library form and rows. Older backups and older
entries without these fields simply show 0 until edited. Exports now
carry "version": 2.


SPREADSHEET IMPORT — your old data is ready to load
---------------------------------------------------
The file nutrition-tracker-spreadsheet-import.json (in the same folder as
this package) was converted from your old nutrition spreadsheet. It holds:

  - 33 entries (25 food + 8 water) for 2026-08-31 through 2026-09-03,
    with the calories, protein, fiber, fat, and carbs as recorded there
  - 35 food-library items converted from the Food Database sheet
  - 4 weigh-ins (243.6, 242.7, 240, 238 lb) from the Weight Tracker sheet

The spreadsheet's Notes column was not carried over (the app has no
per-entry notes field), and the Daily Summary / Weekly / Monthly
Dashboard sheets were computed rollups, so they were skipped.

To load it: open the tracker, go to the Backup tab, use "Import data
from a JSON file", pick nutrition-tracker-spreadsheet-import.json, then
choose Merge. Merge never duplicates — importing the same file twice
adds nothing new.
