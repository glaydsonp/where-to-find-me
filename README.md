# where-to-find-me

Personal landing page of Glaydson Prado (Tech Lead & Full-Stack Developer): who I am, my stack, portfolio, résumé and contact links, styled like a code editor.

Live site: <https://glaydsonp.com>

## Stack

- A single static `index.html` (HTML, CSS and vanilla JavaScript inline, no build step, no frameworks).
- Served by nginx.
- Self-hosted Umami for analytics (see [docs/analytics.md](docs/analytics.md)).

## Project structure

```
.
├── index.html        # the whole site (markup, styles, scripts, PT/EN texts)
├── docs/
│   ├── about.md      # what the site is and how it is built
│   └── analytics.md  # Umami setup and custom events
├── .gitignore
└── README.md
```

## Running locally

Open `index.html` directly in a browser, or serve it over HTTP:

```sh
python3 -m http.server 8000
# then open http://localhost:8000
```

Note: the analytics script only reports for the `glaydsonp.com` domain (`data-domains`), so local visits are not tracked.

## Deployment

Pushing or merging to `main` triggers an automatic rebuild and redeploy of the site at <https://glaydsonp.com>. Work on a branch and open a pull request; merging it is the deploy.

## Documentation

- [docs/about.md](docs/about.md): purpose, sections, features and design decisions.
- [docs/analytics.md](docs/analytics.md): analytics, custom events and how to test them.
