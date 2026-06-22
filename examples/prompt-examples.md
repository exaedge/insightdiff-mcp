# Prompt Examples

## Compare Production And Staging

```text
Use InsightDiff MCP. Capture these two URLs with viewport 1440x900,
wait_until load, delay_ms 3000, and the same full_page setting. Then compare
them with perspective Overall and save the report.

Production: https://production.example.com
Staging: https://staging.example.com
```

## Design Image Versus Public Page

```text
Use my attached design screenshot as image1. Capture
https://production.example.com as image2 with InsightDiff MCP using viewport
1440x900. Run compare_pages with perspective Overall, save the report, and
return a compact summary with the report ID.
```

## Uploaded Screenshot Versus Production

```text
Use my attached screenshot as image1. Capture
https://production.example.com as image2 with InsightDiff MCP. Name the images
Uploaded Screenshot and Production, compare with perspective Overall, and save the
report.
```

## Text Regression Check

```text
Use InsightDiff MCP to capture both public URLs with extract_text true. Then
compare_pages with perspective Text and include image1_text and image2_text
from the screenshot metadata.

Before: https://before.example.com
After: https://after.example.com
```

## Multi-Viewport Visual QA

```text
Use InsightDiff MCP to compare these URLs at mobile, tablet, and desktop
viewports. Keep each comparison separate and save one report per viewport.

Viewports:
- Mobile: 390x844
- Tablet: 768x1024
- Desktop: 1440x900

URL A: https://production.example.com
URL B: https://staging.example.com
```

## Export A Recent Report

```text
Use InsightDiff MCP to list my recent reports, find the newest MCP-created
report for staging versus production, then export it as Markdown.
```
