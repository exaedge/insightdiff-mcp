# InsightDiff MCP Workflows

## Screenshot A Public Page

1. Call `take_screenshot` with URL, viewport, wait, and delay.
2. Use `full_page: true` for whole-page review; use `false` for viewport or hero.
3. If returned image is large, retry with viewport-only or a shorter page.

## Compare Two Public URLs

1. Read usage/rate-limit resources if the job is not trivial.
2. Capture both URLs with identical viewport and timing.
3. Pass only each image content block `data` field to `compare_pages`.
4. Use `perspective: "Overall"` unless the user specifically wants copy checks.
5. Save report unless user asks for disposable output.

## Uploaded Screenshot Vs Public Page

1. Use the uploaded design or private-page screenshot as `image1_base64`.
2. Capture the public page with `take_screenshot` as `image2_base64`.
3. Name images clearly: `Design`, `Implementation`, `Private Screenshot`, `Production`.
4. Compare with `perspective: "Overall"` and include a report title.

## Text Regression

1. Capture both public URLs with `extract_text: true`.
2. Pass screenshot image data plus `image1_text` and `image2_text`.
3. Use `perspective: "Text"`.
4. Report content changes separately from layout noise.

## Multi-Viewport Check

Run separate same-viewport comparisons:

- Mobile: `{ "width": 390, "height": 844 }`
- Tablet: `{ "width": 768, "height": 1024 }`
- Desktop: `{ "width": 1440, "height": 900 }`

Keep each comparison small. Export a report per viewport if the user needs
audit artifacts.

## Report Handoff

1. Use `list_reports` to find recent report IDs.
2. Use `get_report` for full details.
3. Use `export_report` with `markdown` for agent-readable review, `json` for
   automation, `csv` for spreadsheet review, or `html` for standalone sharing.
4. Use `delete_report` only when the user explicitly asks for cleanup.
