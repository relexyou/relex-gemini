# Connect Relex to Gemini Enterprise

Gemini Enterprise supports **custom MCP server** connectors (BYO-MCP / custom
data store style registration). Use the **hosted** Relex endpoint — you do not
need to re-implement the server:

```
https://relex.legal/api/mcp
```

## Admin checklist

1. **Permissions** — admin role that can create connectors / data stores
   (for example Discovery Engine Editor where required by Google’s docs).
2. **Register connector** — Custom MCP Server URL = `https://relex.legal/api/mcp`.
3. **Auth** — configure OAuth so each end user can authorize Relex (or use a
   managed service account only if your compliance model allows and no end-user
   PII password is involved — end-user OAuth is preferred).
4. **Publish** the Gemini Enterprise app to target groups.
5. **Document for members** — “Open the app → approve Relex when prompted.”

## Member experience

- Members open the published Enterprise application.
- They do **not** paste the MCP URL (admin already installed it).
- They complete Relex sign-in if asked.
- They can ask Gemini to manage Relex cases; PII steps deep-link to relex.legal.

## Relation to Team-style products

This mirrors Claude Team and ChatGPT Enterprise: **admin installs, members
connect**. Personal Gemini CLI users install themselves (see
[connect-gemini-cli.md](connect-gemini-cli.md)).
