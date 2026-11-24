# www: the CCDPS landing page

Source of <https://ccdps.plateau-de-saclay.net/>, the landing page of the
Centre de Calcul et de Données du Plateau de Saclay (CCDPS), accredited by the
DGRI. The service cards link to the `*.mesocentre.plateau-de-saclay.net` hosts,
set by `params.domain`. The visible title is `title` (fr) and
`languages.en.title` in `config/_default/hugo.toml`.

- Hugo **v0.167.0 extended** (needed for WebP encoding), pinned. No theme, no
  module, no external font, script or CDN.
- Bilingual: French at `/` (default), English at `/en/`. Strings are in
  `config/_default/hugo.toml`.
- The background is `assets/plateau-saclay.jpg` (2640x1592, JPEG quality 90).
  Hugo makes WebP and JPEG at 800, 1600 and 2400 px (`<picture>` + `srcset`);
  the source itself is never served.
- Image credit: IGN orthophoto from Géoportail, Licence Ouverte Etalab 2.0. It
  is one Markdown param per language, `credit`, in `config/_default/hugo.toml`.
  The repository licence covers the code, not this image.

## Build

    hugo --minify --gc                        # production, into public/
    hugo --minify --gc --environment staging  # staging names

## Deploy

The page is served by Caddy from `/var/www/ccdps` (root:root, 0755). The Caddy
site block, with its strict CSP and HSTS, and the staging provisioning live in
the deployment repository, not here. Production: build, copy `public/` to
`/var/www/ccdps` keeping a `.previous`, `caddy validate`, `systemctl reload caddy`.
