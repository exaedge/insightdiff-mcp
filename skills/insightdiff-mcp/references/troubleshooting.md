# Troubleshooting And Limits

## Screenshot Looks Wrong

- Try `wait_until: "load"` plus `delay_ms: 3000`.
- Use `scroll_to_bottom: true` only when lazy content requires it.
- Use `dismiss_cookie_consent: true` unless the banner is the subject.
- Use identical settings for both comparison sides.
- Use `full_page: false` for above-the-fold checks.

## Screenshot Fails

- Verify URL is public HTTP(S), not private, VPN-only, or internal.
- If omitted scheme causes ambiguity, pass full `https://...`.
- If output exceeds 15MB, use viewport-only, shorter page, or smaller viewport.

## Comparison Fails

- Pass only PNG/JPEG base64, not URLs, report IDs, filenames, JSON objects, or
  whole screenshot responses.
- When using `take_screenshot`, pass only the image content block `data` field.
- Keep each decoded image at or below 15MB.
- If credits are exhausted, stop and report remaining credits.

## Rate Limits

- Read `insightdiff://rate-limit/status` before batch work.
- Break large verification jobs into small comparisons.
- Wait or ask the user before retrying repeated failures.

## Report Confusion

- A successful saved comparison returns `report.id`.
- Saved MCP reports appear in the same dashboard history as web app reports.
- `export_report` returns the actual file body as MCP text content.
