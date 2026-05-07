# Sage Owl Strategy Website
## Deployment Guide: GitHub → Render → GoDaddy

---

## STEP 1 — Set Up GitHub Repository

1. Go to [github.com](https://github.com) → click **New repository**
2. Name it: `sageowl-website` (or whatever you prefer)
3. Set to **Public** (required for free Render hosting)
4. Do NOT check "Add README" — we'll push our own files
5. Click **Create repository**

On your computer, open Terminal (Mac) or Command Prompt (Windows):

```bash
# Navigate into the website folder
cd path/to/sageowl-website

# Initialize git
git init

# Add all files
git add .

# First commit
git commit -m "Initial site launch"

# Connect to your GitHub repo (replace YOUR_USERNAME)
git remote add origin https://github.com/YOUR_USERNAME/sageowl-website.git

# Push
git branch -M main
git push -u origin main
```

---

## STEP 2 — Deploy on Render

1. Go to [render.com](https://render.com) → sign up (free)
2. Click **New** → **Static Site**
3. Connect your GitHub account when prompted
4. Select your `sageowl-website` repository
5. Configure:
   - **Name:** sageowl-strategy
   - **Branch:** main
   - **Root Directory:** (leave blank)
   - **Build Command:** (leave blank — no build needed)
   - **Publish Directory:** `.` (a single dot)
6. Click **Create Static Site**

Render will deploy your site to a `.onrender.com` URL. Every time you push to GitHub, it auto-deploys. ✅

---

## STEP 3 — Connect Your Custom Domain (GoDaddy)

### In Render:
1. Go to your site's dashboard → **Custom Domains**
2. Click **Add Custom Domain**
3. Type: `sageowlstrategy.com`
4. Click **Add**
5. Render will show you a **CNAME record** — copy it

### In GoDaddy:
1. Log into GoDaddy → **My Products** → find your domain
2. Click **DNS** (or Manage DNS)
3. Look for existing CNAME for `www` — edit it, or add new:
   - **Type:** CNAME
   - **Name:** `www`
   - **Value:** (paste the value Render gave you)
   - **TTL:** 600
4. For the root domain (`sageowlstrategy.com` without www), add an A record:
   - **Type:** A
   - **Name:** `@`
   - **Value:** (Render will provide an IP — check their docs at render.com/docs/custom-domains)
5. Save changes

DNS propagation takes 15 minutes to 48 hours. Render will confirm when the domain is verified.

---

## STEP 4 — Activate Tracking

### Google Analytics 4:
1. Go to [analytics.google.com](https://analytics.google.com)
2. Create a new property → get your **Measurement ID** (format: `G-XXXXXXXXXX`)
3. Open each HTML file, find the GA comment block, uncomment it, and replace `G-XXXXXXXXXX` with your real ID

### Metricool:
1. Go to your Metricool dashboard → Settings → Tracking pixel
2. Copy your hash
3. In each HTML file, find the Metricool comment block, uncomment it, and replace `PASTE_YOUR_METRICOOL_HASH_HERE` with your actual hash

---

## STEP 5 — Making Updates Going Forward

Every time you make changes to the site files:

```bash
git add .
git commit -m "Describe what you changed"
git push
```

Render detects the push and auto-deploys within ~60 seconds.

---

## FILE STRUCTURE

```
sageowl-website/
├── index.html              ← Home
├── about.html              ← About Shannon
├── sovereign-room.html     ← The Sovereign Room
├── roadmap.html            ← The Sage Owl Roadmap
├── contact.html            ← Schedule a Discovery Call
├── styles.css              ← All shared styles
├── images/
│   ├── logo.png            ← Full horizontal logo
│   ├── icon.png            ← Owl icon (favicon + inline)
│   ├── shannon-headshot.png
│   ├── shannon-swing.png
│   ├── shannon-media.png
│   └── shannon-banner.png
└── README.md               ← This file
```

---

## ADDING SEO CONTENT (Ongoing)

Each page already has:
- `<title>` tag
- `<meta name="description">`
- `<link rel="canonical">`
- Open Graph tags (og:title, og:description, og:image)
- Schema.org JSON-LD (Home page)

To update: open the relevant HTML file, find the `<head>` section, edit the meta tags.

---

## NOTES

- The Cal.com embed on the Contact page uses `cal.com/inthefeed/sos` — update if your URL changes
- The Skool link is `skool.com/the-sovereign-room-8206` — update if it changes
- Images are referenced as relative paths (`images/logo.png`) so they work on any domain
- The site is fully mobile-responsive
- No database, no build process, no dependencies — pure HTML/CSS/JS = blazing fast load times

---

*Built for Sage Owl Strategy · Shannon Kuykendall · 2026 🦉*
