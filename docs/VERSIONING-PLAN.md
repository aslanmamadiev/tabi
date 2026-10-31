# Tabi · Versioning Plan

**State:** proposed release process; documentation only.

## Source of truth and branches
- `main`: published GitHub Pages. No experimental code.
- `docs/ui-audit-1.0`: specifications and release controls; does not change `index.html`.
- `feature/<module>-<topic>`: one approved UI module or a tightly defined combined change.
- Use small commits and review diffs; any unexpected changed file is grounds to stop.

## Versions
- `PATCH` (1.5.x): localized UI bug fixes with no new feature/data change.
- `MINOR` (1.x): backwards-compatible user-facing features.
- `MAJOR` (2.x): only for a purposely approved incompatible revision.
- Tags/releases are created only for *actual commits*; don't tag uncommitted candidate HTML files.
- Documented candidate v1.5.4 is not evidence that GitHub Pages currently runs v1.5.4.

## Sequence (proposal)
0. Establish baseline and documentation; preserve production untouched.
1. UI-01 header geometry; DS-01 limited animations in a separate change.
2. UI-05 chips; UI-03 clickable metrics.
3. UI-02 dynamic heading; UI-10 settings simplification.
4. UI-07 room folding and ordering; UI-08 inline item names.
5. UI-04 swipe navigation; UI-09 compact Kanban.
Each stage needs behavior details and explicit approval before implementation.

## Release gate
1. Capture existing `index.html` hash and candidate's precise source; export JSON backup from currently working app.
2. Write scoped change request and tests.
3. Implement on feature branch, never directly in `main`.
4. Check JS syntax, HTML structure, key controls, mobile widths, both themes, touch and keyboard.
5. Run storage compatibility tests and multi-device data integrity smoke tests when relevant.
6. Show changes/diff to user, receive release approval.
7. Merge approved candidate; verify GitHub Pages and sync; record commit SHA and changelog entry.
8. Rollback code by revert; restore user data only from an explicit verified backup, never silently.

## Special warning: sync
The current single encrypted-payload sync and merge logic has known race/deletion-reappearance risks. `CORE-01` is frozen for this phase, so **do not claim these are fixed**. Document separately for the future collaboration architecture.
