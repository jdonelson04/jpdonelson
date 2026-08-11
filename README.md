# jpdonelson

Personal site for [NAME]. Currently a single page advertising availability as a
certified lifeguard for parties, community pools, and backyard events in Austin, TX —
structured so other content (other work, projects, hobbies) can be added later without
starting over.

**Live:** https://jdonelson04.github.io/jpdonelson/

Plain HTML/CSS + ~20 lines of vanilla JS. No framework, no build step, no dependencies.

## Structure

```
/
├── index.html          the one page, all seven sections
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

## Publishing

Already wired up. GitHub Pages deploys from the `main` branch, root folder.
To publish a change:

```bash
git add -A
git commit -m "describe the change"
git push
```

Pages rebuilds automatically, usually under a minute. No other steps.

All asset paths are relative (`css/style.css`, not `/css/style.css`), so the site works
locally, under the `/jpdonelson/` subpath, and on a custom domain without changes.

## Adding a custom domain

We own `jpdonelson.com`, plus `.store`, `.studio`, and `.info`.

Target is the apex — `jpdonelson.com` — with `www` redirecting to it.

**At the registrar,** for `jpdonelson.com`:

| Type    | Name  | Value                  |
|---------|-------|------------------------|
| A       | `@`   | `185.199.108.153`      |
| A       | `@`   | `185.199.109.153`      |
| A       | `@`   | `185.199.110.153`      |
| A       | `@`   | `185.199.111.153`      |
| CNAME   | `www` | `jdonelson04.github.io`|

Optionally add four `AAAA` records for IPv6: `2606:50c0:8000::153`, `2606:50c0:8001::153`,
`2606:50c0:8002::153`, `2606:50c0:8003::153`.

**In this repo:** add a file named `CNAME` at the root containing exactly one line:

```
jpdonelson.com
```

**In GitHub:** Settings → Pages → Custom domain → `jpdonelson.com` → Save, then check
**Enforce HTTPS** once the certificate is issued (can take a few minutes).

GitHub issues a free TLS certificate and redirects the old
`jdonelson04.github.io/jpdonelson/` URL to the new domain, so nothing already shared breaks.
DNS changes can take up to 24 hours to propagate, though it is usually much faster.

**The other TLDs.** GitHub Pages serves exactly one custom domain per repository. To make
`.store`, `.studio`, or `.info` reach the site, set up URL forwarding at the registrar
pointing each one at `https://jpdonelson.com` — that is a registrar feature, not a GitHub one.

## Placeholders to replace

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

Find them all:

```bash
grep -rn "\[NAME\]\|\[EMAIL\]\|\[PHONE\]\|\[HANDLE\]\|\[Issuing body\]" .
```

Images: replace `images/hero.svg` and `images/gallery-1..6.svg` with real photos. If you use
`.jpg`, update the `src` attributes in `index.html`. Keep gallery photos roughly 4:3 — the CSS
crops to that ratio regardless.

## A note on running git here

Editing these files through the Claude desktop folder bridge can leave stale
`.git/index.lock` files behind, because the mount blocks the cleanup step. Run git
commands in your own Terminal. If you ever see
`Unable to create '.git/index.lock': File exists`, delete that file and retry.
