# campurastudios.com

Static site, no build step. GitHub Pages serves it as-is.

- `/`: the studio
- `/golfcoursetycoon/`: the game
- `/impressum/`, `/privacy/`: German legal pages (required for a German operator)

Everything still owed is marked `TODO(ede)`: `grep -rn "TODO(ede)" .`

## Going live (once)

1. **GitHub:** create a *public* repo `campurastudios-site` (Pages from a private repo needs a paid plan)
   and push `main`. Settings → Pages → Source: *Deploy from a branch*, `main`, `/ (root)`.
   Custom domain: `campurastudios.com` (the `CNAME` file already says so).
2. **Squarespace → Domains → campurastudios.com → DNS.** Delete Squarespace's own website
   records (the `@` A records and the `www` CNAME pointing at Squarespace). **Leave every MX, TXT
   and `google._domainkey` record alone: those are your Google Workspace mail.** Add:

   | Host | Type | Value |
   |---|---|---|
   | @ | A | 185.199.108.153 |
   | @ | A | 185.199.109.153 |
   | @ | A | 185.199.110.153 |
   | @ | A | 185.199.111.153 |
   | www | CNAME | `<your-github-username>.github.io` |

3. Wait for DNS (minutes to a few hours), then tick **Enforce HTTPS** in the Pages settings.
4. Keep auto-renew on for the domain at Squarespace: your email lives on it.

## Preview locally

    python -m http.server 8000

then open http://localhost:8000/. Paths are absolute (`/assets/...`), so opening the files
directly from disk will not load the styles.
