# Sugrowth Deployment Notes

These notes assume the domain is `sugrowth.ca`, the registrar is Namecheap, DNS is managed by Cloudflare, and the source code lives in `sugrowth/Sugrowth-Public`.

## Recommended Hosting

Use Cloudflare Pages connected to GitHub.

1. In Cloudflare Pages, connect the GitHub repo `sugrowth/Sugrowth-Public`.
2. Set the production branch to `site`.
3. Leave the build command empty.
4. Set the output directory to `/`.
5. Add `site-test` as a preview branch.
6. Add custom domains:
   - `sugrowth.ca`
   - `www.sugrowth.ca`
7. Keep DNS in Cloudflare since the domain is already using Cloudflare.

This keeps the website running from GitHub while Cloudflare handles CDN, SSL, previews, and DNS.

## GitHub Pages Fallback

If you prefer GitHub Pages instead:

1. Go to GitHub repo settings.
2. Open Pages.
3. Set the source branch to `site`.
4. Set the folder to `/`.
5. Keep the `CNAME` file as `sugrowth.ca`.
6. In Cloudflare DNS, point the apex and `www` records to GitHub Pages according to GitHub's current Pages instructions.

## Domain Email

For receiving email at `support@sugrowth.ca`, `scrolloff@sugrowth.ca`, and `textezi@sugrowth.ca`, use Cloudflare Email Service routing.

1. In Cloudflare, open Compute > Email Service > Email Routing for `sugrowth.ca`.
2. Add a destination address such as `sugrowth@gmail.com`.
3. Verify that destination inbox.
4. Create these routing rules:
   - `support@sugrowth.ca` -> `sugrowth@gmail.com`
   - `scrolloff@sugrowth.ca` -> `sugrowth@gmail.com`
   - `textezi@sugrowth.ca` -> `sugrowth@gmail.com`
5. Add the MX and TXT records Cloudflare shows during domain onboarding.
6. Remove conflicting MX records if Namecheap or another email provider added any earlier.

For each rule, use:

- Email pattern: `support`, `scrolloff`, or `textezi`
- Domain: `sugrowth.ca`
- Action: Send to an email
- Destination: `sugrowth@gmail.com`

For human replies from `support@sugrowth.ca`, `scrolloff@sugrowth.ca`, or `textezi@sugrowth.ca`, use a mailbox provider such as Google Workspace, Zoho Mail, Proton Mail, or Fastmail. For app or system email, Cloudflare Email Service can send outbound messages through the REST API or a Workers binding after the sending domain is onboarded.

## Suggested Branch Flow

1. Build and test on `site-test`.
2. Merge `site-test` into `site` when ready.
3. Cloudflare Pages deploys `site` to production.
4. Keep `main` as the clean repository baseline unless you decide to make it the default development branch.
