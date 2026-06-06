# Deployment Notes

## Current Build

This site is a static Astro website for Fishermans Road Art Gallery.

- Domain: `fishermansgallery.au`
- Public email: `admin@fishermansgallery.au`
- Facebook: `https://www.facebook.com/profile.php?id=61569997992313`
- GitHub repository: `https://github.com/fishermansgallery/fishermans-road-art-gallery`
- Build command: `npm run build`
- Output directory: `dist`

## Current Deployment Status

As of 6 June 2026, GitHub and Cloudflare Pages are set up.

GitHub:

- Account: `fishermansgallery`
- Repository: `fishermansgallery/fishermans-road-art-gallery`
- Repository URL: `https://github.com/fishermansgallery/fishermans-road-art-gallery`
- Production branch: `main`

Cloudflare Pages:

- Account shown in Wrangler/Cloudflare: `david.jp.ramsay@gmail.com`
- Account ID: `45f6d9d178d3293809ae6d5ca02467c6`
- Project: `fishermans-road-art-gallery`
- Pages hostname: `https://fishermans-road-art-gallery.pages.dev`
- Direct deployment returned by Wrangler on 6 June 2026: `https://755f25bc.fishermans-road-art-gallery.pages.dev`
- Deployment source: direct Wrangler upload, not Git-connected yet

The `.pages.dev` URL is deployed, but the managed school network currently blocks that URL category, so local browser/curl checks may show a Jamf/Wandera block page instead of the site. Cloudflare's deployment list shows the Pages deployment succeeded.

## Domain Status

Cloudflare DNS has been started for `fishermansgallery.au`.

Assigned Cloudflare nameservers:

```text
braelyn.ns.cloudflare.com
tony.ns.cloudflare.com
```

GoDaddy still showed `fishermansgallery.au` as `Pending Registration` on 6 June 2026. Public DNS checks returned no nameservers yet, so the domain is not ready for the custom-domain cutover.

Cloudflare Pages will not attach `fishermansgallery.au` as a custom domain until DNS management is transferred to Cloudflare. The Pages custom-domain wizard currently shows:

```text
Before adding fishermansgallery.au to your Pages project, you'll need to transfer your DNS to Cloudflare.
```

## GoDaddy DNS

When GoDaddy finishes registering the domain, use Cloudflare as the authoritative DNS provider.

1. In GoDaddy, open `fishermansgallery.au`.
2. Open the domain's DNS or nameserver settings.
3. Choose custom nameservers.
4. Replace the GoDaddy nameservers with:
   - `braelyn.ns.cloudflare.com`
   - `tony.ns.cloudflare.com`
5. Save the change.
6. In Cloudflare, open `fishermansgallery.au` and use **I updated my nameservers** if shown.

Propagation can be quick, but GoDaddy and Cloudflare both warn that global DNS changes can take up to 48 hours.

## After Nameservers Are Active

After Cloudflare confirms `fishermansgallery.au` is active:

1. Open Cloudflare Pages > `fishermans-road-art-gallery` > **Custom domains**.
2. Add `fishermansgallery.au`.
3. Add `www.fishermansgallery.au`.
4. Confirm Cloudflare created the required Pages DNS records.
5. Visit `https://fishermansgallery.au` and `https://www.fishermansgallery.au`.
6. Confirm `www` redirects to the apex domain.

## Email

The public contact flow opens a prefilled email to `admin@fishermansgallery.au`. That address still needs working mail delivery before launch.

Recommended next step after nameservers are active:

1. Use Cloudflare Email Routing for `admin@fishermansgallery.au`.
2. Forward it to an existing mailbox the gallery can monitor.
3. Add any MX/SPF/DKIM/DMARC records Cloudflare requires.
4. Send a test email to `admin@fishermansgallery.au`.

If GoDaddy email, Google Workspace, or Microsoft 365 is used instead, recreate their mail records inside Cloudflare DNS after the nameserver switch.

## Pages CMS

The `.pages.yml` file lets Pages CMS edit homepage copy and image uploads after the GitHub repository exists.

1. Authorize Pages CMS for the GitHub repository.
2. Open `https://app.pagescms.org/`.
3. Select the repository and `main` branch.
4. Edit homepage content and media.
