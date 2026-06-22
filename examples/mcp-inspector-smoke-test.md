# MCP Inspector Smoke Test

Run MCP Inspector:

```bash
npx @modelcontextprotocol/inspector
```

In the Inspector UI:

1. Select `Streamable HTTP`.
2. Enter `https://insightdiff.exaedge.ai/mcp`.
3. Add header `Authorization: Bearer <YOUR_API_KEY>`.
4. Connect.
5. Call `get_mcp_help`.
6. Read `insightdiff://usage/monthly`.
7. Read `insightdiff://rate-limit/status`.

Expected:

- `get_mcp_help` returns the InsightDiff MCP quickstart.
- Usage and rate-limit resources return JSON scoped to the authenticated user.
- No response includes the raw API key.

If the Inspector returns `401 Unauthorized`, check that the key is active and
that the custom `Authorization` header is being forwarded to the MCP endpoint.
