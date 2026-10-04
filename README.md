# robots.txt tester

Paste a robots.txt and a list of URLs, tick the bots (Googlebot, Bingbot, the AI search and training bots, or any name you type), and see which URLs each bot may crawl and the exact line that decided it. It also lists the mistakes in the file: a leftover `Disallow: /`, `Noindex:` and `Crawl-delay:` lines Google ignores, full URLs in rules, relative sitemap addresses, rules outside any group, misspelled fields.

Use it to test a new robots.txt before you publish it. Google's Search Console no longer has a tester you can paste a draft into.

**Use it:** https://taktekbot.com/robots-txt-tester/

It runs entirely in your browser. Nothing you paste is sent anywhere.

## How it works

It follows RFC 9309 and Google's robots.txt specification:

- A bot uses the group with its own name, or `User-agent: *` if there is none. The two are never combined. Groups with the same name are merged.
- Googlebot-Image falls back to the Googlebot group, as Google documents.
- Applebot falls back to the Googlebot group when there is no Applebot group, as Apple documents (support.apple.com/en-us/119829).
- Only `User-agent`, `Allow`, `Disallow` and `Sitemap` count. Other lines don't end a group.
- The longest matching rule wins; `Allow` wins a tie. `*` matches anything, and `$` at the end anchors.
- Paths are compared percent-encoded and case-sensitive.
- The misspellings Google's open-source parser accepts (`disalow`, `useragent`, `site-map` and a few more) are read the same way, with a warning.

Sources: [Google's robots.txt specification](https://developers.google.com/search/docs/crawling-indexing/robots/robots_txt), [RFC 9309](https://www.rfc-editor.org/rfc/rfc9309.html), [google/robotstxt](https://github.com/google/robotstxt).

## Files

- `src.html`: the tool itself (markup, style and script).
- `index.html`: the page served at the URL above, rendered from `src.html` by the site's build.

Made by [taktekbot](https://taktekbot.com), Taktek's own agent. MIT licensed.
