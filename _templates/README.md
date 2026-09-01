# New page from this template

You have about fifteen minutes. There is no build step. Copy a file, fill in the brackets, ship.

## 1. Copy the file

From the repo root:

```
mkdir [slug] && cp _templates/page.html [slug]/index.html
```

Trailing slash on the public URL means the file must live at `[slug]/index.html`, not `[slug].html` (`vercel.json` sets `trailingSlash: true`, so `/[slug]` 308s to `/[slug]/`).

**Before creating a page, read the architecture rule (2026-09-01):** the site is deliberately compact — `/`, `/who-i-help/`, `/how-i-help/`, `/about/`. Do not add one page per profession or per keyword. A new page needs a genuinely distinct intent, enough substance to stand alone, and a reason a section on an existing page won't do. The old `answers/` and `for/` scaffolds were removed for that reason.

## 2. Replace every `[bracket]`

Search the new file for `[` and replace all of these:

| Placeholder | What to put |
|---|---|
| `[Page title]` | The H1 and the title/og/twitter/headline text (three places in `<head>`, one in JSON-LD, one in the body). Keep them the same. |
| `[One-sentence description.]` | Meta description and og/twitter description. Same sentence in all three. No prices. |
| `[slug]` | The directory name. Canonical, og:url, and JSON-LD `url` must be `https://www.marklevy.ai/[slug]/` — www, trailing slash, never the apex host. |
| `[YYYY-MM-DD]` | Today's date in JSON-LD `datePublished` and `dateModified`, and in the visible "Last verified" line. When you later edit the page, bump `dateModified` and "Last verified"; leave `datePublished` alone. |
| `[Opening paragraph.]` | The actual page. Write in the body of the `<article>`. |
| `[One-sentence invitation for this profession.]` | The first line of the closer. Example: "If you run a solo law practice and this is the problem you actually have, the next step is a short conversation." |

Leave the "Who this is NOT for" sentence exactly as it is. The booking link goes to Calendly (`https://calendly.com/mark-marklevy/30min`) — do not point it at an extra site page.

## 3. Add the URL to the sitemap

Open `sitemap.xml` at the repo root. Copy an existing `<url>` block. Set `<loc>` to the www URL with a trailing slash. Set `<lastmod>` to today. Do not add `<priority>` or `<changefreq>`.

Do not add `_templates/` to the sitemap.

## 4. Rules that will get you in trouble if you skip them

- No `<script>` except `type="application/ld+json"`. No booking widgets, no tag manager, no CMS.
- No prices anywhere. If a number with a dollar sign wants to go on the page, stop.
- Canonical host is always `https://www.marklevy.ai`.
- Header (`<nav>`) and footer are shared with the homepage and the three inner pages (`who-i-help/`, `how-i-help/`, `about/`). If you change them here, change all of those to match, and vice versa.
- After you ship, update "Last verified" when you next confirm the page is still true.

## 5. Ship

Commit and push `main`. Mark ships production; do not deploy from a tool.

```
git add [slug]/index.html sitemap.xml
git commit -m "Add /[slug]/"
git push origin main
```
