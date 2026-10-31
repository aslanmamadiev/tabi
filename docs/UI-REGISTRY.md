# Tabi · UI Registry

**Spec:** UI-AUDIT-1.0 · **Date:** 2026-10-31 · **Status:** requirements agreed; implementation not yet approved.

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
| UI-01 | Header | Center kanji 旅 inside its tile. Use coherent sync/settings icons precisely centered in equal-size tiles across viewport widths. | Design approved; implementation pending |
| UI-02 | Hero | Dynamic title based on relocation phase. | Phase rules TBD |
| UI-03 | Stats | Counts become interactive filters. | Mappings and reset TBD |
| UI-04 | Navigation | Swipe between Objects and Kanban. | Resolve conflicts with drag/scroll |
| UI-05 | Search & filters | Compact filter chips. | Chips and composition TBD |
| UI-06 | Progress | **No change.** Existing computation and interaction frozen. | Frozen |
| UI-07 | Rooms | Collapsible groups and reorder rooms. | Persistence design TBD |
| UI-08 | Item cards | Edit item title inline. | Save/cancel rules TBD |
| UI-09 | Kanban | Optional compact cards. | Density controls TBD |
| UI-10 | Settings | Reduce visual density; simplify without removing functions. | Layout TBD |
| CORE-01 | Storage & sync | **No change.** Keep local data, account login, Supabase, encryption, sync and schemas intact. | Frozen |
| DS-01 | Design system | Add subtle animations; honor reduced-motion preference. | Motion spec TBD |

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
- **Visual candidate:** `Tabi-Komorebi-Dusk-v1.5.4.html`, generated in ChatGPT, **not yet committed** or live. Verify file independently before adopting it as coding baseline.
- Treat these as separate version tracks until an explicit release.
