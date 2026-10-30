# hartwick.tech

The website for Hartwick Technologies. It's a plain HTML site hosted free on GitHub Pages, with no build step and nothing to install.

## What's in this folder

| File | What it does |
|---|---|
| `index.html` | The whole site: content, styles and a tiny script |
| `404.html` | The page people see if they follow a broken link |
| `favicon.svg`, `apple-touch-icon.png` | The little "H" icon in browser tabs and on phone home screens |
| `og-image.png` | The preview image when someone shares the link on LinkedIn, Slack or iMessage |
| `CNAME` | Tells GitHub Pages the site lives at hartwick.tech |
| `robots.txt`, `sitemap.xml` | Help Google find and index the site |
| `.nojekyll` | Tells GitHub to serve the files as they are |

---

## One-time setup (about 30 minutes, plus waiting for DNS)

### 1. Create the repository
1. Go to https://github.com/new while signed in as **amandahartwick**.
2. Repository name: **`amandahartwick.github.io`** (exactly that).
3. Set it to **Public**. On a free GitHub account, Pages only works on public repositories, and the site is public anyway.
4. Don't add a README, .gitignore or license. Click **Create repository**.

### 2. Put the files in it
Either:
- **Ask Claude to push them** (it can once the repo exists), or
- Do it yourself: on the new repo's page, click **uploading an existing file**, drag in every file from this folder (including `.nojekyll` and `CNAME`), and click **Commit changes**.

### 3. Turn on GitHub Pages
1. In the repo, go to **Settings → Pages**.
2. Under **Build and deployment**, set Source to **Deploy from a branch**, Branch to **main** and folder to **/ (root)**. Click **Save**.
3. In a minute or two the site is live at https://amandahartwick.github.io.

### 4. Connect hartwick.tech
GitHub says to add the domain in GitHub **before** changing DNS.

1. Still in **Settings → Pages**, under **Custom domain**, type `hartwick.tech` and click **Save**.
2. **Verify the domain (recommended).** This stops anyone else from claiming your domain on GitHub. Click your profile photo → **Settings → Pages → Add a domain**, enter `hartwick.tech`, and GitHub shows you a TXT record to add. It looks like:
   - Type **TXT**, Host/Name **`_github-pages-challenge-amandahartwick`**, Value: the code GitHub shows you
   - Keep this record in place permanently.
3. **Add the DNS records in Namecheap** (hartwick.tech is registered there):
   1. Sign in at namecheap.com → **Domain List** → click **Manage** next to hartwick.tech.
   2. On the **Domain** tab, check that **Nameservers** says **Namecheap BasicDNS**. If it says something else, stop and ask Claude, because the records then go somewhere else.
   3. Open the **Advanced DNS** tab. Under **Host Records**, **delete** these if you see them (they're Namecheap's "parked domain" placeholders, and they block the site):
      - **CNAME Record**, host `www`, value `parkingpage.namecheap.com.`
      - **URL Redirect Record**, host `@`
      - Any other **A Record** or **CNAME Record** on host `@` or `www`
   4. Click **Add New Record** for each row in the table below. Leave TTL on **Automatic**. Namecheap doesn't need a dot at the end of the CNAME value.
   5. Click the green checkmark on each row (or **Save All Changes**).
   6. **Don't change the Mail Settings section** further down the Advanced DNS page, or any **TXT** records that mention Google or `v=spf1`. Those run your amanda@hartwick.tech email.

| Type | Host / Name | Value |
|---|---|---|
| A | `@` | `185.199.108.153` |
| A | `@` | `185.199.109.153` |
| A | `@` | `185.199.110.153` |
| A | `@` | `185.199.111.153` |
| AAAA | `@` | `2606:50c0:8000::153` |
| AAAA | `@` | `2606:50c0:8001::153` |
| AAAA | `@` | `2606:50c0:8002::153` |
| AAAA | `@` | `2606:50c0:8003::153` |
| CNAME | `www` | `amandahartwick.github.io` |

> ⚠️ **Don't touch your email records.** Leave the Mail Settings (MX) and the Google-related **TXT** records alone. They make amanda@hartwick.tech work. The only things to delete are the parking-page records listed above.

In Namecheap, the GitHub verification TXT record from step 2 goes in as: Type **TXT Record**, Host **`_github-pages-challenge-amandahartwick`** (Namecheap adds `.hartwick.tech` for you), Value: the code GitHub shows.

4. Wait. DNS changes usually show up within an hour but can take up to a day or two.
5. Back in **Settings → Pages**, once the DNS check passes, tick **Enforce HTTPS**. (The checkbox stays greyed out until GitHub has issued the certificate, which can take up to an hour.)
6. Visit https://hartwick.tech and https://www.hartwick.tech. Both should show the site.

### 5. Turn on the "Book a call" buttons
Until you do this, those buttons open an email to you, so nothing is broken in the meantime.

1. In Google Calendar (signed in as amanda@hartwick.tech), click **Create → Appointment schedule**.
2. Title: *Intro call with Amanda Hartwick*. Length: **20 minutes**. Set your available hours, choose **Google Meet**, and add a buffer between meetings if you like. Click **Save**.
3. Click **Share** (or **Open booking page**) and copy the booking page link.
4. Open `index.html` on GitHub, click the pencil icon, search for `BOOKING_URL`, paste the link between the quotes, and click **Commit changes**:
   ```js
   const BOOKING_URL = "https://calendar.app.google/your-link-here";
   ```

---

## Changing the site later
- **Small text edits:** open `index.html` on GitHub, click the pencil icon, edit, and **Commit changes**. The live site updates within a minute or two.
- **Prices** are in the "What I do" section. Search for `class="price"`.
- **Bigger changes:** ask Claude, and it can update the file and push it.
