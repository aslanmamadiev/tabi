# Tabi · CHANGELOG

## [Unreleased] — UI-08 Kanban + bulk actions
- Inline item-title editing now also works in Kanban (same Enter, blur, Escape semantics).
- Existing Select multiple action menu now includes confirmed bulk deletion, using existing soft-delete flag and sync path.
- Existing bulk room reassignment, label changes, mark done and uncheck remain available.
- Draft preview only, awaiting device verification and user approval.

## [Unreleased] — UI-08 inline item titles
- Tap/click a title in the Objects view to edit directly; Enter/blur saves, Escape cancels.
- Blank names rejected, 160-character limit retained, existing updatedAt/persist/sync path used.
- Drag long-press remains on cards outside the active text editor; Kanban and status logic untouched.
- Candidate awaiting mobile/touch acceptance; no merge to main.


## [Unreleased] — UI-07 room reorder feedback
- Accent insertion line tracks the target position during room-handle dragging; cancel clears the marker without reordering.
- Only UI-07 room drag interaction changed. Awaiting device acceptance.


## [Unreleased] — UI-07 room controls
- Collapse/expand rooms with local-only preference; reorder rooms in Settings by handle or arrows (existing synced room order).
- Minimal room-delete SVG matching Settings close icon; deletion safeguards preserved.
- LABEL-01: defer custom status labels, colors, ordering and deletion until a separate architecture review.
- UI-07 awaits mobile/iPad acceptance; no changes to accepted UI-01–05 or sync architecture.


## [Accepted] — UI-05 filter simplification (2026-11-07)
- Removed the experimental four-chip filter row after review: its actions duplicated existing interactive statistics, decision counter and unfinished-only toggle.
- Restored `index.html` exactly to the accepted UI-04 version; no changes to existing filters, layout, data, or sync.


## [Accepted] — UI-04 interactive swipe refinement (2026-11-07)
- Finger-tracked horizontal displacement in the active list/board area; easing on completion and elastic snap-back when the gesture is too short.
- Supports `prefers-reduced-motion`. Does not modify accepted components or Supabase.
- User confirmed swipe and navigation behavior; UI-04 frozen. Not yet merged to `main`.


## [Unreleased] — UI-04 navigation and orientation candidate

### Added
- Touch-only horizontal swipes between Objects and Kanban, with guards for editable controls, long-press drag and the Kanban scrolling region.
- A right swipe from the left edge of the Kanban board scroll range returns to Objects; horizontal column scrolling retains priority elsewhere.
- Responsive layout recomputation after phone/tablet rotation, including delayed mobile browser resize settling. Narrow landscape/portrait refinements; no forced zoom.

### Safety and verification
- No changes to frozen UI-01 / UI-02 / UI-03 / UI-11, progress, storage contracts, encryption or sync.
- JavaScript syntax check done; mobile gestures/orientation and visual layouts require user acceptance on real hardware.


## [Planned] — DS-01 focus indicator alignment (approved requirement 2026-11-07)
- iPadOS Dusk observation: an old light-green `#b0c7b7` generic focus outline conflicts with the warm-gold input border, while blue text-selection handles are native iPadOS behavior.
- Approved future solution: unify app focus/active outlines with theme tokens (Komorebi `#A65B48`, Dusk `#D5A76E`), preserve keyboard visibility and native iPadOS selection, check both iPad orientations.
- **Not implemented**. No edits to `index.html`, frozen components, cloud storage, or production.


## [Unreleased] — UI-03 statistic filters (approved 2026-11-07)

### Added
- Interactive statistic cards: **Всего объектов** resets filters and shows the full Objects list; **Комнат** toggles occupied-room groups; **С цветной меткой** toggles colored objects in both Objects and Kanban.
- Selected card border and accessibility `aria-pressed`; the global counter values and their formulas are unchanged.

### Scope
- Client-side view filtering only; no local storage schema, Supabase, synchronization, auth, theme, progress, project-name or accepted UI-01/UI-02/UI-11 changes.
- User approved UI-03 behavior and visual appearance on 2026-11-07. This does not authorize merging into production `main`.


## [Unreleased] — UI-02 dynamic hero (approved 2026-11-07)

### Changed
- Main welcome heading now reflects the stage inferred from existing item statuses and completion: empty list, decisions pending, planning, partially completed, fully completed.
- Only the hero heading changes; counts and progress logic remain unchanged.
- No new data schema, localStorage key, sync behavior, theme or layout change.
- UI-11 project rename accepted; UI-01 header controls remain frozen.

### Acceptance
- User approved Russian headline variants and UI-02 scope on 2026-11-07. The component is now frozen; this is **not** permission to merge into production `main`.


## [Unreleased] — v1.5.6 candidate

### Added
- **UI-11 · Project title:** tap “Мой переезд” beside Tabi in the header to rename the current project inline; Enter or blur saves, Escape cancels. Default title “Мой переезд”; maximum 48 characters.
- Project title is stored in a separate browser-only key `tabi-project-name-v1` and shown in the browser tab title. It does **not** sync via Supabase; no modification to CORE-01.

### Scope and approvals
- UI-01 controls, accepted 2026-11-07, are frozen and unchanged by UI-11.
- Upcoming orientation reflow remains tracked under UI-04, not implemented here.
- Candidate awaiting mobile verification and approval; neither `main` nor GitHub Pages updated.


## [Unreleased] — v1.5.5 candidate

### Changed
- **UI-01 Header:** Kanji tile and both header action tiles now share a 48×48 desktop / 44×44 mobile sizing system; center-aligned kanji and SVGs, narrow-screen spacing adjustments.
- Scope limited to header CSS only. No changes to JavaScript, localStorage, Supabase, encryption, progress, cards or the approved themes.

### Fixed after mobile review (2026-11-07)
- Replaced the sun-like settings glyph with an eight-tooth cog silhouette and central hole.
- Replaced uneven custom refresh arcs with balanced standard two-arrow refresh paths.
- Removed the status dot from the sync button markup (not only hidden with CSS).
- Preserved the existing explicit sync action and fallback notice when the account is not configured.
- UI changes restricted to header SVGs and their alignment CSS; no storage, network, or auth changes in this revision.

### Mobile feedback revision (2026-11-07)
- **UI-01:** replaced the overly subtle settings icon with a solid, eight-tooth gear silhouette. The eight protruding teeth remain visible at the 21–22 px mobile glyph size; a contrasting central hole remains.
- **UI-04 (planned):** recorded automatic layout reflow after rotating the phone in `UI-REGISTRY.md`. No orientation code changed in this patch.

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
