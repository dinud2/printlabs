# Deploying 3D Printing Labs (free, ~15 minutes)

The whole `site/` folder is a static website — no build step. Hosting, the consultation form
(with file uploads), and email notifications are all free on Netlify's free tier.

## 1. Deploy to Netlify

**Easiest (drag & drop):**
1. Go to https://app.netlify.com and sign up (free, use any account).
2. On the dashboard, find "Sites" → drag the entire `site/` folder onto the drop area
   ("Drag and drop your site output folder here").
3. Netlify gives you a live URL like `random-name-123.netlify.app` within seconds. Done.

> When you later change the site, drag the folder in again (Deploys tab → drag & drop)
> — it replaces the old version at the same URL.

## 2. Turn on email notifications for the form

Netlify auto-detects the `consultation` form on deploy.

1. In your site's dashboard: **Forms** → verify `consultation` is listed.
2. Go to **Site configuration → Notifications → Form submission notifications**
   (on newer UI: Forms → Notifications).
3. **Add notification → Email notification** → set the recipient to
   `dinudaham02@gmail.com` → save.

Every submission now emails you the customer's name/email/phone, project details, and
**download links for their uploaded model files** (files are stored by Netlify; links are in
the email and in the Forms dashboard).

**Free-tier limits:** 100 submissions/month, 8MB max per uploaded file (the form already
enforces 8MB client-side and tells customers to paste a Drive/WeTransfer link for bigger
models).

**Test after deploying:** submit the form yourself with a small STL and confirm the email
arrives at dinudaham02@gmail.com. (Check spam the first time.)

## 3. Connect your Namecheap domain (free)

1. Netlify dashboard → **Domain management → Add a domain** → enter your domain
   (e.g. `3dprintinglabs.ca`) → Netlify shows the DNS records it needs.
2. Recommended: use **Netlify DNS** — Netlify gives you 4 nameservers
   (like `dns1.p03.nsone.net`). In Namecheap: **Domain List → Manage → Nameservers →
   Custom DNS** → paste the 4 nameservers. Wait up to a few hours for propagation.
   - Alternative (keep Namecheap DNS): add an **A record** `@ → 75.2.60.5` and a
     **CNAME** `www → your-site.netlify.app` in Namecheap's Advanced DNS tab.
3. Back in Netlify, HTTPS is provisioned automatically (Let's Encrypt) once DNS resolves.

## 4. Editing the site later

- All copy lives directly in the four HTML files (`index.html`, `work.html`,
  `consultation.html`, `success.html`) — edit text, redeploy.
- Project photos live in `assets/projects/`. To add a project: drop in a photo (JPG,
  ~1600px max edge) and copy one of the `<article>` blocks in `work.html`.
- The gallery captions were drafted from the photos — tweak titles/descriptions in
  `work.html` if anything is off.

## Later: automatic customer status emails ("printing" / "shipped")

Today's flow already promises email updates, which you can send manually from Gmail
(a template like "Your print is complete — shipping tomorrow" takes 30 seconds).
When you want to automate it, good zero/low-cost options:

1. **Google Sheet + Apps Script** (free): track orders in a sheet with a Status column;
   an Apps Script trigger emails the customer from your Gmail whenever you change the
   status. No servers, sends from your real address.
2. **Netlify Function + email API** (free tier): a small serverless function that sends
   templated emails via an email API (e.g. Resend/Brevo free tiers) — good once volume grows.

Option 1 is the natural first step — ask Claude to build it when you're ready.
