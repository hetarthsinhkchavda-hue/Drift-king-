# Drift King - GitHub setup (sign in with Google or email, unique driver names)

## 1. Make a free Firebase project
1. Go to https://console.firebase.google.com and click **Add project**. Name it, for example, drift-king. You can turn Google Analytics off.
2. Open **Build > Authentication > Get started > Sign-in method**.
   - Turn on **Google** (pick your support email) and save.
   - Turn on **Email/Password** and save.
3. Open **Build > Firestore Database > Create database**. Choose **Production mode** and the location closest to your players.
4. In Firestore, open the **Rules** tab. Delete everything, paste the contents of `firestore.rules`, and press **Publish**.

## 2. Connect the game
1. In Firebase, open **Project settings (gear icon) > Your apps > Web (</>)**. Give it any name and register it.
2. Copy the config values shown (apiKey, authDomain, projectId, appId).
3. Open `index.html` in any text editor. Search for `PASTE_API_KEY`. Replace the four `PASTE_...` values in `FB_CONFIG` with your own.
   (This key is meant to be public. The rules in step 1.4 are what protect your data.)

## 3. Put it on GitHub
1. Create a new public repository on github.com.
2. Upload `index.html` (and `firestore.rules` if you like).
3. Open **Settings > Pages**. Under Branch choose **main** and **/ (root)**, then Save. After a minute your game is live at `https://YOURNAME.github.io/REPO-NAME/`.

## 4. Allow your website to sign in
In Firebase open **Authentication > Settings > Authorized domains > Add domain** and add `YOURNAME.github.io`.

## 5. Test
Open your link. You should see Sign up > Google or email > Profile (driver name) > the home screen. Try the same driver name in two different accounts. The second one must be refused.

## How it works
- Flow: Sign up (Google or email) > Submit > Profile page > Driver name.
- Driver names are unique. "Max Verstappen" and "max_verstappen" count as the same name.
- Best lap times are saved to the `scores` collection (one per player per map) when a player beats their record. A leaderboard screen is the next step.
- If `FB_CONFIG` is left as PASTE_..., the game still runs without sign-in, for testing.
