# Tabi · UI Registry

**Spec:** UI-AUDIT-1.0 · **Date:** 2026-10-31 · **Status:** UI-01, UI-02, UI-03 and UI-11 accepted; frozen pending an explicitly approved change request.

## Immutable development rules
1. Every change specifies module ID, scope, acceptance criteria, and files touched before editing.
2. Anything not explicitly in scope must preserve its appearance, behavior, and data contract.
3. Never modify Supabase schema, RLS, authentication, encryption, localStorage keys, or sync without a separate explicit decision.
4. GitHub Pages production remains on `main`. Do not deploy without approval of a specific candidate.
5. Before release: compare against baseline, test responsive layouts and both themes, verify export/import and existing records.
6. "No change" means freeze behavior, not permission for incidental redesign.

## Approved component requirements

| ID | Component | Approved change / contract | Status |
|---|---|---|---|
| UI-01 | Header controls | Center kanji 旅 inside its tile; coherent sync/settings icons in equal tiles. **FROZEN: approved 2026-11-07.** | Accepted — no further changes |
| UI-02 | Hero | Dynamic heading based on inventory states; no new persisted phase field. | Accepted 2026-11-07 — frozen |
| UI-03 | Stats | Counts become interactive filters without changing values or visual card layout: Total resets, Rooms shows occupied room groups, Tagged filters colored objects. | Accepted 2026-11-07 — frozen |
| UI-04 | Navigation & viewport | Touch swipe between Objects/Kanban, preserving drag and Kanban horizontal scrolling; responsive reflow when device orientation changes. | Implemented in candidate; device acceptance pending |
| UI-05 | Search & filters | Compact filter chips. | Chips and composition TBD |
| UI-06 | Progress | **No change.** Existing computation and interaction frozen. | Frozen |
| UI-07 | Rooms | Collapsible groups and reorder rooms. | Persistence design TBD |
| UI-08 | Item cards | Edit item title inline. | Save/cancel rules TBD |
| UI-09 | Kanban | Optional compact cards. | Density controls TBD |
| UI-10 | Settings | Reduce visual density; simplify without removing functions. | Layout TBD |
| UI-11 | Project name | Tap the text after “Tabi ·” to edit project title inline; default “Мой переезд”; Enter/blur saves, Escape cancels, empty title keeps previous; max 48 characters. Independent local-only browser storage, no cloud sync. | Accepted 2026-11-07 — frozen |
| CORE-01 | Storage & sync | **No change.** Keep local data, account login, Supabase, encryption, sync and schemas intact. | Frozen |
| DS-01 | Design system | Subtle animations (respect reduced-motion) **and consistent focus/active-state colors across Komorebi / Dusk**; keep native iPadOS/iOS text-selection handles. | Focus styling accepted as requirement 2026-11-07; implementation pending |

## UI-04 implemented candidate — swipe gestures and viewport
- In Objects, a short horizontal finger swipe (≥75 px in ≤700 ms; horizontal displacement ≥1.7× vertical, vertical displacement ≤65 px) left opens Kanban; right opens Objects (if not already selected).
- In Kanban, horizontal scrolling of columns remains native; **right swipe at the leftmost board scroll edge** returns to Objects. A swipe over buttons, links, inputs, or text editors does not switch tabs.
- Long-hold card drag retains priority; gesture code neither prevents native scrolling nor modifies persisted data. No new storage keys or Supabase operations.
- Layout width remeasured from document viewport on resize/orientationchange/screen.orientation/visualViewport.resize (plus delayed second measure to accommodate mobile browser UI). CSS is responsive in shallow landscape and narrow portrait viewports. No forced zoom or viewport-meta edits.
- Manual device checks pending: iPad portrait ↔ landscape, Android/iOS, both themes, long-press drag, horizontal Kanban, form editing, pagination/filters and touch navigation.

## UI-04 additional acceptance criteria — orientation (requested 2026-11-07)
- After rotating a phone between portrait and landscape, viewport width and layout must recalculate automatically; no manual pinch-to-zoom, page refresh, or viewport reset required.
- Preserve readable font sizes, usable touch targets, and no unintended horizontal overflow at typical mobile widths.
- Keep active Objects/Kanban view, filter state, and local data intact; orientation must not trigger data mutations or Supabase requests.
- Check on Android Chrome and iOS Safari; test both Komorebi and Dusk.
- **Not implemented**: this is an added acceptance requirement for UI-04; do not change orientation handling during UI-01.

