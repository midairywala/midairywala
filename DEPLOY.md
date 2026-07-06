# Deploying midairywala.com to Vercel

Your site is now a set of plain static files — no build step, no server. Everything Vercel needs is in this folder:

```
index.html            ← the site
favicon.svg           ← favicon (scalable)
favicon.png           ← favicon (256×256)
apple-touch-icon.png  ← icon for iOS home screen
og-image.png          ← social-share preview image
robots.txt            ← search-engine instructions
sitemap.xml           ← search-engine sitemap
vercel.json           ← small config (clean URLs + security headers)
```

Keep all of these in the **same folder** — the paths in `index.html` expect them at the site root.

---

## Step 1 — Deploy to Vercel

Pick whichever method you're comfortable with. Both are free.

### Method A — Vercel CLI (fastest, ~5 min)

1. Create a free account at **vercel.com** (sign up with email or GitHub).
2. Install **Node.js** if you don't have it: **nodejs.org** (the "LTS" version).
3. Open **Terminal** and run:
   ```
   npm i -g vercel
   ```
4. Move into this folder, e.g.:
   ```
   cd "path/to/Personal Website"
   ```
5. Run:
   ```
   vercel
   ```
   Follow the prompts (log in, "set up and deploy", accept the defaults, name it `midairywala`). It gives you a preview URL like `midairywala-xxxx.vercel.app`.
6. When it looks right, promote it to production:
   ```
   vercel --prod
   ```

### Method B — GitHub + Vercel (no terminal)

1. Create a **GitHub** account and a **new repository**.
2. In the repo, click **Add file → Upload files**, drag in all the files from this folder, and commit.
3. Go to **vercel.com → Add New… → Project**, import that repo, and click **Deploy**.
4. From then on, editing a file in GitHub auto-redeploys the site.

**Verify first:** open the `*.vercel.app` URL on your computer and phone. Check that the fonts, scroll animation, favicon, and all links work **before** touching your domain.

---

## Step 2 — Connect your domain (midairywala.com)

1. In your Vercel **project → Settings → Domains**, add both:
   - `midairywala.com`
   - `www.midairywala.com`
   Set **www.midairywala.com** as the primary (Vercel will offer to redirect the other one to it — accept). This matches the site's canonical URL.
2. Vercel will show you the exact **DNS records** to create. They'll look like:
   - **A record** for `midairywala.com` → an IP Vercel gives you (e.g. `76.76.21.21`)
   - **CNAME** for `www` → `cname.vercel-dns.com`
   Use exactly what Vercel displays.

## Step 3 — Update DNS at your registrar

Your domain's DNS currently points to **Webflow**. You'll swap those records for Vercel's.

1. Log in wherever **midairywala.com** is registered / where its DNS is managed (e.g. GoDaddy, Namecheap, Google Domains, Cloudflare — wherever you bought it).
2. Find the DNS settings and **replace the existing Webflow A record(s) and the `www` CNAME** with the values Vercel gave you in Step 2.
3. Save. DNS changes usually take effect within minutes but can take up to a few hours.
4. Vercel automatically issues an **HTTPS certificate** once the domain resolves — no action needed.

> I can't make DNS changes for you (that needs your registrar login), but if you paste me the records Vercel shows, I'll tell you exactly what to enter and where.

---

## Step 4 — Safe cutover (no downtime)

- Deploy and verify on the `*.vercel.app` URL **first**.
- Only then change DNS.
- **Leave the Webflow site published** until midairywala.com is confirmed serving the new Vercel site (check in an incognito window and on your phone).
- Once it's confirmed working, you can **downgrade or cancel the Webflow site plan** to stop paying for it. (Don't cancel before the domain is fully switched over.)

## Editing later

To change anything, edit `index.html` and redeploy (`vercel --prod`, or just commit to GitHub if you used Method B). Send me what you want changed and I'll hand you an updated file.
