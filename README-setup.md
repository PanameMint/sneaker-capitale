# Sneaker Capitale admin — setup

## 1. Deploy the theme changes
Unzip this into your repo root, keeping the folder structure:
- `_layouts/post.html` (replaces existing)
- `_layouts/home.html` (replaces existing)
- `_includes/buy-sidebar.html` (new)
- Append `assets/css/style-additions.css` onto the end of your existing `assets/css/style.css`, then delete the standalone file

Commit and push to `main`. GitHub Pages rebuilds automatically. Existing posts are unaffected — the new gallery/sidebar only render when a post's front matter includes `gallery` or `buy_links`.

## 2. Decide where the admin panel lives — this is the important security choice

**Recommended: keep `admin/` off the public site entirely.** Your repo has to stay public for free GitHub Pages hosting, so anything you publish under it is technically reachable by anyone with the URL. The admin panel doesn't expose anything dangerous on its own (it's just a form — nothing works without your GitHub token), but there's no reason to make it discoverable.

Two ways to do that:

**Option A — run it locally (simplest, no exposure at all)**
Don't commit `admin/` to the repo. Just keep `admin/index.html` on your own computer and open it directly in a browser (double-click it, or drag it into a browser tab). It talks straight to the GitHub API regardless of where it's opened from.

**Option B — keep it in the repo but excluded from the built site**
Add this to `_config.yml`:
```yaml
exclude:
  - admin/
```
Jekyll won't copy it into the published `_site`, so it never becomes a live URL — it just sits as source in the repo for you to download and run locally when needed.

If you ever do want it reachable as a live URL (e.g. to publish from your phone without syncing a file), skip the exclude and use the passphrase lock below — just know that's a UX speed bump, not a real barrier, since the page's own source is visible to anyone who looks.

## 3. Set your passphrase lock (only matters if you're hosting the page publicly)
Open `admin/index.html` in a browser, open devtools console (F12), and run:
```js
crypto.subtle.digest('SHA-256', new TextEncoder().encode('your-passphrase')).then(b => console.log(Array.from(new Uint8Array(b)).map(x => x.toString(16).padStart(2,'0')).join('')))
```
Copy the printed hash, then in `admin/index.html` find:
```js
const PASSPHRASE_HASH = 'REPLACE_WITH_YOUR_OWN_SHA256_HASH';
```
and paste your hash in. Your actual passphrase never has to leave your own browser — I never see it, and it isn't stored anywhere as plain text.

## 4. Generate your GitHub token
Go to github.com/settings/tokens → Fine-grained tokens → Generate new token.
- **Repository access**: only `sneaker-capitale`, nothing else
- **Permissions**: Contents → Read and write. Leave everything else as No access.
- **Expiration**: set a real date (e.g. 90 days), not "no expiration" — you'll get a reminder to rotate it
- Treat this token like a password: don't paste it anywhere except the admin panel's Settings tab, don't screenshot it, don't commit it to the repo

The token is what actually protects your site — it's tied to your GitHub account, so the real question is "who can generate a valid token for this repo," which comes down to:
- **Turn on two-factor authentication** on your GitHub account (Settings → Password and authentication) — this is the single biggest thing standing between "someone gets my password" and "someone owns my site"
- Don't add collaborators to the repo unless you mean to
- If you ever suspect a token leaked, revoke it immediately from the tokens page — a revoked token stops working instantly, even if someone has it saved

## 5. Using it day to day
Open the admin panel (locally, or wherever you decided to host it), unlock with your passphrase if you set one, go to Settings and paste your token in once — it's saved in that browser's local storage so you won't need to re-enter it each time (until you disconnect or clear browser data). Then New post / Manage posts work as normal.
