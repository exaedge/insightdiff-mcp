# Current MCP Contract

## Tools

### `get_mcp_help`

No input. Use first when the client needs built-in examples or current notes.

### `take_screenshot`

Required: `url`.

Optional:

- `viewport`: `{ "width": 390..1440, "height": number }`
- `full_page`: default is full page unless viewport is explicit; with explicit
  viewport, omitted means viewport-only
- `wait_until`: `load`, `domcontentloaded`, `networkidle0`, `networkidle2`
- `delay_ms`: `0..30000`
- `scroll_to_bottom`, `dismiss_cookie_consent`, `extract_text`
- `auth`: per-request target-site auth, never the MCP API key

`auth` modes:

- `basic`: `username`, `password`
- `token`: `token`, sent as `Authorization: Bearer <token>`
- `api_key`: `api_key.header`, `api_key.value`
- `cookie`: `cookie.name`, `cookie.value`, optional `cookie.domain`
- `custom_headers`: `headers`, limited to 10 entries

Returns PNG image content plus JSON metadata.

### `compare_pages`

Required: `image1_base64`, `image2_base64`, `perspective`.

Optional:

- `image1_name`, `image2_name`
- `image1_text`, `image2_text`
- `scopes`: optional caller-provided page sections or bounding boxes to focus
  analysis
- `save_report`, `report_title`
- `return_full_report`
- `report_format`: `markdown` or `json`
- `language`: `en` or `ja`; omit for English

Use `perspective: "Overall"` for visual/layout; `"Text"` for copy/content.

### `configure_compare_output`

Optional: `return_full_report`, `report_format`, `save_report`.
Use to set user defaults before repeated comparisons.

### Reports

- `list_reports({ limit?, cursor? })`
- `get_report({ report_id })`
- `delete_report({ report_id })`
- `export_report({ report_id, format, sections?, statuses? })`

Export formats: `json`, `markdown`, `csv`, `html`. PDF is web-client only.
`sections` can include `metadata`, `summary`, `text_analysis`, and
`visual_analysis`. `statuses` can include `Same`, `Changed`, `Added`, and
`Removed`.

## Resources

- `insightdiff://usage/monthly`
- `insightdiff://rate-limit/status`
