# Account log

A one-page record of money taken out of an account: amount, date, and what it was for.
There's no login. The page runs on Sevalla's free static hosting and saves entries in a free Google Firestore database.

Use neutral names in every step below (for example `account-log`). The project ID is visible in the page's code and the site name can appear in its web address.

## 1. Create the database (Firebase)

1. Go to https://console.firebase.google.com and create a project. You don't need Google Analytics. Stay on the free Spark plan.
2. Open **Firestore Database** and create a database. Keep the default database ID, choose a US location, and start in **production mode**. The location can't be changed later.
3. Open the **Rules** tab, replace everything with the contents of `firestore.rules`, and click **Publish**.
4. Open **Project settings** (the gear icon), and under **Your apps** add a **Web** app. Don't turn on Firebase Hosting.
5. Copy `projectId` and `apiKey` from the settings it shows you.

## 2. Add the two values to the page

Near the top of the script in `index.html`, replace the placeholders:

```js
const PROJECT_ID = "PASTE_PROJECT_ID_HERE";
const API_KEY = "PASTE_API_KEY_HERE";
```

These values are designed to be public. `firestore.rules` is what controls access.

## 3. Publish on Sevalla

1. Push this folder to a GitHub repository.
2. In Sevalla, go to **Static sites** and add a site from that repository.
3. Leave the **Build command** empty and set the **Publish directory** to the repository root.
4. Deploy, then open the site and save a test entry.

Remove the test entry in the Firebase console under **Firestore Database**.

## Looking after it

- **Fix or remove an entry:** Firebase console > Firestore Database > `withdrawals`. `amountCents` is the amount in cents, so 12550 means $125.50.
- **Keep your own copy:** don't count on automatic backups on the free plan. Copy the list from the page into a spreadsheet now and then.
- **Who can see it:** anyone who has the link can read and add entries. Search engines are asked not to list it.
