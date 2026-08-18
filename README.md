# sparkbasin.com

Static site for SparkBasin LLC. Plain HTML + one CSS file. No build step,
no framework, no dependencies. Hosted on GitHub Pages.

## Layout

    index.html            Home
    support/index.html    Support
    privacy/index.html    Privacy policy (minimal truthful policy — see below)
    privacy/<app-slug>/   Per-app privacy policies, added as needed
    terms/index.html      Terms of service
    404.html              Not-found page (GitHub Pages serves this automatically)
    assets/site.css       All styles
    robots.txt, sitemap.xml
    .nojekyll             Tells GitHub Pages to serve files as-is (no Jekyll)
    CNAME                 Created by GitHub when the custom domain is set

Every page duplicates the header/footer by hand. That is intentional — four
pages don't justify a toolchain. If you edit the footer, edit it in all five
HTML files (grep for "Thermopolis").

NOTE: this repo must be PUBLIC (GitHub Pages on the free plan requires it).
Never commit secrets, keys, or private business documents here.

## ⚠️ Before any app store submission

`privacy/index.html` is a truthful minimal policy for the current state
(static site, no apps shipped, nothing collected). Before submitting any
app, update it — or add `/privacy/<app-slug>/` — to accurately describe
that app's actual data practices (analytics, ad SDKs, backend, permissions)
and bump the "Last updated" date. The store listing's privacy URL must
match reality at review time.

## Deploy (GitHub Pages)

1. Push this repo (public) to GitHub.
2. Repo → Settings → Pages → Source: **Deploy from a branch** →
   Branch: `main`, folder `/ (root)` → Save.
3. Site appears at `https://<owner>.github.io/<repo>/` within a minute or
   two. Every push to `main` redeploys automatically.
4. After DNS is set (below): Settings → Pages → Custom domain →
   `sparkbasin.com` → Save. Wait for the DNS check, then tick
   **Enforce HTTPS** once the certificate is issued (can take up to an
   hour).

## DNS at Namecheap (BasicDNS — nameservers do NOT change; email untouched)

Namecheap → Domain List → sparkbasin.com → Advanced DNS:

1. **Delete** the default "URL Redirect Record" for host `@`
   (the sparkbasin.com → www redirect), and any parking A/CNAME records.
   Do NOT touch MX, SPF/TXT, or DKIM records — those are email.
2. **Add** four A records, host `@`, TTL Automatic:
   - 185.199.108.153
   - 185.199.109.153
   - 185.199.110.153
   - 185.199.111.153
3. **Add** a CNAME record, host `www`, value `<owner>.github.io.`
   (the GitHub *account* domain — no repo name).
4. Optional (IPv6): AAAA records for `@`:
   2606:50c0:8000::153, 2606:50c0:8001::153,
   2606:50c0:8002::153, 2606:50c0:8003::153

With `sparkbasin.com` set as the custom domain in repo settings,
`www.sparkbasin.com` automatically 301-redirects to the apex.

Current values are documented at GitHub's "Managing a custom domain for
your GitHub Pages site" page — verify there if this README is old.

## Google Search Console

Verify as a **Domain property** (`sparkbasin.com`) using the DNS TXT record
Google provides — added at Namecheap (Advanced DNS → TXT record, host `@`).

Account caveat: do NOT create a Google account on `olie@sparkbasin.com`
until the Workspace-vs-Proton decision is made (avoids a conflicting
consumer account). Verify Search Console from an existing Google account;
additional owners can be added later, and Play Console verification can be
satisfied from whichever account ends up being the developer account.
