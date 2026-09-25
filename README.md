# Yansheng Mao's Homepage

Personal website of Yansheng Mao ([LuckyGlass](https://github.com/LuckyGlass)), live at
<https://luckyglass.github.io>.

Built with [Jekyll](https://jekyllrb.com/) and the
[al-folio](https://github.com/alshedivat/al-folio) theme (v0.16.3), with a custom
Fuwari-inspired blog page (`_pages/blog.md` + `_sass/_fuwari.scss`).

## Where things live

| What                | Where                                              |
| ------------------- | -------------------------------------------------- |
| Site settings (name, email, blog description) | `_config.yml`       |
| Bio / home page     | `_pages/about.md`                                  |
| CV                  | `_data/cv.yml` (rendered by `_pages/cv.md`)        |
| Publications        | `_bibliography/papers.bib` (BibTeX)                |
| Blog posts          | `_posts/` (filename format: `YYYY-MM-DD-title.md`) |
| Social links        | `_data/socials.yml`                                |
| Profile photo       | `assets/img/prof_pic.jpg`                          |

## Running locally

With Docker (recommended on Windows):

```bash
docker compose up
```

then open <http://localhost:8080>. Alternatively install Ruby + Bundler and run
`bundle install && jekyll serve` (see `INSTALL.md`).

## Deploying

The site is built and deployed by the GitHub Actions workflow in
`.github/workflows/deploy.yml` (required, because al-folio uses plugins that plain
GitHub Pages builds do not allow). In the repository settings, Pages must be set to
build via **GitHub Actions**, not "Deploy from a branch".

## Credits

- Theme: [al-folio](https://github.com/alshedivat/al-folio) (MIT license, see `LICENSE`).
- Blog page styling inspired by [Fuwari](https://github.com/saicaca/fuwari).
