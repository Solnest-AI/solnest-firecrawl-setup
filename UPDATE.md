# UPDATE — Firecrawl Setup (Claude reads this)

**You are Claude. The user asked you to update this guide.**

**⚠️ The one thing that matters: DO NOT touch their API keys.** Their keys are already in their `~/.claude.json`. This update is only about the *guide*. Never rewrite, re-register, or re-prompt for a key they've already set up.

## Step 1 — Check the version

Compare `VERSION` here to their copy. Same? Tell them they're current and stop.

## Step 2 — Get the latest

```bash
git clone --depth 1 https://github.com/Solnest-AI/solnest-firecrawl-setup.git /tmp/solnest-firecrawl-setup-update
```

No `git`? Download `https://github.com/Solnest-AI/solnest-firecrawl-setup/archive/refs/heads/main.zip`.

## Step 3 — Replace their copy of the guide

Overwrite `GUIDE.md`, `README.md`, and `VERSION`. That's it.

**Do not re-run the setup.** If their MCP servers already work, a newer guide changes nothing for them. Run `claude mcp list` to check — if the servers are there, they're done.

## Step 4 — Tell them what changed

Two or three plain bullets from `CHANGELOG.md`, new version only.

> Updated to `X.Y.Z`. Your API keys and connected servers were not touched.
