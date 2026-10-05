---
"schema_version": 2
"thread_id": "01M466ZDBPTY0PG9JCGVKTMNR7"
"title": "Run ThreadVault locally for testing"
"slug": "run-threadvault-loca"
"account": "default"
"client": "claude-desktop"
"model": ""
"created": "2026-10-05T14:20:09.974661+00:00"
"updated": "2026-10-05T14:46:55.877752+00:00"
"page": 1
"prev": null
"next": null
"turn_count": 8
"turn_range":
- 1
- 0
"bytes": 3099
"gaps": []
"redacted": false
"tags": []
"open_turn": 4
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

<!-- turn i=2 role=assistant fidelity=verbatim chars=1842 hash=49f6fd73 nonce=4968 -->
## Claude

That error is expected. claude.ai only accepts public HTTPS URLs, and `127.0.0.1` is only reachable from your own computer. The fix is a tunnel, which gives your local server a temporary public `https://` address. I checked and neither `cloudflared` nor `ngrok` is installed on your machine. I recommend `cloudflared` because it needs no account.

**1. Install it (once)**
```powershell
winget install Cloudflare.cloudflared
```
Then close and reopen the terminal so the command is found.

**2. Start the server (terminal 1)**
```powershell
cd "d:\Dev Projects\2026\eoxs\thread save"
powershell -File scripts\run_local.ps1
```

**3. Start the tunnel (terminal 2)**
```powershell
cloudflared tunnel --url http://127.0.0.1:8000
```
It prints a URL like `https://random-words.trycloudflare.com`.

**4. Add the connector**

In the dialog, use `https://random-words.trycloudflare.com/mcp`. Keep the `/mcp` at the end.

**5. Check your saves**

Chat in claude.ai, then look in `vault_local\default\...` for the markdown files.

- **The URL changes on each run.** If you restart the tunnel, you'll need to edit the connector with the new URL. Leave the tunnel running while you iterate. The server auto-reloads, so code edits don't need a tunnel restart.
- **The tunnel is open to the internet.** Local auth is turned off, so anyone who has the URL could write to your test vault. The URL is random and short-lived, so this is fine for testing. Close the tunnel when you're done.
- **Turn off the Render connector** while you test, so saves don't go to both places.
- **Two connectors with the same tools:** your `thread2` connector will expose the same tool names as the Render one, so disabling the other avoids confusion.

If you'd rather use `ngrok`, it works the same way (`ngrok http 8000`), but it requires a free account and authtoken first.
<!-- /turn i=2 nonce=4968 -->

---

<!-- turn i=3 role=user ts=2026-10-05T14:41:15.966740+00:00 fidelity=verbatim chars=91 hash=fe73e0f2 anchor="like i just wanted to run it locally, li" turn_key=6df5dc798164737629474ca40971b5ab644b4ac1b2ddf3055e6db98bb13a237c nonce=4968 -->
## User

like i just wanted to run it locally, like as studio way, so why installing these packages?
<!-- /turn i=3 nonce=4968 -->

---

<!-- turn i=3 role=assistant fidelity=verbatim chars=2288 hash=f516145e nonce=4968 -->
## Claude

You don't need a tunnel or any extra install. The tunnel was only for claude.ai in the browser, which only accepts `https://` URLs. The simpler way is to connect Claude Desktop directly to your local code (stdio mode). It runs as a program on your computer, with no server, URL or Render involved.

I tested this mode: starting the server through stdio and saving a turn worked, and it wrote the markdown file. I deleted that test folder afterwards.

## Set it up (one time)

1. Open Claude Desktop, then **Settings → Developer → Edit Config**. This opens `claude_desktop_config.json`.
2. Add this inside it. It's the same as your claude_desktop_config.example.json, with a separate test folder:
   ```json
   {
     "mcpServers": {
       "threadvault-local": {
         "command": "C:\\Python314\\python.exe",
         "args": ["-m", "thread_save.server"],
         "env": {
           "THREAD_SAVE_VAULT_ROOT": "D:\\Dev Projects\\2026\\eoxs\\thread save\\vault_local",
           "THREAD_SAVE_ACCOUNT": "dhanshree"
         }
       }
     }
   }
   ```
   If the file already has other servers, add only the `threadvault-local` block inside the existing `mcpServers`.
3. Fully quit Claude Desktop (including the tray icon) and reopen it.
4. Start a chat. The `vault_save_turn` tool should appear under the tools list. Then check `vault_local\dhanshree\...` for the saved files.

## How it works day to day

- **Code changes:** Claude Desktop starts a fresh copy of your code each time it launches. After you edit the code, restart Claude Desktop to pick it up.
- **Render:** keep the Render connector off in Desktop while you test, so saves don't go to both places.
- **No GitHub sync:** the stdio mode never pushes to GitHub, so there is nothing to worry about there.
- **Differences from Render:** stdio skips the web layer (OAuth, viewer links, GitHub sync loop). It tests the core saving logic, which is the part you wanted to check. To test the exact Render web path, you'd need the HTTP server and a tunnel after all.

If you only use Claude Code, `claude mcp add threadvault-local -- C:\Python314\python.exe -m thread_save.server` does the same thing, and you can skip the Desktop config. Setting this up in Claude Desktop is your choice, so I haven't touched that config file.
<!-- /turn i=3 nonce=4968 -->

---

<!-- turn i=4 role=user ts=2026-10-05T14:46:55.877618+00:00 fidelity=verbatim chars=31 hash=3e6b5f9c anchor="why dhanshree? word in account?" turn_key=07cf3085a632f0ebb11d3a66df26645185ce04d950d66dcdd3e31fab97578738 nonce=4968 -->
## User

why dhanshree? word in account?
<!-- /turn i=4 nonce=4968 -->

---

<!-- turn i=4 role=assistant fidelity=open chars=48 hash=af50fba6 nonce=4968 -->
## Claude

[response pending — will be filled on next turn]
<!-- /turn i=4 nonce=4968 -->
