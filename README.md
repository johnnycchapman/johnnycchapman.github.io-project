# On the Hour

**One page. Fifty outlets. Every hour, on the hour.**

A lightweight news aggregator that pulls the top headline and summary from 50 major news organizations around the world and displays them in a single, clean, newspaper-inspired grid. The page refreshes at the top of every clock hour — no infinite scroll, no algorithmic feed, no ads.

Built to be read like a front page, not doomscrolled.

---

## What it does

- Pulls the **top story** from each of 50 news outlets' public RSS feeds
- Shows the headline, a scrollable summary, the publish timestamp, and a direct link to the original article
- Refreshes automatically **at the top of every hour** (3:00, 4:00, 5:00…) with a live countdown to the next edition
- Manual refresh button if you can't wait
- Works as a single static HTML file — no build step, no backend, no database

## The outlets

Fifty English-language news sources across global, regional, and political perspectives, including:

- **Wire services:** Reuters, Associated Press
- **UK:** BBC, The Guardian, Financial Times, The Times, The Telegraph, Sky News
- **US:** New York Times, Washington Post, Wall Street Journal, CNN, NBC, CBS, ABC, Fox News, NPR, USA Today, Politico, The Atlantic, Bloomberg, Axios, The Hill
- **Europe:** Der Spiegel, Deutsche Welle, France 24, Le Monde, El País, ANSA, Euronews, Politico EU, The Local
- **Middle East:** Al Jazeera, Haaretz, Times of Israel
- **Asia-Pacific:** NHK World, Japan Times, South China Morning Post, Xinhua, Straits Times, The Hindu, Times of India, Hindustan Times, Dawn
- **Russia/Ukraine:** The Moscow Times, Kyiv Independent
- **Americas/Oceania/Africa:** CBC, Globe and Mail, ABC Australia, AllAfrica

## How it works

The site is a single HTML file. On load (and every hour after), it fetches each outlet's RSS feed in parallel batches via [rss2json.com](https://rss2json.com), extracts the top item, strips HTML tags from the summary, and renders it as a card. All rendering is client-side — there's no server.

**Tech:**
- Pure HTML, CSS, and vanilla JavaScript — no frameworks
- Google Fonts: *Fraunces* (serif) and *JetBrains Mono* (monospace)
- Inline SVG favicon — no extra assets to host

## Design

The aesthetic borrows from print newspaper conventions: cream paper color, ink-black text, a double-rule masthead, monospace typographic credits, and an italicized masthead wordmark. Accent red for the live indicator and the clock hand in the favicon. Each card is a self-contained clipping with its own scrollable body so long summaries don't break the grid.

## Running it locally

Just open `index.html` in any modern browser. That's it.

```bash
# or serve it with any static file server if you prefer:
python -m http.server 8000
# then visit http://localhost:8000
```

## Deployment

Deployed as a static site. Any static host works — GitHub Pages, Cloudflare Pages, Netlify, Vercel. No build command, no environment variables, no secrets.

## Known limitations

- **Some feeds occasionally fail** (rate limiting, outlet-side outages, format changes). Cards that fail show a "Feed Unavailable" label and fall back to a direct link to the outlet.
- **Iframes weren't used** because most major news sites block embedding via `X-Frame-Options` / `Content-Security-Policy` headers. RSS + Open Graph data is the most reliable approach.
- **Free tier of rss2json** caps requests — if the site sees heavy traffic, the next step is to swap in a Cloudflare Worker that parses RSS server-side and caches results in KV.

## Roadmap ideas

- Pull Open Graph images from each article for richer cards
- Server-side RSS parsing via Cloudflare Worker for better reliability
- User-selectable outlet subsets ("just US," "just international," etc.)
- Light/dark mode toggle
- Sparkline of how many times a story has been syndicated across outlets (shared narrative detection)

## License

MIT — do whatever you want with it.

Headlines and summaries remain the property of their respective publishers and are displayed under the normal expectations of RSS syndication. All article links go directly to the original publisher.
