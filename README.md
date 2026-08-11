# [NAME] — Lifeguard Site

Static one-page site advertising availability as a certified lifeguard for private parties,
community pools, and backyard events in Austin, TX.

Plain HTML/CSS + ~20 lines of vanilla JS. No framework, no build step, no dependencies.

## Structure

```
/
├── index.html          all seven sections, currently lorem ipsum
├── css/style.css       single stylesheet
├── js/main.js          mobile nav toggle + footer year
├── images/             SVG placeholders — swap for real photos
├── .nojekyll           tells GitHub Pages to serve files as-is
└── README.md
```

## Local preview

```bash
python3 -m http.server 8000
# open http://localhost:8000
```

Opening `index.html` directly with `file://` also works, since there's no build step.

## Publishing to GitHub Pages

1. Create a new repo on GitHub (suggested name: `lifeguard-site`). **Public** — Pages
   requires public repos on free accounts.
2. Push this folder:
   ```bash
   git remote add origin https://github.com/<username>/lifeguard-site.git
   git branch -M main
   git push -u origin main
   ```
3. In the repo: **Settings → Pages → Build and deployment → Source: Deploy from a branch**,
   branch `main`, folder `/ (root)`. Save.
4. Wait ~1 minute. Live at `https://<username>.github.io/lifeguard-site/`.

All asset paths are relative (`css/style.css`, not `/css/style.css`), so the site works
both locally and under the `/lifeguard-site/` subpath without changes.

## Adding a custom domain later

1. Buy the domain.
2. Add a file named `CNAME` at the repo root containing only the domain (e.g. `example.com`).
3. At the registrar, add four `A` records pointing at `185.199.108.153`, `185.199.109.153`,
   `185.199.110.153`, `185.199.111.153` — or a `CNAME` record for `www` pointing at
   `<username>.github.io`.
4. Settings → Pages → Custom domain → enter it → check **Enforce HTTPS**.

Nothing in the site needs to change.

## Placeholders to replace

Search for these tokens across the project:

| Token             | What it is                                       |
|-------------------|--------------------------------------------------|
| `[NAME]`          | His name — page title, nav brand, footer         |
| `[EMAIL]`         | Contact email (also in the `mailto:` href)       |
| `[PHONE]`         | Display phone number                             |
| `[PHONE-E164]`    | `tel:` href value, e.g. `+15125550123`           |
| `[HANDLE]`        | Instagram handle, no `@`                         |
| `[Issuing body]`  | e.g. American Red Cross                          |
| `[date]`          | Certification expiration dates                   |
| `[Parent name]`   | Testimonial attributions                         |
| `[Season/year]`   | City of Austin lifeguard season                  |

```bash
grep -rn "\[NAME\]\|\[EMAIL\]\|\[PHONE\]\|\[HANDLE\]" .
```

Images: replace `images/hero.svg` and `images/gallery-1..6.svg` with real photos. If you use
`.jpg`, update the `src` attributes in `index.html`. Keep gallery photos roughly 4:3 — the CSS
crops to that ratio regardless.
