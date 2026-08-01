# Install Relex for Gemini

**MCP URL:**

```
https://relex.legal/api/mcp
```

## Gemini CLI (personal / developer)

1. Install and sign into [Gemini CLI](https://geminicli.com/).
2. Add Relex:

   ```bash
   gemini mcp add --transport http relex https://relex.legal/api/mcp
   ```

3. Verify:

   ```bash
   gemini mcp list
   ```

4. Authenticate:

   ```text
   /mcp auth relex
   ```

   Browser opens → Relex OAuth (Google/Apple).

5. Prompt:

   > Set up my practice workflow with Relex

API-key fallback:

```bash
gemini mcp add --transport http \
  --header "Authorization: Bearer rlx_..." \
  relex https://relex.legal/api/mcp
```

Create the key in Relex → **Settings → API Keys**.

## Gemini Enterprise / Team (admin vs member)

### Admin

1. Confirm network egress to `https://relex.legal` is allowed.
2. In Gemini Enterprise (or Vertex AI Agent Builder / custom MCP data store),
   create a **Custom MCP Server** pointing at `https://relex.legal/api/mcp`.
3. Configure OAuth per Google’s custom MCP documentation (redirect URLs, client
   registration with your IdP if required).
4. Grant the application to the right users/groups.
5. Tell members Relex is available in the Enterprise app — they only need to
   approve / sign in when prompted.

### Member

1. Open the Gemini Enterprise application your admin published.
2. If prompted, **Connect** / sign in to Relex (your own account).
3. You generally **cannot** add a new custom MCP URL yourself in a locked-down
   Enterprise tenant. If tools are missing, contact your admin.

| Symptom | Fix |
|---------|-----|
| `gemini mcp add` forbidden / no effect in managed env | Use Enterprise app path; ask admin |
| Connected but 401 | Re-run `/mcp auth relex` or refresh API key |
| Tools not listed | `gemini mcp list`; check name `relex` and transport `http` |

## After connect

1. PII password (browser deep link)
2. Know-how
3. Encrypted parties (counts only)
4. First case

Skills in `plugin/skills/` teach Gemini the PII-safe workflow — load as project
context or agent instructions when useful.
