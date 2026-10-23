# microcosm.bio

The one-page site for Microcosm Bioscience. It's plain static files with no
build step, hosted on GitHub Pages.

| File | What it is |
| --- | --- |
| `index.html` | The page: logo (inline SVG), tagline, "Contact us" link |
| `styles.css` | All styling. Colors live at the top. |
| `404.html` | Shown for any missing URL |
| `favicon.svg`, `apple-touch-icon.png` | Browser tab / home-screen icons |
| `og.png` | 1200×630 preview image for link shares (Slack, LinkedIn, iMessage…) |
| `CNAME` | Tells GitHub Pages the custom domain. Don't delete it. |

## Change the colors

Every color on the site, logo included, comes from these six lines at the top
of `styles.css`:

```css
:root {
  --bg:      #0B0841;  /* page background */
  --logo:    #FFFFFF;  /* Microcosm, Bioscience, rule */
  --orb:     #DA7842;  /* circle */
  --tagline: #ADC9E9;
  --link:    #6093D4;
  --link-hover: #8DB3E6;
}
```

Edit the hex values, save, and redeploy. For example, setting `--orb: #3FB68B;`
turns the circle green and `--logo: #F4E9D8;` makes the wordmark cream. An
alternate light palette sits in a comment right below the block, ready to paste in.

Three places can't read CSS variables, so if you change `--bg` or `--orb`,
update these by hand too:

- `index.html` and `404.html`: `<meta name="theme-color" content="#0B0841">` (mobile browser bar color)
- `favicon.svg`: the two `fill="#…"` values
- `apple-touch-icon.png` and `og.png` are images; regenerate them (ask Claude) or leave them as they are

## Edit the text

Open `index.html`:

- **Tagline**: the `<p class="tagline">` line. The `<br>` sets where the line
  breaks on wide screens; on phones the text wraps on its own. Also update the
  matching `description`, `og:description`, and `twitter:description` meta tags in `<head>`.
- **Contact link**: `<a class="contact" href="mailto:contact@microcosm.bio">`.

The logo is drawn as vector outlines (Tw Cen MT Bold Italic / Italic converted
to paths), so the site never loads the font file. To change the logo
wording, the outlines have to be regenerated from the font.

## Redeploy

```bash
cd ~/microcosm-site && git add -A && git commit -m "Update site" && git push
```

GitHub Pages rebuilds automatically, and changes are live in about a minute.

## Preview locally

```bash
cd ~/microcosm-site && python3 -m http.server 8000
```

Then open http://localhost:8000.

## DNS (Namecheap → microcosm.bio → Advanced DNS)

| Type | Host | Value |
| --- | --- | --- |
| A | `@` | `185.199.108.153` |
| A | `@` | `185.199.109.153` |
| A | `@` | `185.199.110.153` |
| A | `@` | `185.199.111.153` |
| CNAME | `www` | `jacklindsay-1.github.io.` |

The MX, SPF, DKIM (`google._domainkey`), DMARC, and google-site-verification
records run Google Workspace email. Leave them alone.
