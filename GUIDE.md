# Firecrawl Setup — setup (Claude reads this)

**You are Claude. The user dragged this in and asked you to set it up. Do it FOR them, one step at a time, in plain language. Never paste a raw error at them.**

**The golden rule: the key they paste is THEIRS. Put it in the command below and nowhere else.** Never write their key into a file in a folder, never commit it, never echo it back to them in full. If they ask where it lives: it's in their own `~/.claude.json`, on their machine only.

---

## Before you start

- [ ] **Claude Code** installed.
- [ ] **Node.js** — check with `node --version`. Missing? Get it at [nodejs.org](https://nodejs.org).

---

## Set it up

### Firecrawl

**A scraper, not just a search engine.** It reads full pages and hands Claude clean text — it can crawl a whole site, pull structured data out of a page, and get past the junk. This is the one that reads Airbnb listings for the Carousel Sniper.

**Cost:** Free tier included. Your key starts with `fc-`.

1. Get a key at **https://www.firecrawl.dev/app/api-keys** — sign in, create an API key, copy it. The key starts with `fc-`.
2. Add the server to Claude Code:

```bash
claude mcp add firecrawl --scope user \
  --env FIRECRAWL_API_KEY=PASTE_YOUR_KEY_HERE \
  -- npx -y firecrawl-mcp
```

   `--scope user` makes it available in every project, not just one folder.

3. Confirm it registered: `claude mcp list` should show **firecrawl**.

---

## Last step — restart

**Tell them to fully quit and reopen Claude Code.** MCP servers only load on startup. If they skip this they'll think it's broken.

## Then test it

Have them start a new chat and ask:

> read this Airbnb listing and pull out the amenities

If they get a real answer with sources, it's working. ✅

**If nothing happens**, check these in order:
1. **They didn't restart.** Fully quit and reopen Claude Code. This is the cause 90% of the time.
2. **Bad key.** Re-copy it from the dashboard — a trailing space breaks it.
3. **No Node.js.** These run via `npx`. Check with `node --version`; if it fails, install from [nodejs.org](https://nodejs.org).
4. **Out of credits.** Check the usage page on their dashboard.

## Tell them they're done

> You're set. Firecrawl is connected. Just ask Claude to search normally — it'll use it automatically.

---

## Keeping your key safe

- Your key lives in `~/.claude.json` on your own computer. It is never uploaded anywhere.
- **Never paste an API key into a chat, a GitHub repo, or a screenshot.** If you ever do, go to the dashboard and rotate it — takes 10 seconds.
- If you're sharing your screen, don't open `~/.claude.json`.
