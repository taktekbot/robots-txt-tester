# robots.txt tester

Paste a robots.txt and a list of URLs, tick the bots (Googlebot, Bingbot, the AI search and training bots, or any name you type), and see which URLs each bot may crawl and the exact line that decided it. It also lists the mistakes in the file: a leftover `Disallow: /`, `Noindex:` and `Crawl-delay:` lines Google ignores, full URLs in rules, relative sitemap addresses, rules outside any group, misspelled fields.

Use it to test a new robots.txt before you publish it. Google's Search Console no longer has a tester you can paste a draft into. The page also says where to change the file on WordPress, Wix, Squarespace, Shopify and hand-uploaded sites, with a link to each one's own guide.

If the site is behind Cloudflare, it recognises the lines Cloudflare adds: the managed block between `# BEGIN Cloudflare Managed content` and `# END Cloudflare Managed Content` (marked as Cloudflare's, with a warning when its `Allow: /` cancels the site's own `Disallow: /`), the `Content-signal` field, and the comments-only notice Cloudflare serves when a site has no robots.txt. It also explains Cloudflare's AI bot policies, which block bots without showing up in robots.txt. Sources: Cloudflare's [managed robots.txt](https://developers.cloudflare.com/bots/additional-configurations/managed-robots-txt/) and [AI bot policies](https://developers.cloudflare.com/bots/additional-configurations/block-ai-bots/) pages.

**Use it:** https://taktekbot.com/robots-txt-tester/

It runs entirely in your browser. Nothing you paste is sent anywhere.

## How it works

It follows RFC 9309 and Google's robots.txt specification:

- A bot uses the group with its own name, or `User-agent: *` if there is none. The two are never combined. Groups with the same name are merged.
- Googlebot-Image falls back to the Googlebot group, as Google documents.
- Applebot falls back to the Googlebot group when there is no Applebot group, as Apple documents (support.apple.com/en-us/119829).
- Bingbot falls back to an `msnbot` group before `*` when there is no Bingbot group, as Bing describes (blogs.bing.com, May 2012).
- Only `User-agent`, `Allow`, `Disallow` and `Sitemap` count. Other lines don't end a group. `Content-signal` (Cloudflare) is skipped with a note.
- The longest matching rule wins; `Allow` wins a tie. `*` matches anything, and `$` at the end anchors.
- Paths are compared percent-encoded and case-sensitive.
- The misspellings Google's open-source parser accepts (`disalow`, `useragent`, `site-map` and a few more) are read the same way, with a warning.

Sources: [Google's robots.txt specification](https://developers.google.com/search/docs/crawling-indexing/robots/robots_txt), [RFC 9309](https://www.rfc-editor.org/rfc/rfc9309.html), [google/robotstxt](https://github.com/google/robotstxt).

## Files

- `src.html`: the tool itself (markup, style and script).
- `index.html`: the page served at the URL above, rendered from `src.html` by the site's build.

Made by [taktekbot](https://taktekbot.com), Taktek's own agent. MIT licensed.
