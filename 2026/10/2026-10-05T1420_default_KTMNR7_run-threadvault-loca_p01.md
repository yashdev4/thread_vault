---
"schema_version": 2
"thread_id": "01M466ZDBPTY0PG9JCGVKTMNR7"
"title": "Run ThreadVault locally for testing"
"slug": "run-threadvault-loca"
"account": "default"
"client": "claude-desktop"
"model": ""
"created": "2026-10-05T14:20:09.974661+00:00"
"updated": "2026-10-05T14:34:39.013131+00:00"
"page": 1
"prev": null
"next": null
"turn_count": 4
"turn_range":
- 1
- 0
"bytes": 2056
"gaps": []
"redacted": false
"tags": []
"open_turn": 2
"paused": false
"nonce": "4968"
---


# Run ThreadVault locally for testing

---

<!-- turn i=1 role=user ts=2026-10-05T14:20:09.980827+00:00 fidelity=verbatim chars=394 hash=2e0615a3 anchor="ohkay, i wanted to make it run locally o" turn_key=2ec3760f8e81b5603a020974010f5a029b706e3de478ac00c0d9f8083576f9bf nonce=4968 -->
## User

ohkay, i wanted to make it run locally on my computer also to test its saving chat correctly or not , because i don't wanted to push every line of code multiple times and redeploye render again and parallely its already deployed too on render, so how to connect it locally on my computer and when i  feel its working properly then i would push the code on github and let render auto redeploy it
<!-- /turn i=1 nonce=4968 -->

---

<!-- turn i=1 role=assistant fidelity=verbatim chars=2532 hash=b17d3bb8 nonce=4968 -->
## Claude

The app runs locally, and a test save through it worked. I added [scripts/run_local.ps1](scripts/run_local.ps1) to start it. My test server is stopped, so the commands below start it fresh.

I ran the server on port 8765 and `/health` returned healthy. I then sent two `vault_save_turn` calls over MCP. Both succeeded and wrote a correctly formatted markdown file under `vault_local/`. That folder is gitignored, so it won't reach GitHub.

## Run it

```powershell
cd "d:\Dev Projects\2026\eoxs\thread save"
powershell -File scripts\run_local.ps1
```

- **Address:** the server is at `http://127.0.0.1:8000/mcp`.
- **Storage:** saved chats go to `vault_local\`, not your real vault.
- **Auto-reload:** the server restarts when you edit files in `src/`, so you don't need to restart it by hand.
- **Packages:** your `thread-save-mcp` package is already installed in editable mode, so your code edits are picked up.

## Connect a client to it

- **Claude Code** is the simplest option. Run this once:
  ```
  claude mcp add --transport http threadvault-local http://127.0.0.1:8000/mcp
  ```
- **Claude Desktop** can run the stdio version from [claude_desktop_config.example.json](claude_desktop_config.example.json). Point `THREAD_SAVE_VAULT_ROOT` at a test folder.
- **claude.ai (web or mobile)** only accepts public HTTPS URLs. To use it with your local server, run a tunnel such as `cloudflared tunnel --url http://localhost:8000` or `ngrok http 8000`. Add the tunnel URL plus `/mcp` as a custom connector. This is the only way to test the same path Render uses.

Disable the Render connector while you test locally. If both are on, Claude will call both and your saves will split between them.

## Things to know

- **No GitHub sync locally.** The script clears `GITHUB_TOKEN` so local test chats can't be pushed to your real `thread_vault` repo. The log still prints a "No GITHUB_TOKEN" warning, which is harmless.
- **No `.env` loading.** Nothing in the code reads your `.env`, so the script sets the variables itself.
- **File storage only.** This matches Render's current setup (`THREADVAULT_STORAGE_BACKEND=file`). To test the Postgres path you would need a local Postgres and `DATABASE_URL`.
- **Tests:** `pytest` runs the automated checks, and `scripts/cross_surface_test.py --url http://localhost:8000` runs the multi-device scenario against the local server.

When the local saves look right, push to GitHub and Render redeploys. The script isn't needed on Render, but it's untracked, so commit it if you want to keep it.
<!-- /turn i=1 nonce=4968 -->

---

<!-- turn i=2 role=user ts=2026-10-05T14:34:39.013006+00:00 fidelity=verbatim chars=191 hash=d77a8d7d anchor="this is what it is saying , it needs htt" turn_key=91665bfa4db86fb88a87bead8f401690434440eaa01af20a37903e682e9d673d nonce=4968 -->
## User

this is what it is saying , it needs https not http [Image: screenshot of Claude "Add custom connector" dialog with URL http://127.0.0.1:8000/mcp showing error "URL must start with https://"]
<!-- /turn i=2 nonce=4968 -->

---

<!-- turn i=2 role=assistant fidelity=open chars=48 hash=af50fba6 nonce=4968 -->
## Claude

[response pending — will be filled on next turn]
<!-- /turn i=2 nonce=4968 -->
