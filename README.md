# MUSE Dallas · website

One-page site for MUSE Dallas, served as a **Cloudflare Worker** (static assets, no build step).

```
public/                 everything visitors see
  index.html            page, styles and script
  404.html              "page not found" page
  _headers              caching and security headers
  robots.txt
  assets/img/           photos, flyers, logo, favicon
  assets/fonts/         Cormorant Garamond + Jost (self-hosted, SIL Open Font License)
  assets/vendor/        Swiper (card carousels)
wrangler.jsonc          Cloudflare Worker settings
```

## Deploy (one-time setup)

1. In the Cloudflare dashboard go to **Workers & Pages → Create → Import a repository**.
2. Connect GitHub and pick this repo.
3. Leave the build command empty. The deploy command is `npx wrangler deploy` (the default).
4. Deploy. The site goes live on a `muse-dallas.<your-subdomain>.workers.dev` address.
5. To use the real domain: the Worker → **Settings → Domains & Routes → Add → Custom domain**.

After that, every push to `main` redeploys automatically.

To preview locally: `npx wrangler dev`, then open http://localhost:8787

## Common edits (all in `public/index.html`)

Search for `EDIT HERE` near the bottom of the file.

| To change | Edit |
|---|---|
| Resy link | `LINKS.resy` (every Reserve button, including the phone bar) |
| Tripleseat private event form | `LINKS.tripleseat` |
| Cocktail / food menu buttons | `LINKS.cocktailMenu`, `LINKS.foodMenu` |
| Instagram / TikTok | `LINKS.instagram`, `LINKS.tiktok` |
| Cocktail cards | `COCKTAILS` list |
| Event flyers | `EVENTS` list: title, kicker, date, image, description, optional ticket link |

Any link left as `''` shows a "coming soon" note when clicked.

### Event flyers
1. Save the flyer in `public/assets/img/` as `.webp`, 4:5 portrait (e.g. 1200×1500).
2. Add or edit its entry in `EVENTS` with `img:'file-name'` (no extension) and `flyer:true`.
3. The text under the carousel (date, name, description, Reserve button) comes from the same entry.

### Photos
- Hero: replace `public/assets/img/hero-portrait.webp` (subject on the left half).
- After Dark: background loop is the `<img>` tags in `#adMedia` (a comment shows how to use a video); the photo row is `.ad-strip`.
- Gallery strip: the `<button class="g-item">` tags, in scroll order. It loops and scrolls itself.

### Hours and address
In the "HOURS & ADDRESS" section, replace each `Coming soon` and the "Address coming soon" line.

### When the domain is live
In the `<head>`, change `og:image` to a full URL (e.g. `https://musedallas.com/assets/img/bar.webp`) so link previews show the photo.
