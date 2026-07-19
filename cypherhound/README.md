# CypherHound site

Static landing page + Terms of Service + Privacy Policy for the CypherHound
Discord bot. No build step — plain HTML/CSS, ready for GitHub Pages.

## Before you publish

Open `terms.html` and `privacy.html` and replace the placeholder
`contact@example.com` with a real contact address (an email, or a link to a
support Discord server). Also double check the claims in Section 1 of the
privacy policy still match what the bot actually logs if you add any
database/logging later.

## Deploy to GitHub Pages (username.github.io style)

1. Create a new GitHub repo. For a **user/organization site**, it must be
   named exactly `<your-username>.github.io`. For a **project site**, any
   repo name works and your site will live at
   `https://<your-username>.github.io/<repo-name>/`.

2. Push these files to the repo root:
   ```bash
   cd cypherhound-site
   git init
   git add .
   git commit -m "CypherHound site"
   git branch -M main
   git remote add origin https://github.com/<your-username>/<repo-name>.git
   git push -u origin main
   ```

3. On GitHub: **Settings → Pages** → under "Build and deployment", set
   **Source** to `Deploy from a branch`, branch `main`, folder `/ (root)` →
   **Save**.

4. GitHub will give you a live URL within a minute or two, e.g.
   `https://yourusername.github.io/cypherhound/`. `terms.html` and
   `privacy.html` will be at that same base URL.

## Link it from Discord

In the [Discord Developer Portal](https://discord.com/developers/applications),
open your CypherHound application → **General Information** → scroll to
**Terms of Service URL** and **Privacy Policy URL** → paste in:
```
https://yourusername.github.io/cypherhound/terms.html
https://yourusername.github.io/cypherhound/privacy.html
```
Save changes. These links will then show up automatically on the bot's
public profile page/invite screen.

## Files

- `index.html` — landing page with command overview
- `terms.html` — Terms of Service
- `privacy.html` — Privacy Policy
- `style.css` — shared styling
- `assets/logo.png`, `assets/banner.png` — branding art
