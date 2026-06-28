# Setting up Reading Block (one time, ~5 minutes)

This guide gets the extension running in Chrome and connected to your Google
Calendar. You only do this once. Follow it top to bottom.

There are two halves:
- **Part A** loads the extension into Chrome.
- **Part B** gives it permission to use your Google Calendar.

We do Part A first because Part B needs a code (the "Extension ID") that only
appears after Part A.

---

## Part A: Load the extension into Chrome

1. Download this project to your computer (if you cloned or unzipped it, just
   remember where the folder is).
2. Open Chrome. In the address bar type `chrome://extensions` and press Enter.
3. Top-right of that page, turn **Developer mode** ON.
4. Click **Load unpacked** (top-left).
5. In the file picker, select **this project's folder** (the one containing
   `manifest.json`), then click Select.
6. A card titled **Reading Block** appears.
7. On that card, find **ID:** followed by a long string of letters. **Copy that
   whole ID and keep it handy.** You'll need it in Part B.

> Keep the project folder where it is. Chrome ties the Extension ID to the
> folder's location, so if you move the folder later, the ID changes and you'd
> have to redo Part B.

If the icon is hidden, click the puzzle-piece icon in Chrome's toolbar and pin
"Reading Block".

---

## Part B: Give it permission to use Google Calendar

Google requires every app to register before it can touch your calendar. It's
free. You'll create a "project," switch on the Calendar feature, and generate a
login ID that you paste into the extension.

### B1. Create a Google Cloud project
1. Go to **https://console.cloud.google.com** and sign in.
2. At the top, click the project dropdown, then **New Project**. Name it
   `Reading Block` and click **Create**. Make sure it's the selected project.

### B2. Turn on the Calendar API
1. In the top search bar, type **Google Calendar API** and click it.
2. Click **Enable**.

### B3. Set up the consent screen
1. Left menu → **APIs & Services** → **OAuth consent screen** (in newer consoles
   this may appear as **Google Auth Platform** → **Audience**).
2. Choose **External**, click **Create**.
3. Fill in the required fields (app name `Reading Block`, your email for the
   support and developer contact fields). Save and continue through the next
   screens; you can skip "Scopes" and "Optional info."
4. On **Test users**, click **Add Users** and add your own Google email address,
   then Save. (While the app is in "Testing" mode, only the test users you list
   can use it. That's fine, it's just you.)

### B4. Create the login ID (the "OAuth client")
1. Left menu → **APIs & Services** → **Credentials**.
2. Click **+ Create Credentials** → **OAuth client ID**.
3. **Application type:** choose **Chrome Extension** (older consoles call this
   **Chrome App**).
4. Name it `Reading Block`.
5. In the **Item ID / Application ID** field, paste the **Extension ID** you
   copied in Part A, step 7.
6. Click **Create** and copy the **Client ID** (it ends in
   `.apps.googleusercontent.com`).

### B5. Put the Client ID into the extension
1. Open `manifest.json` in this project folder with any text editor.
2. Find `PASTE_YOUR_GOOGLE_CLIENT_ID_HERE.apps.googleusercontent.com`.
3. Replace that whole placeholder (keep the quotes) with your Client ID. Save.

### B6. Reload the extension
1. Back on `chrome://extensions`, click the circular **reload** arrow on the
   Reading Block card.

---

## Part C: First use

1. Open five articles and **left-click the Reading Block icon once** on each. A
   small "Saved" confirmation appears in the corner each time.
2. On the fifth save, Google asks permission to add events to your calendar.
   Because this is your own personal, unpublished app, it may warn that the app
   is "unverified." That's expected: click **Advanced**, then **Go to Reading
   Block (unsafe)**, then **Allow**.
3. Done. A 30-minute reading block appears on the next free day in your chosen
   window, with the five links in the event notes.

---

## If something goes wrong
- **"Access blocked ... has not completed the Google verification process"
  (Error 403: access_denied):** your Google account isn't on the tester list. Go
  to the Google Cloud Console → APIs & Services → OAuth consent screen (or Google
  Auth Platform → Audience) → Test users → Add users → add your own email → Save.
  Wait a minute and try again.
- **Consent never appears / "bad client id":** the Client ID in `manifest.json`
  doesn't match, or the Extension ID in the OAuth client is wrong. Re-check Part A
  step 7 and Part B steps 4–5, then reload.
- **"No free slot found":** your chosen window had no meeting-free block on a free
  day in the lookahead period. Widen the window or days in Settings.
- **Nothing happens on the 5th save:** open `chrome://extensions`, click "service
  worker" under the Reading Block card to see logs.
