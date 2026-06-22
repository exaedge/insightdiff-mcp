# Setup And Safety

## Client Config

Use a dedicated API key per MCP client. The key starts with `pv_live_...`.
Store it in the MCP client config, not in prompts or tool arguments.

```json
{
  "mcpServers": {
    "insightDiff": {
      "url": "https://insightdiff.exaedge.ai/mcp",
      "headers": { "Authorization": "Bearer <YOUR_API_KEY>" }
    }
  }
}
```

## Key Handling

- Create keys from authenticated Settings/API-key UI or `POST /api/keys`.
- Copy the raw key once; it is not shown again.
- Revoke stale keys with `DELETE /api/keys/:id`.
- Active-key and credit limits are the enforcement boundary.

## Safety Rules

- MCP auth key is client auth; target-site auth is per screenshot call.
- Do not pass sensitive target-site credentials to pages with untrusted third
  party subresources unless the user explicitly accepts that risk.
- Target-site auth is not persisted in reports.
- Private/internal IP ranges are blocked by screenshot URL validation.
- `compare_pages` accepts only PNG/JPEG base64, with or without data URL prefix.

## Disabled From MCP

Do not call or mention as available: `estimate_credits`, `submit_feedback`,
`analyze_html_scopes`, webpage archive capture, billing/admin/contact/testimonial
automation, or API-key management through MCP.
