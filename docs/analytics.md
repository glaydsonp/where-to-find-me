# Analytics

The site uses [Umami](https://umami.is), self-hosted.

- Dashboard and script host: <https://umami.glaydsonp.com>
- Website ID: `c2598392-8190-4829-aa9d-4aaaee1693b0` (public; it is visible in the page source and is not a secret)

## Script tag

In the `<head>` of `index.html`:

```html
<script defer src="https://umami.glaydsonp.com/script.js" data-website-id="c2598392-8190-4829-aa9d-4aaaee1693b0" data-domains="glaydsonp.com"></script>
```

- `defer`: loads without blocking rendering.
- `data-website-id`: identifies the site in Umami.
- `data-domains="glaydsonp.com"`: Umami only reports from this domain, so local development and previews are not tracked.

## Measured automatically

Umami collects, without extra code: page views and visitors, referrer (traffic source), UTM parameters, country, device, browser and OS, and visit duration.

Note: on a single-page site Umami cannot infer time on page from navigation between pages, so duration is limited. The custom `time-on-page` event below fills that gap.

## Custom events

A small inline script at the end of `<body>` in `index.html` uses event delegation and calls `window.umami.track`.

| Event | Fires when | Properties |
| --- | --- | --- |
| `click` | Any `<a>` or `<button>` is clicked. | `text` (trimmed label, max 100 chars), `href`, `external` (`true` if the link leaves the site), `section` (heading or id of the closest section/header/footer) |
| `contact-click` | A `mailto:` or `tel:` link is clicked (in addition to `click`). | `type` (`mailto` or `tel`), `value` (address or number, query string removed) |
| `scroll-depth` | The visitor first reaches 25%, 50%, 75% and 100% of the page. Once per milestone. | `percent` (`25`, `50`, `75` or `100`) |
| `time-on-page` | The page is hidden or unloaded (`pagehide`, or `visibilitychange` to `hidden`). Once per visit. | `seconds` (rounded time since load) |

## Adblock behavior

If the Umami script is blocked (adblock, privacy extensions) `window.umami` is undefined. The tracking helper checks for it and wraps calls in `try/catch`, so it fails silently and never breaks the page. Those visits are simply not counted.

## Privacy

Umami does not use cookies and does not store personal data or track visitors across sites, so no cookie banner is needed for it. Event properties only contain interface information (labels, links, sections); do not add personal data to them.

## Testing

1. Open <https://glaydsonp.com> in a normal window (adblock off).
2. In the Umami dashboard open the site and go to **Realtime**.
3. Click buttons and links, click the e-mail link, scroll to the bottom, then switch tabs or close the page.
4. Check that `click`, `contact-click`, `scroll-depth` and `time-on-page` show up under **Events**.

In the browser DevTools Network tab you can also see the requests to `umami.glaydsonp.com`.

## Adding a new event

Call the helper defined in the inline analytics script:

```js
track('event-name', { key: 'value' });
```

Guidelines: use kebab-case names, flat and small properties, and no personal data. For a new interaction, prefer extending the existing delegated listener instead of adding per-element handlers.
