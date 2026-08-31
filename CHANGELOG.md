# Changelog

## 1.1.0

- **Fixed: the guide and the setup script disagreed about your API key.** `START-HERE.md` said never
  put a key in the chat and pointed at `.env` + `setup-keys.sh`; `GUIDE.md` handed out a
  `claude mcp add --env FIRECRAWL_API_KEY=...` line instead and never mentioned the script. `GUIDE.md`
  now uses the `.env` + script path, with the raw command kept only as a labelled manual fallback.
- Added a warning that `solnest-connectors-setup` installs Firecrawl a different way under the same
  server name, so running both silently replaces one with the other.
- `.env.template` and `KEYS.md` used `EXA_API_KEY` as the worked example. They use `FIRECRAWL_API_KEY` now.

## 1.0.0

- First public release.