## UI-11 · Project name change request (2026-11-07)
- Allowed: text label immediately after “Tabi ·”, its editor control, a new independent localStorage key `tabi-project-name-v1`, and browser tab title.
- Prohibited: changing approved UI-01 icon shapes / button sizes / alignment, hero, progress, room and item data models, Supabase, authentication, encryption or existing storage keys.
- Default project title: **Мой переезд**; edit by tapping; save on Enter or blur; cancel on Escape; avoid accidental empty names, HTML injection and overflow.
- **Storage caveat:** name is device/browser-origin local; it is not synced across devices. Adding cloud sync would require separate CORE-01 approval.
- Test narrow screens, Komorebi/Dusk, persistence after reload, and both action buttons unaffected.

## UI-02 · Dynamic hero — acceptance rules (candidate)
- Empty inventory: **«Порядок в вещах.»**
- Has items, none completed, at least one undecided/unclassified: **«Время определиться.»**
- Has items, none completed, all decided red/green: **«План обретает форму.»**
- Some completed, not all: **«Шаг за шагом.»**
- Every current item completed: **«Всё на своих местах.»**
- Use existing `state.items` and existing `done` / `status` fields; no new stored phase, no changes to progress calculations, filters, or sync.
- Only the hero `h1` content changes. The subtitle, action buttons, header, themes and frozen UI-01/UI-11 remain unchanged.
- Five deterministic stage tests and JavaScript syntax check passed; user accepted 2026-11-07. Further changes require separate approval.

## UI-03 · Statistics as filters — acceptance rules (candidate)
- Counters keep original global totals: all nondeleted items, distinct rooms containing nondeleted items, all items with colored (non-`none`) marks. Searching or filtering must **not** change the counters.
- **Всего объектов**: reset search, selected room, unfinished-only, pending-decision filter, other stat filters; navigate to Objects.
- **Комнат**: switch to Objects and toggle display of only room groups with matching objects (hide empty room groups). Do not modify rooms or counts.
- **С цветной меткой**: toggle visibility of objects whose status is not `none`; work in both Objects and Kanban.
- Each selected stat displays a subtle border and `aria-pressed`; tap again to clear the toggle. Other existing search/room filters remain composable.
- Only `index.html` statistics markup, stat-specific CSS, ephemeral `statFilter` state, `filtered()` clause and stat click handler are in scope. **Not in scope:** data models, Supabase, project title, hero heading, progress computations, approved UI-01/02/11.
- Test empty inventory, mixed colored/uncolored items, room filtering, searching, dark/light theme and mobile widths. No stored filter state.

## DS-01 · Focus / active state consistency — approved requirement (2026-11-07)
- Evidence: **iPad screenshot**, Dusk mode, editing the project name. A light-green outer outline appears beside the theme-colored input border and blue iPadOS text-selection handles.
- Root cause in source: legacy generic `button:focus-visible,input:focus-visible,select:focus-visible` uses a fixed `#b0c7b7` outline, independent of the later Komorebi/Dusk design tokens. Treat focus outline and active border as distinct states; do not misclassify iPadOS selection handles as app UI.
- Unify focus indicators for relevant controls (buttons, inputs, selects, text editors) using theme tokens: Komorebi `--accent: #A65B48` terracotta; Dusk `--accent: #D5A76E` warm gold. Use adequate contrast and keyboard focus visibility; avoid distracting duplicate rings on touch.
- Preserve **system-native text selection** (iPadOS blue handles), input behavior, hit targets, and semantics. Do not disable focus outlines outright.
- Test on **iPadOS Safari (landscape and portrait)**, iOS Safari, Android Chrome; both themes; keyboard and touch navigation; project title editing; active stats.
- Approved as a **future DS-01 design requirement only**. No implementation in currently approved UI-01/UI-02/UI-03/UI-11 and no modification to production `main`.

## Design invariants
- Two visual identities: Komorebi (light) and Dusk (dark). Keep approved semantics: red = leave; yellow = undecided; green = send/take; gray = unclassified.
- Checkbox completion is independent of category but only eligible for red/green.
- Keep search, card drag, Kanban, quick add, JSON backup, Auth and existing user data.
- Protect touch targets and icon symmetry; changes must work on narrow mobile screens.
- Don't infer completion of UI changes from requirements being recorded.

## Change request template
```
Change ID:
Target version:
Module IDs:
User-approved behavior:
Files allowed:
Files prohibited:
Acceptance tests:
Data impact (none / migration):
Rollback:
Approval / status:
```

## Baseline identification
- **Published:** GitHub `main/index.html`, fetched on 2026-10-31; blob SHA `81fad849978f44cb8eac737f090b699d82372906`; length 41,986 characters.
- **Visual baseline:** v1.5.4 is committed to `release/1.5.4-candidate` and deployed to Vercel Preview. UI-01 work is isolated on `feature/ui-01-header-v1.5.5`.
- Treat these as separate version tracks until an explicit release.
