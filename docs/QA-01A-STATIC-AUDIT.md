# QA-01A · Статический аудит · 2026-11-07

Scope: index.html from fix/ui-11-project-outside-tap. Read-only inspection; no main merge, no data changes. JavaScript syntax: PASS. No browser, device or sync integration testing performed.

## Findings to verify

1. **Medium · Merge timestamp tie:** merge(a,b) chooses the local item on equal updatedAt timestamps. Concurrent equal-ms updates may resolve differently depending on device. Needs controlled two-device conflict test; do not modify CORE-01 without approval.
2. **Medium · Import validation:** hydrate validates only rooms/items arrays and item id/name types. Malformed labels, duplicate IDs and invalid statuses are not fully rejected. Test with disposable data before changing imports.
3. **Medium · No-op drag:** finishDrag writes order and timestamps even if dropped at the original position; may trigger unnecessary sync. Test before optimizing.
4. **Medium · Inline edit during render:** if sync/render occurs during inline editing, input can be detached and user edits lost. Reproduce with controlled test.
5. **Low · Bulk delete + room selection:** delete takes priority and ignores simultaneously selected room. Consider UX guard after testing.
6. **Low · Room drag boundary:** insertion marker not shown when pointer is over own row or empty space. Touch test edge cases.

## Confirmed by code inspection

- Project title saves on Enter, blur, outside pointerdown; Escape cancels.
- Inline name edit and modal both limit names to 160 characters.
- Room order uses existing rooms and roomsUpdated fields.
- Kanban density and project title are local-only preferences by design.
- Bulk delete uses tombstone deleted=true and updatedAt.
- No duplicate literal static HTML IDs detected (template expressions excluded).

## Gates

QA-01B: functional tests on disposable items, iPad/phone and keyboard. QA-01C: explicit permission and backups before cloud or import conflict tests. Findings are static risk hypotheses, not reproduced defects. Do not merge main without approval.
