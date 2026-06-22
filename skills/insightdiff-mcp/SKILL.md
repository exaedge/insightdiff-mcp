---
name: insightdiff-mcp
description: "Use for InsightDiff MCP visual QA: screenshots, compare_pages, design-vs-page, staging/prod diffs, report export, usage checks."
---

# InsightDiff MCP

Use this skill for visual verification work through the InsightDiff MCP server:
capturing screenshots, comparing URLs or image inputs, checking copy regressions,
reviewing saved reports, exporting results, and reading usage/rate-limit state.

## First Moves

1. Confirm the MCP server is configured. If not, read
   `references/setup-and-safety.md` and help create client config without asking
   the user to paste a raw key into chat.
2. For unclear MCP behavior, call `get_mcp_help` first; it is no-cost.
3. Before batch or credit-sensitive comparisons, read
   `insightdiff://usage/monthly` and `insightdiff://rate-limit/status`.
4. Choose the workflow in `references/workflows.md`.
5. Use exact inputs from `references/tool-reference.md`; never invent disabled
   tools or pass URLs/report IDs as image base64.

## Operating Rules

- Use `take_screenshot` only for public HTTP(S) URLs.
- For private/VPN pages, internal pages, design screenshots, or photos,
  obtain PNG/JPEG base64 another way and pass it to `compare_pages`.
- Use identical viewport, full-page, wait, delay, scroll, and cookie settings
  for both sides of a URL comparison.
- Prefer `return_full_report: false` for routine agent work; export Markdown or
  HTML when a human-readable artifact is needed.
- Save reports by default for user-facing verification; use `save_report: false`
  for quick disposable checks.
- Never put the MCP API key in tool arguments, reports, screenshots, or logs.

## References

- Setup, auth, safety: `references/setup-and-safety.md`
- Common visual QA workflows: `references/workflows.md`
- Current tool/resource contract: `references/tool-reference.md`
- Troubleshooting and limits: `references/troubleshooting.md`

## Test Prompts

See `evals/evals.json` for realistic prompts to validate this skill.
