# Tabi · CHANGELOG

## [Unreleased] — v1.5.5 candidate

### Changed
- **UI-01 Header:** Kanji tile and both header action tiles now share a 48×48 desktop / 44×44 mobile sizing system; center-aligned kanji and SVGs, narrow-screen spacing adjustments.
- Scope limited to header CSS only. No changes to JavaScript, localStorage, Supabase, encryption, progress, cards or the approved themes.

### Verification pending
- Visual review at 320/360/390/768px with Komorebi and Dusk.
- Mobile browser comparison and end-user approval before merging into main.


This is a **reconstructed history**, prepared on 2026-10-31 from conversation decisions and surviving HTML snapshots. Earlier changes were not consistently tagged in Git: do not interpret every heading as a GitHub Release or as a live deployment.

## Status legend
- **Built**: a corresponding standalone HTML artifact exists.
- **Production**: verified in GitHub `main`, not inferred from standalone builds.
- **Candidate**: prepared but not released.
- **Proposed**: not implemented.

## [1.5.4] — Candidate, not deployed
- Replaced mismatched header glyphs with consistent linear SVG sync and settings icons.
- Standardized placement of the two header icon tiles, including narrow screens.
- Made settings' close icon visually smaller and more discreet while retaining a usable touch target.
- Preserved Komorebi / Dusk visual identities.

## [1.5.3] — Built, not deployed
- Alignment polish for top controls, room addition button, select arrows and room deletion controls.
- Added top-right close affordance to settings modal.
- Later close-button design was reconsidered and refined in 1.5.4.

## [1.5.2] — Built, not deployed
- Approved warm **Komorebi** daytime palette and contrasting **Dusk** evening palette.
- Theme-dependent status indicator styling while preserving red/yellow/green/gray meanings.
- Kept existing core inventory and cloud architecture.

## [1.5.1] — Built, not deployed
- Experimental **Hikari** color system after feedback on colder/lower-contrast previous palettes.
- Theme iteration, not a data model change.

## [1.5.0] — Built, not deployed
- Introduced separate light/dark-theme controls and a retrofuturist palette foundation.
- Introduced 旅 brand tile and kanji favicon.
- Replaced first-visitor seeded personal item names with an empty initial item list; existing browser/cloud records retained.
- Added room-scoped inline new-item composer (plus button for room).
- Added clickable `N требуют решения` filter (implementation counts undecided/unclassified items).
- Updated alignment/layout of sync/settings buttons.
- **Important:** Prior discussions proposed safer deletion merging and conflict handling, but do not count them as implemented; the original encrypted-document sync mechanism remained.

## [1.4] — Published core generation / GitHub main baseline
- Added Supabase email/password authentication.
- Added per-account ownership for cloud records and backend RLS policies restricting reads/writes to owner.
- Continued client-side PBKDF2/AES-GCM encrypted JSON payload sync and local storage.
- Migrated development from standalone HTML into GitHub Pages and a linked Supabase project.
- Status verified only as generation: current `main/index.html` has auth and cloud code, and **does not include 1.5.x themes**.

## [1.3] — Built
- Removed blue status and mapped legacy blue status to yellow, resetting completion when appropriate.
- Introduced bulk selection and group operations, and unfinished-only filter.
- Retained card completion rules: completion only for red (leave) / green (send or take).
- Continued Kanban and long-press item movement.

## [1.2] — Built
- Developed independent checkbox completion state, separate from decision color.
- Added progress/completion tracking and long-press movement of objects.
- Continued rooms, editing, search, JSON import/export and offline local persistence.

## [1.0–1.1] — Historical early builds (exact release boundary unverified)
- Room-grouped objects, color decisions and item cards.
- Objects/Kanban views, search and filters, new/edit items, room/category settings.
- Local browser storage, JSON backup/export/import developed in early iterations.
- Initial personal item names were included as sample seed data; later removed from initial state in 1.5.

## Known unresolved
- `CORE-01`: sync is based on a per-user encrypted blob and timestamp merge. Concurrent writes can race; deletion tombstones are not fully protected against reappearance. This was **not fixed** in 1.5.x.
- Historical version numbers before 1.2 and specific features introduced at each early step are approximate because releases were not formally tagged.
- No explicit user authorization yet to replace production `main` with 1.5.4.

## Forward plan
UI-AUDIT-1.0 identifies scoped UI-01..UI-10 and DS-01 work. Requirements are approved; implementation is not yet started. See `UI-REGISTRY.md` and `VERSIONING-PLAN.md`.
