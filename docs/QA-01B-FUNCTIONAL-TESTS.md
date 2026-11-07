# QA-01B · Functional acceptance scenarios

Status: **PENDING MANUAL DEVICE EXECUTION**. Test only on disposable sample inventory, not real synced data. Do not import into a production account.

## Test fixture

Create two rooms (A, B), three items: Alpha (A/red), Beta (A/yellow), Gamma (B/green). Record original names, statuses and order. Prefer an isolated browser profile with sync disconnected. Export a JSON backup before beginning.

## Cases

| ID | Steps | Expected | Result |
|---|---|---|---|
| B01 | Rename project; tap outside input | Name saves; editor closes; persists after reload | Pending |
| B02 | Rename project; press Escape | Original name remains | Pending |
| B03 | Edit Alpha title in Objects; Enter; reload | New name persists | Pending |
| B04 | Edit Alpha title in Kanban; tap outside | New name persists, no green focus ring | Pending |
| B05 | Edit Beta title; blank input | Empty name rejected; original restored | Pending |
| B06 | Collapse room A; reload; expand | Collapse preference persists locally; cards remain | Pending |
| B07 | Move room B before A; reload | New room order persists | Pending |
| B08 | Rename room A; inspect its cards | Cards retain room membership under new name | Pending |
| B09 | Drag Alpha A→B; reload | Exactly one Alpha in B | Pending |
| B10 | Drag Alpha within same room onto same position | No unwanted reordering or state change | Pending |
| B11 | Kanban drag Beta yellow→red; reload | Status red; completion false | Pending |
| B12 | Toggle compact Kanban; reload | Density preference persists; status unaffected | Pending |
| B13 | Select Alpha and Beta; apply room B and color green | Both updated; Gamma unchanged | Pending |
| B14 | Select Gamma; delete; cancel confirmation | Gamma remains | Pending |
| B15 | Select Gamma; confirm delete; reload | Gamma absent; others unchanged | Pending |
| B16 | Switch Komorebi/Dusk; focus name, theme selector, item editor | Accent matches theme; no duplicate green ring | Pending |
| B17 | Resize portrait/landscape; use tab/swipe navigation | No clipped controls or accidental drag | Pending |
| B18 | During inline name edit, trigger a render via another UI update | No silent loss of user input (risk QA-01A-04) | Pending |

## Execution matrix

- iPad Safari touch / portrait and landscape.
- Phone browser touch / portrait.
- Desktop Chromium keyboard and pointer.
- Both Komorebi and Dusk themes.

## Exit criteria

No data loss, duplication, unexpected status change or blocked navigation. Any failure must include device, browser, scenario ID, expected vs actual, and screenshot if visual. Do not label these scenarios passed until executed. QA-01C cloud/import testing requires separate user approval and backup.
