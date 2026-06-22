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
- `auth`: per-request target-site auth

Returns PNG image content plus JSON metadata.

### `compare_pages`

Required: `image1_base64`, `image2_base64`, `perspective`.

Optional:

- `image1_name`, `image2_name`
- `image1_text`, `image2_text`
- `scopes`
- `save_report`, `report_title`
- `return_full_report`
- `report_format`: `markdown` or `json`

Use `perspective: "Overall"` for visual/layout; `"Text"` for copy/content.

### `configure_compare_output`

Optional: `return_full_report`, `report_format`, `save_report`.
Use to set user defaults before repeated comparisons.

### Reports

- `list_reports({ limit?, cursor? })`
- `get_report({ report_id })`
- `delete_report({ report_id })`
- `export_report({ report_id, format })`

Export formats: `json`, `markdown`, `csv`, `html`. PDF is web-client only.

## Resources

- `insightdiff://usage/monthly`
- `insightdiff://rate-limit/status`
