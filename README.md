# tour body plugin

Connect Codex, ChatGPT and Claude Code to your [tour body](https://tour.foreignbody.app) account. tour body is foreign body's tour management app for artists, tour managers and crew.

Your agent can read your tours: schedule days, members and their roles, flights, trains, hotel stays, document titles and reviewed details imported from tour documents. After you approve a change, it can create a tour, update tour details and add or edit flights, trains and hotel stays. It can't delete anything, invite people, send messages or make payments.

## What's in this repository

- `plugins/tour-body/`: the plugin. It contains the `tour-body` MCP server connection (`https://tour.foreignbody.app/mcp`, Streamable HTTP) and the `tour-body` skill, which reads before writing, asks you before saving and keeps flight times in each airport's local time.
- `.agents/plugins/marketplace.json`: the Codex and ChatGPT marketplace.
- `.claude-plugin/marketplace.json`: the Claude Code marketplace.

## Before you connect

- You need a tour body account with PRO. Accounts without PRO can't approve a connection, and the tools reply that PRO is required.
- You sign in on tour.foreignbody.app and approve the connection. Each connection reaches only your own account: the tours you can see in the app. Your client keeps the sign-in, and tour body never shows you tokens.

## Install in Codex

```bash
codex plugin marketplace add foreign-body/tour-body-mcp
```

Then open `/plugins` in Codex, choose the tour body marketplace and install tour body. Sign in to tour body and allow access when asked.

## Install in Claude Code

```text
/plugin marketplace add foreign-body/tour-body-mcp
/plugin install tour-body@tour-body
```

Then run `/mcp`, select the tour body server and choose Authenticate.

## Connect without the plugin

Every client uses the same server URL, `https://tour.foreignbody.app/mcp`, and the same tour body sign-in.

- **Claude (claude.ai and Claude Desktop):** Customize > Connectors > Add > Add custom connector (older versions: Settings > Connectors). Name it `tour body`, enter the URL, then Connect, sign in to tour body and select Allow. Custom connectors need a paid Claude plan (Pro, Max, Team or Enterprise); on Team and Enterprise an owner first adds it under Organization settings > Connectors. The Claude mobile apps can use a connector but can't add one.
- **Claude Code:** run `claude mcp add --transport http tour-body https://tour.foreignbody.app/mcp`, then run `/mcp` in Claude Code, choose `tour-body` and select Authenticate.
- **Codex** (the CLI, the IDE extension and Codex in the ChatGPT desktop app share this setup): run `codex mcp add tour-body --url https://tour.foreignbody.app/mcp`, then `codex mcp login tour-body` and sign in in the browser window that opens. To disconnect, run `codex mcp logout tour-body`.
- **ChatGPT:** a tour body listing in the ChatGPT and Codex plugin directory is coming soon. Until then, if your ChatGPT plan and workspace allow custom MCP servers, go to chatgpt.com/plugins, select + > Add custom MCP server, enter the URL, sign in and select Create as a plugin. Which plans can add one, and whether it can make changes, depends on your ChatGPT plan; see the guide.

## Manage or end a connection

See and end each AI connection in tour body on the web under Account > AI connections (https://tour.foreignbody.app/settings/ai). The app loses access within about a minute.

## Links

- Guide: https://tour.foreignbody.app/guide/ai
- Support: https://tour.foreignbody.app/support
- Privacy policy: https://tour.foreignbody.app/privacy
- Terms: https://tour.foreignbody.app/terms

## Maintaining

The plugin carries the same identity and listing in three manifests: `plugin.json` with `mcp.json` (portable Agent Plugins format), `.codex-plugin/plugin.json` with `.mcp.json` (read by current Codex builds), and `.claude-plugin/plugin.json` (Claude Code, which also reads `.mcp.json`). Change them together, including the version.
