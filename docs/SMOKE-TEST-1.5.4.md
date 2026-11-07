# Tabi v1.5.4 · Pre-release smoke test

Date: 2026-10-31

## Test environment
Chromium headless, synthetic in-memory localStorage and randomUUID because the runner blocks local-file/localhost browsing. Network calls to Supabase were blocked. This is **not** an authentication, E2E, or true hosting test.

## Passed
- JavaScript initialized without page errors in synthetic context.
- Viewport widths 360px, 390px, 1280px: no horizontal document overflow.
- Sync/settings tiles had equal width/height and aligned Y positions; 44px at mobile, 48px desktop.
- Empty user starts with 4 room groups and zero items.
- Room quick-add saved one new item into local mock storage and updated total count.
- Settings opened and closed from the top-right close control.
- Kanban rendered four columns.

## Not yet tested
- Existing real user data migration and browser localStorage persistence on actual origin.
- Supabase authentication, encryption, realtime sync or conflict handling.
- Touch drag behavior, across-device browser differences, accessibility review, theme screenshots.
- Actual preview deployment to dedicated preview origin.

## Deployment safeguard
- Production `main` unchanged; draft PR #1 is not approved for merge.
- Dedicated hosted preview remains pending independent provider connection and configuration; do not embed account secrets in the preview.
