# Deployment Notes

## Current Build

This site is a static Astro website for Fishermans Road Art Gallery.

- Domain: `fishermansgallery.au`
- Public email: `admin@fishermansgallery.au`
- Facebook: `https://www.facebook.com/profile.php?id=61569997992313`
- Build command: `npm run build`
- Output directory: `dist`

## Account Creation

Brand-new GitHub and Cloudflare accounts need to be created manually in the browser because they require passwords, verification emails, and often CAPTCHA or 2FA.

Use an email address that can receive verification immediately. If `admin@fishermansgallery.au` is not receiving mail yet, use a working email first and add the gallery email later after DNS and email routing are configured.

## GitHub

1. Create or log in to the dedicated GitHub account.
2. Create a repository named `fishermans-road-art-gallery` or `fishermansgallery`.
3. Push this project to the repository.
4. Keep `main` as the production branch.

## Cloudflare Pages

1. Create or log in to the dedicated Cloudflare account.
2. Add the domain `fishermansgallery.au` to Cloudflare.
3. Create a Pages project using **Workers & Pages** > **Create application** > **Pages** > **Connect to Git**.
4. Select the GitHub repository.
5. Use these build settings:
   - Framework preset: Astro
   - Build command: `npm run build`
   - Output directory: `dist`
   - Root directory: `/`
   - Production branch: `main`
   - Environment variable: `NODE_VERSION=22`
6. After the first deploy, add custom domains:
   - `fishermansgallery.au`
   - `www.fishermansgallery.au`

## GoDaddy DNS

Use Cloudflare as the authoritative DNS provider for the domain.

1. In Cloudflare, copy the two assigned nameservers for `fishermansgallery.au`.
2. In GoDaddy, open the domain DNS settings.
3. Go to **Nameservers**.
4. Choose the option to use custom nameservers.
5. Paste the two Cloudflare nameservers and save.

Propagation can be quick, but GoDaddy and Cloudflare both warn that global DNS changes can take up to 48 hours.

## Email

The public contact flow opens a prefilled email to `admin@fishermansgallery.au`. That address needs working mail delivery before launch.

Options:

- Use GoDaddy email if it was purchased with the domain.
- Use Cloudflare Email Routing to forward `admin@fishermansgallery.au` to an existing mailbox.
- Use Google Workspace or Microsoft 365 and add their MX, SPF, DKIM and DMARC records in Cloudflare.

Do not switch nameservers away from GoDaddy until any required mail records are recreated in Cloudflare.

## Pages CMS

The `.pages.yml` file lets Pages CMS edit homepage copy and image uploads after the GitHub repository exists.

1. Authorize Pages CMS for the GitHub repository.
2. Open `https://app.pagescms.org/`.
3. Select the repository and `main` branch.
4. Edit homepage content and media.
