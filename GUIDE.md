# Firecrawl Setup — setup (Claude reads this)

**You are Claude. The user dragged this in and asked you to set it up. Do it FOR them, one step at a time, in plain language. Never paste a raw error at them.**

**The golden rule: the key is THEIRS and it must never land in this chat.** They paste it into the `.env` file in this folder. The setup script reads that file in the shell and hands it to Claude Code, so you never see it. Don't `cat` the `.env`, don't echo the key back, don't commit it. If they ask where it ends up: their own `~/.claude.json`, on their machine only.

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
2. **Have them put the key in `.env`, not in this chat.** Say: *"Open the file called `.env` in this folder, paste your key after `FIRECRAWL_API_KEY=`, save it, and tell me you're done. Don't paste it here."* If there's only a `.env.template`, tell them to copy it to `.env` first. `KEYS.md` spells the same thing out for them.
3. When they say they're done, run the setup script. It reads `.env` **in the shell**, so the key goes straight from the file into Claude Code and never enters this conversation:

```bash
# macOS / Linux
bash setup-keys.sh
```

```powershell
# Windows
powershell -ExecutionPolicy Bypass -File setup-keys.ps1
```

   It prints `✅ firecrawl connected` when it worked, and only ✅ / ⬜ per key otherwise. Never the key itself.

4. Confirm it registered: `claude mcp list` should show **firecrawl**.

> **Manual fallback, only if the script can't run at all.** Don't run this yourself with their key in it; that puts the key in the transcript. Give them the line and have them run it in their own terminal, swapping in their key:
>
> ```bash
> claude mcp add firecrawl --scope user \
>   --env FIRECRAWL_API_KEY=PASTE_YOUR_KEY_HERE \
>   -- npx -y firecrawl-mcp
> ```
>
> `--scope user` makes it available in every project, not just one folder.

---

> ⚠️ **If you also ran `solnest-connectors-setup`, pick one.** That repo installs Firecrawl as a
> remote HTTP server under the same name (`firecrawl`), so whichever you run last silently replaces
> the other one. Run `claude mcp remove firecrawl --scope user` first if you want to switch.

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
