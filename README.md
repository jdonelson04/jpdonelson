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

## Adding a custom domain later

We own `jdonelson.com`. The likely setup is a subdomain for this site — e.g.
`jp.jdonelson.com` — leaving the apex free.

For a subdomain:

1. At the registrar, add a `CNAME` record: `jp` → `jdonelson04.github.io`
2. Add a file named `CNAME` at the repo root containing only `jp.jdonelson.com`
3. GitHub → Settings → Pages → Custom domain → enter it → check **Enforce HTTPS**

For the apex (`jdonelson.com`) instead, use four `A` records pointing at
`185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`.

Either way, GitHub issues a free TLS certificate and redirects the old
`jdonelson04.github.io/jpdonelson/` URL to the new domain. Nothing in the site changes.

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
