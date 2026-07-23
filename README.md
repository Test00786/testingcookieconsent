# TrendyNest Dummy Test Site — Deploy to Netlify

## What's in this folder
19 static HTML pages matching the site map + cookie table from earlier, each with
a tiny inline `<script>` that sets that page's cookies via `document.cookie`
(1‑day expiry, `path=/`, `SameSite=Lax`) and nav links that recreate the depth
structure, so a crawler-based scanner discovers pages the same way it would on
a real site.

## Deploy (2 minutes, no account changes needed)
1. Go to https://app.netlify.com/drop
2. Drag this whole `main` folder onto the page.
3. Netlify gives you a random URL like `https://random-name-123.netlify.app` —
   that's your working `https://` domain. Use it wherever these notes said
   `www.trendynest.example`.
4. (Optional) In Site settings → Domain management, you can rename the
   Netlify subdomain or attach a real custom domain if you own one.

## About the "subdomain" test (blog.trendynest.example)
Netlify Drop gives you one flat domain — it can't create a true subdomain
for you. To actually test the **Include Subdomain** checkbox for real:
- Deploy the sibling `blog-subdomain-deploy` folder as a **second, separate**
  Netlify site the same way (drag-and-drop).
- If you own a real domain, add both sites as custom domains on that domain:
  `www.yourdomain.com` for the main site and `blog.yourdomain.com` for the
  blog site (Netlify → Domain management → Add custom domain, then update
  your DNS with a CNAME record).
- Without a real domain, you'll have two unrelated `*.netlify.app` URLs —
  fine for testing Page Depth/Limit/Exclude/Include-URL logic, but it won't
  exercise true subdomain detection since they won't share a parent domain.

## Notes on the cookies
- All cookies here are set as first-party via JS for simplicity, including
  the three "Unwanted"-category ones (`shadow_tracker`, `adnetworkX_uid`,
  `cross_site_pixel`). A real ad-tech tracker would usually be third-party
  (set from an iframe on someone else's domain) — swap these for an actual
  third-party test pixel if your scanner specifically needs to detect
  third-party cookies.
- `/login/`, `/admin/`, and `/admin/dashboard/` are the pages meant for your
  Exclude URLs test.
- `/shop/men/shirts/casual/` and `/shop/men/shirts/formal/` sit at depth 4 —
  useful for testing Page Depth limits.
- There's a `404.html` and no page actually 404s on this site by default —
  add a URL like `/shop/discontinued-page/` to Include/Exclude URLs to
  trigger a real "unreachable URL" test case.
