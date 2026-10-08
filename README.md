# mildreyruiz.com — Bilingual portfolio site

Personal portfolio of **Mildrey Ruiz** (director, director of photography, editor and web developer), live at **https://mildreyruiz.com**.

A fast, static, bilingual (Spanish / English) site that presents 14 lines of video work, selected cases, credentials and downloadable CVs. Designed, built and deployed end to end by me: UI/UX, front-end code, DNS and hosting.

> *Sitio estático bilingüe (ES/EN) con mi portfolio audiovisual y web. Diseño, desarrollo y despliegue propios.*

## Features

- **ES / EN language toggle** — every text node exists in both languages and is switched client-side.
- **14 reel categories** in four blocks (brand and story, music, events, vertical 9:16), each with an embedded poster image linking to the video.
- **Selected work** cases, a **credentials** block and downloadable **CV PDFs** (Spanish and English).
- **"On location" carousel** — auto-advancing, pause on hover, arrows and dots.
- **Responsive and touch-friendly** — audited at 390 px width: no horizontal overflow, enlarged touch targets on the carousel controls.
- **Social sharing and SEO metadata** — canonical URL, Open Graph and Twitter Card tags, `robots.txt` and `sitemap.xml`.

## Tech stack

- HTML5, CSS3 and vanilla JavaScript (no framework, no runtime dependencies).
- Google Fonts (Inter).
- Images embedded as base64 inside a single HTML file, so the page renders without extra requests.
- Small build step: a master HTML file is the single source of truth, and the published `index.html` is regenerated from it by injecting the social metadata block and font weights.

## Project structure

```
site/
├── index.html      # published page (generated from the master file)
├── og.jpg          # 1200×630 social-share image
├── robots.txt
├── sitemap.xml
└── CV_*.pdf        # downloadable CVs (ES / EN)
```

## Deployment and infrastructure

- **Hosting:** Cloudflare Workers with static assets.
- **DNS and HTTPS:** domain delegated to Cloudflare nameservers; custom domain attached to the Worker; HTTPS enforced.
- **Domain registration:** managed through WordPress.com, with Cloudflare as the DNS provider.
- **Redeploy:** upload the `site/` folder to the Worker.

Lessons learned during setup (documented so I don't repeat them):

1. Create the hosting site **before** pointing DNS at it, otherwise the provider returns "site not found".
2. An apex (root) domain on a Cloudflare Worker requires the zone to be on Cloudflare nameservers.
3. Add the **root** domain only; `www` follows the apex automatically.
4. After a nameserver change, a stale local DNS cache can hide a site that is already live worldwide. Check the browser's secure-DNS setting first.

## Known limitations and roadmap

- The page is a single ~2.6 MB file; on mobile data the whole file downloads before first paint. Planned: move images to separate files with lazy loading.
- Deployment is manual (folder upload). Planned: version-controlled deploys from this repository with an automated pipeline.
- Mobile header drops the section navigation. Planned: a compact menu.

## Development notes

Built with an AI-assisted workflow (Claude) for drafting and review; design decisions, copy, structure, verification and deployment are mine.

## License

© Mildrey Ruiz. All rights reserved. The code is published for reference; images, videos and text are not licensed for reuse.
