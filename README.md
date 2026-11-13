# Ignite website

The website for the Ignite young adults ministry. Members sign in (Google or an emailed link) to see the calendar, RSVP and sign up to help. The "New here?" welcome stays public so newcomers can read it first. Leaders get a Leaders tab to edit everything.

- **Upcoming / Month**: the calendar (nights, leaders, passages, times, locations), RSVPs (Going / Maybe / Can't go, plus guests) and helper roles (Setup, Snacks…) with spot limits
- **Your plans**: each member sees what they've said yes to
- **New here?**: what Ignite is, basic info, leaders and contacts (link straight to it with `#new-here`)
- **Leaders** (leaders only): fill gaps, see RSVP and helper counts, copy RSVP lists, leader-only notes, manage leader accounts, see everyone who's signed up

Files:
- `index.html`: the whole site
- `firebase-config.js`: your Firebase settings (fill this in once)
- `firestore.rules`: security rules (who can read and edit what)

## One-time setup (about 20 minutes)

### 1. Create the database (Firebase, free)
1. Go to https://console.firebase.google.com and click **Create a project**. Name it `ignite`. You can turn Google Analytics off.
2. In the left menu, open **Build → Firestore Database → Create database**. Pick a location near you (for example `us-west1`), choose **production mode**, and finish.
3. Open the **Rules** tab, delete what's there, paste everything from `firestore.rules`, and click **Publish**.
4. Open **Build → Authentication → Get started**. Under Sign-in method, click **Google**, turn it on, choose your email as the support email, and **Save**.
5. Still under Sign-in method, click **Add new provider → Email/Password**. Turn on **Email link (passwordless sign-in)** (you can leave plain Email/Password off) and **Save**. This lets people without a Google account sign in with a link sent to their email.

### 2. Make yourself the first leader
1. Go back to **Firestore Database → Data** and click **Start collection**.
2. Collection ID: `leaders`
3. Document ID: the email you'll sign in with, all lowercase (for example `you@gmail.com`)
4. Add two fields:
   - `name` (string): your name
   - `owner` (boolean): `true`
5. Save. You can add every other leader from the site itself later.

### 3. Connect the site to the database
1. Click the gear icon → **Project settings**. Under **Your apps**, click the web icon `</>`.
2. Name it `ignite-site` and register it (skip Firebase Hosting).
3. Copy the values from the `firebaseConfig` it shows into `firebase-config.js`, replacing each `PASTE_...`.

### 4. Put it online (GitHub Pages, free)
1. On GitHub, create a new **public** repository named `ignite`.
2. Click **Add file → Upload files** and upload all the files in this folder. Commit.
3. Open the repo's **Settings → Pages**. Under Build and deployment, choose **Deploy from a branch**, branch `main`, folder `/ (root)`, and **Save**.
4. After a minute your site is live at `https://YOUR-USERNAME.github.io/ignite/`.

### 5. Allow sign-in on your site's address
1. In Firebase, open **Authentication → Settings → Authorized domains → Add domain**.
2. Add `YOUR-USERNAME.github.io`.

### 6. Try it
1. Open your site and sign in with the account you added in step 2.
2. Add your name when it asks. The **Leaders** tab appears. Add other leaders there by the email they sign in with.
3. Open **New here?** and tap **Edit this page** to fill in the welcome info and leader contacts.

## Good to know
- Public (no sign-in): the New here welcome, leader names, roles and bios.
- Signed-in members: the calendar, who's going, helper sign-ups, leader phone numbers and emails.
- Leaders only: leader notes, the leader account list, the member list.
- Each member can only change their own RSVP. Leaders can change anything.
- Sign-in emails come from Firebase and may land in spam the first time. Tell people to check there.
- The owner (you) can't be removed from the site. To change the owner, edit the `leaders` collection in the Firebase console.
- The free Firebase plan covers far more traffic than a church group needs.
