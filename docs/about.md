# About the site

## Purpose

A one-page personal site that presents Glaydson Prado, Tech Lead & Full-Stack Developer (mobile, backend and cloud infrastructure), and points visitors to the portfolio, résumé and contact channels.

## Sections

| Section | Anchor | Content |
| --- | --- | --- |
| Home | `#inicio` | Name, role and a short lead paragraph, with links to portfolio and résumé. |
| About (`sobre.md`) | `#sobre` | Short bio, team leadership summary, education and location. |
| Stack (`stack.json`) | `#stack` | Technologies rendered as a JSON snippet: mobile, backend, data, messaging, infra. |
| Portfolio | `#portfolio` | Three placeholder project cards, marked as "coming soon". |
| Résumé (`curriculo.md`) | `#curriculo` | Résumé PDF button (disabled until the PDF exists) and a LinkedIn link. |
| Contact (`contato.json`) | `#contato` | E-mail, GitHub and LinkedIn as a JSON snippet and as a list of links. |

## Features

- **Language switch (PT/EN).** All visible texts live in the `I18N` object inside `index.html` and are applied through `data-i18n` attributes. The language comes from the `?lang=pt|en` query string, then from `localStorage`, then from the browser language. Changing it updates `<html lang>`, the title, the meta description and the URL.
- **Mobile menu.** On small screens the navigation becomes an "explorer" panel (dialog with `aria-modal`), closable with a button, the Escape key or by choosing a link; focus is moved in and out of it.
- **Active section tracking.** An `IntersectionObserver` updates `aria-current` on navigation links and the active editor tab while scrolling.
- **Accessibility.** Skip link, visible focus outline, ARIA labels (also translated), `prefers-reduced-motion` support for smooth scrolling and the blinking cursor.
- **SEO and sharing.** Canonical URL, `hreflang` alternates for `pt-BR`/`en`, Open Graph tags, theme color and an inline SVG favicon.
- **Analytics.** Umami script plus custom events; see [analytics.md](analytics.md).

## Technologies

HTML5, CSS (custom properties, grid/flexbox) and vanilla JavaScript, all in one file. Fonts: JetBrains Mono and Inter from Google Fonts. No build tooling and no dependencies.

## Design decisions

- **Code-editor theme.** The page mimics an IDE: dark palette defined as CSS variables, editor tabs, a line-number gutter on the hero, section titles as file names (`sobre.md`, `stack.json`) and code-style comments. There is a single dark theme; no theme switcher exists.
- **Single file.** Keeping everything in `index.html` makes deployment trivial (static hosting, no build) and the whole site easy to audit.
- **No frameworks.** The site is small enough that vanilla JS is simpler, faster and has nothing to maintain.
- **Resilient enhancements.** `localStorage` and analytics calls are wrapped in `try/catch`, so the page works when storage or tracking is blocked.
