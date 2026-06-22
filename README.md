# InsightDiff MCP

Public setup guide, examples, and optional agent skill for the hosted
InsightDiff MCP server.

InsightDiff MCP is a remote MCP endpoint. Users connect their MCP client to:

```text
https://insightdiff.exaedge.ai/mcp
```

This repository contains client setup docs and the optional agent skill only.
It does not contain the InsightDiff server and it is not used to run an MCP
server.

## MCP Snapshot

- Server name: `insightDiff`
- Transport: Streamable HTTP
- Endpoint: `https://insightdiff.exaedge.ai/mcp`
- Authentication: `Authorization: Bearer pv_live_...`
- API key prefix: `pv_live_`
- Active key limit: 5 keys per user

## Account And Pricing

- Create account / sign in: https://insightdiff.exaedge.ai/
- Pricing: https://insightdiff.exaedge.ai/#pricing
- API keys: https://insightdiff.exaedge.ai/settings
- Contact sales: https://insightdiff.exaedge.ai/contact

| Plan | Price | Credits | Notes |
| --- | ---: | ---: | --- |
| Free | $0 | 100 credits on signup | No credit card required. Includes screenshot tools and web access. |
| Pro | $4.99/mo | 1,000 credits/month | Advanced analysis, cloud report storage, exports, private-page screenshot workflows, and priority support. |
| Enterprise | Contact sales | Custom | Custom credits, infrastructure, integrations, SLA, and deployment options. |

MCP usage shares the same account credits and rate limits as the web app.
`compare_pages` uses credits. Screenshot capture is tracked separately.

## 1. Create An API Key

1. Sign in to InsightDiff.
2. Open `Settings`.
3. Open `API Keys`.
4. Create a key for your MCP client.
5. Copy the full `pv_live_...` key immediately. It is shown once.

Do not commit real API keys. Use placeholders in shared examples.

## 2. Configure The MCP Client

Use this exact server name and endpoint:

```json
{
  "mcpServers": {
    "insightDiff": {
      "url": "https://insightdiff.exaedge.ai/mcp",
      "headers": {
        "Authorization": "Bearer <YOUR_API_KEY>"
      }
    }
  }
}
```

Restart the MCP client after editing its config.

Some clients support remote URL plus custom headers directly. Others only
support OAuth-style remote connector flows. A client must be able to send the
custom `Authorization` header to use the current InsightDiff API-key endpoint.

## 3. Optional: Install The Agent Skill

The MCP server is the tool endpoint. The optional skill teaches supported AI
agents safer workflow patterns for using those tools.

The skill folder is committed at `skills/insightdiff-mcp`.

Claude Code:

```bash
git clone https://github.com/exaedge/insightdiff-mcp.git
mkdir -p ~/.claude/skills
cp -R insightdiff-mcp/skills/insightdiff-mcp ~/.claude/skills/
```

OpenCode:

```bash
git clone https://github.com/exaedge/insightdiff-mcp.git
mkdir -p ~/.opencode/skill
cp -R insightdiff-mcp/skills/insightdiff-mcp ~/.opencode/skill/
```

Cursor:

```bash
git clone https://github.com/exaedge/insightdiff-mcp.git
mkdir -p ~/.cursor/skills
cp -R insightdiff-mcp/skills/insightdiff-mcp ~/.cursor/skills/
```

Restart the agent or editor after installing the skill.

## 4. Smoke Test

Use MCP Inspector:

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

Expected result: help text returns, resources return authenticated JSON, and no
response includes the raw API key.

## Tools

- `get_mcp_help`: return built-in workflow guidance.
- `take_screenshot`: capture a public HTTP(S) page as PNG.
- `compare_pages`: compare two PNG/JPEG screenshots or uploaded images.
- `configure_compare_output`: set default compare response style.
- `list_reports`: list saved verification reports.
- `get_report`: read one saved report.
- `delete_report`: remove a saved report from the active list.
- `export_report`: export a saved report as JSON, Markdown, CSV, or HTML.

### Tool Input Notes

`take_screenshot` accepts optional `viewport`, `full_page`, `wait_until`,
`delay_ms`, `scroll_to_bottom`, `dismiss_cookie_consent`, `extract_text`, and
`auth`. `auth` is target-site auth for one screenshot request only, not the MCP
API key. Supported `auth.type` values are `basic`, `token`, `api_key`, `cookie`,
and `custom_headers`.

`compare_pages` requires `image1_base64`, `image2_base64`, and `perspective`.
Optional fields include `image1_name`, `image2_name`, `image1_text`,
`image2_text`, `scopes`, `save_report`, `report_title`, `return_full_report`,
`report_format`, and `language`. `perspective` is `Overall` or `Text`.
`report_format` is `markdown` or `json`. `language` is `en` or `ja`.

`export_report` accepts `report_id`, `format`, `sections`, and `statuses`.
Formats are `json`, `markdown`, `csv`, and `html`. `sections` can include
`metadata`, `summary`, `text_analysis`, and `visual_analysis`. `statuses` can
include `Same`, `Changed`, `Added`, and `Removed`.

## Resources

- `insightdiff://usage/monthly`: monthly usage and credit state.
- `insightdiff://rate-limit/status`: current rate-limit state.

## Example Prompts

Compare production and staging:

```text
Use InsightDiff MCP. Capture https://production.example.com and
https://staging.example.com with viewport 1440x900, then compare them with
perspective Overall and save the report.
```

Compare an uploaded screenshot with a public page:

```text
Use my attached screenshot as image1. Capture https://production.example.com
as image2 with InsightDiff MCP, then run compare_pages with perspective Overall.
```

Check copy changes:

```text
Capture both URLs with extract_text true, then compare_pages with perspective
Text and return a compact summary.
```

More examples are in [`examples/`](examples/).

## Limits And Safety

- `take_screenshot` captures public HTTP(S) pages only.
- Private, VPN-only, or internal pages should be supplied as uploaded PNG/JPEG
  screenshots to `compare_pages`.
- Screenshot responses are capped at 15 MB.
- Each `compare_pages` image input must decode to 15 MB or less.
- Target-site credentials passed to `take_screenshot.auth` are for that one
  screenshot request only. They are not the MCP API key.
- Never place the MCP API key inside tool arguments, prompts, reports,
  screenshots, or logs.

## Troubleshooting

`401 Unauthorized`:

- Check the `Authorization` header is present.
- Confirm the key starts with `pv_live_`.
- Confirm the key was not revoked or expired.
- Confirm the client supports custom headers for remote MCP.

Screenshot fails:

- Use a public `https://...` URL.
- For private, VPN-only, or internal pages, upload a PNG/JPEG screenshot and
  use `compare_pages`.

Comparison fails:

- Pass actual PNG/JPEG base64 in `image1_base64` and `image2_base64`.
- When using `take_screenshot` output, pass the image content block `data`
  field, not the full JSON response.
- Do not pass URLs, report IDs, filenames, or file objects as base64 inputs.
