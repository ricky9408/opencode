# OpenCode subagent transcript navigation

Evidence for anomalyco/opencode#60727.

- Before: dev `df832cb2cacf7389c3754c02396cdf30835c8350`, with the new regression test applied and the composer-mode fix removed.
- After: `b97cea7e43cb357608e9d0ea21f8b19432385aa2`.
- Fixture: a child session with 20 local user messages and two active subagents, 120 columns by 30 rows. No model requests or live user sessions.
- Images rasterize `captureSpans()` from the real headless OpenTUI renderer, preserving text, colors and cell widths. They are renderer captures, not a live-terminal recording.
- Sequence: PageUp from the end, then Home. Before, Home leaves the paged viewport in place. After, it shows message 0000. The final End capture shows message 0019.
- The negative control fails on Home with the fix removed; the corrected source passes at 60 and 120 columns. The test also covers PageUp/PageDown, Ctrl+G, modal isolation, picker selection and returning to the parent session.

Run the committed regression from `packages/tui`:

```sh
bun test --timeout 30000 test/session-subagent-navigation.test.tsx
```
