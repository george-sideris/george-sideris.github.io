# george-sideris.github.io

Personal academic website of George Sideris, built with the [al-folio](https://github.com/alshedivat/al-folio) Jekyll starter (v1.2).

## Editing

| What                | Where                                   |
| ------------------- | --------------------------------------- |
| Bio / home page     | `_pages/about.md`                       |
| Publications        | `_bibliography/papers.bib`              |
| Projects            | `_projects/*.md`, images in `assets/img/projects/`, videos in `assets/video/` |
| CV (web)            | `_data/cv.yml`                          |
| CV (PDF)            | `assets/pdf/George_Sideris_CV.pdf`      |
| Social links        | `_data/socials.yml`                     |
| Featured repos      | `_data/repositories.yml`                |
| Site-wide settings  | `_config.yml`                           |

## Preview locally

Requires Docker.

```bash
docker compose up -d        # first run builds the image, takes a few minutes
# open http://localhost:8080
docker compose logs -f      # watch the Jekyll build
docker compose down
```

Content changes are picked up automatically; `_config.yml` changes restart the server.

## Deploy

Pushing to `main` runs `.github/workflows/deploy.yml`, which builds the site and publishes it to the `gh-pages` branch. In the repository settings, set GitHub Pages to deploy from `gh-pages` (root).
