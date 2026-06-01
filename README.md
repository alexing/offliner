# offliner

An **offline and private** viewer for your X (Twitter) archive — a memory chest
to open today and ten years from now. A single `index.html`, no build, no
dependencies, no network. Open it with a double click and you're done.

> Also designed to add your **Facebook** archive later on. Hence the name: what
> you downloaded from social media, to view it *offline*.

## Why

The official X export is a `.zip` full of thousands of `.js` files and an ugly,
limited viewer. `offliner` turns it into something pleasant to inhabit: you browse
through **eras** (year by year), it rebuilds your **threads**, shows you **stats**,
**"on this day"**, your **likes**, all with filters and search — without a single
byte leaving your machine.

## Privacy (the most important part)

- **100% client-side, zero network.** No analytics, no telemetry, no external
  requests. A CSP (`connect-src 'none'`) blocks fetch/XHR/websockets.
- **Your data is never versioned.** The `data/` folder is in `.gitignore`: your
  personal archive stays on your disk, never on GitHub.
- System fonts (no CDNs). Works with real `file://`, no server needed.

## How to use it

1. Download your X archive: *Settings → Your account → Download an archive of your data*.
2. Unzip it. You'll get a folder like `twitter-2026-05-31-abc123…/`.
3. Move it into `data/` and rename it to **`twitter`** (so it becomes `data/twitter/`,
   with its `Your archive.html`, `assets/` and `data/` inside).
   - If you prefer a different name/location, change the `EXPORT_ROOT` constant at
     the very top of `index.html`.
4. Open **`index.html`** with a double click.

```
offliner/
├── index.html          ← the viewer (the only thing versioned as code)
├── README.md
├── .gitignore
└── data/               ← your archives (ignored by git)
    └── twitter/        ← your X export goes here
        ├── Your archive.html
        ├── assets/
        └── data/       ← manifest.js, tweets.js, tweets_media/, …
```

## What it does

- **Tweets** — chronological timeline with **year dividers** and an era strip to
  jump around; ascending/descending order; filters by year/month, type
  (own/replies/RTs), with media and with location; full-text search (includes the
  domains of the links).
- **Threads** — rebuilds your *self-threads* by chaining together replies to
  yourself that are inside the archive.
- **On this day** — anniversaries by month-day, with a date picker.
- **Likes** — the list of your likes with their text (it honestly marks the ones
  the archive doesn't include).
- **Stats** — totals, tweets per year, top by favorites/RTs, most used hashtags
  and mentions.
- **Local media** — photos, videos and gifs served from your own archive.
- **Permalinks** per tweet (with `Esc`/click outside to close).

## Honesty about the limits

The export only has **your side**. `offliner` never invents what isn't there:

- **Replies to others** show your tweet and mark that the original isn't in the
  archive (with a "view on X" link in case you want to open it online).
- **Retweets** show the text as-is (sometimes truncated with `…`); the original
  isn't embedded.
- **Quotes** link to the quoted tweet but warn that it isn't in the archive.

## Roadmap

- [ ] **Facebook** module (`data/facebook/`), reusing the same core.

## Credits

Inspired by the idea of [ronilaukkarinen/tweets](https://github.com/ronilaukkarinen/tweets).
The X export format is documented in `RECON.md` (local, not versioned).

Personal use.
