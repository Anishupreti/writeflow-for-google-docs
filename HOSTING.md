# Hosting the website on GitHub Pages

Free hosting on GitHub, with **your own domain** on top. Google's OAuth verification requires the homepage and privacy policy to be on a domain you own and have verified, so a plain `username.github.io` address is fine for the beta but not for verification.

## 1. Create the website repository (5 minutes)

On a free GitHub account, Pages only publishes from a **public** repository, so keep the website separate from the add-on code (which can stay private).

1. On GitHub: **New repository** → name it, for example, `writeflow-site` → **Public** → Create.
2. Upload the contents of this `site/` folder to the root of that repository: `index.html`, `help.html`, `privacy.html`, `terms.html`, `style.css` and `.nojekyll`. Leave out this `HOSTING.md` and `CNAME.example`.
3. Repository **Settings → Pages** → Source: **Deploy from a branch** → Branch: `main`, folder `/ (root)` → Save.
4. After a minute the site is live at `https://USERNAME.github.io/writeflow-site/`. That's enough for the beta.

## 2. Add your own domain (before Google verification)

1. Buy a domain from any registrar.
2. In the website repository: **Settings → Pages → Custom domain** → enter `www.yourdomain.com` → Save. GitHub adds a `CNAME` file to the repository (see `CNAME.example`).
3. At your registrar's DNS settings, add the records GitHub's documentation lists for custom domains. At the time of writing these are:
   - `www` → **CNAME** → `USERNAME.github.io`
   - the bare domain (`@`) → **A** records `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
   
   Check GitHub's "Managing a custom domain for your GitHub Pages site" page for the current values before saving.
4. Back in **Settings → Pages**, wait for the DNS check to pass, then tick **Enforce HTTPS**.
5. Optional but recommended: verify the domain for your GitHub account (**GitHub Settings → Pages → Add a domain**) so nobody else can claim it on GitHub.

## 3. Verify the domain with Google

1. Open **Google Search Console** → Add property → **Domain** → `yourdomain.com`.
2. Add the TXT record it gives you at your registrar; click Verify.
3. Use a Google account that is an **owner or editor** of the add-on's Google Cloud project, as Google requires.
4. On the OAuth consent screen, add `yourdomain.com` under **Authorized domains**, and set the homepage, privacy policy and terms links to `https://www.yourdomain.com/`, `/privacy.html` and `/terms.html`.

## 4. Point the add-on at the site

In `Code.gs`, set:
- `CONFIG.siteUrl` to `https://www.yourdomain.com` (no trailing slash)
- `CONFIG.supportEmail` to an address on your domain, if you set up email there

Then release as in `RELEASING.md`. The sidebar and Help dialog start showing the Help, Privacy and Terms links automatically.

## Before verification, also on the site

- Replace `support@YOUR-DOMAIN.example` in `index.html` and `help.html`.
- Point the "Join the beta" button at your sign-up form.
- Fill every `[bracket]` in `privacy.html` and `terms.html` (edit `launch/PRIVACY.md` and `launch/TERMS.md`, then regenerate), and remove the "Draft" notice only after legal review.
