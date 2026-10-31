# GitHub-only preview deployment design

Status: **proposed; not deployed**.

## Constraint
GitHub Pages has one active publishing source per repository. GitHub's built-in pull request Pages preview is not generally available. A second branch cannot simultaneously publish a separate Pages website using ordinary deployment configuration.

## Target
- Production: `https://aslanmamadiev.github.io/tabi/`
- Preview: `https://aslanmamadiev.github.io/tabi/preview/`
- Preview must have a visibly distinct banner and never auto-connect to real synced data.

## Safe deployment design (requires approval)
1. Introduce one GitHub Actions Pages publisher sourced from trusted `main`, with explicit permissions and production environment protection.
2. Assemble root production files from the approved `main` commit and a `preview/` subtree from a pinned candidate commit.
3. Deploy one Pages artifact containing both directories.
4. Only after testing and approval, merge the candidate to main, remove/advance preview, create tag and changelog.
5. Roll back with Git revert / previous release commit.

## Current implementation
- Candidate branch: `release/1.5.4-candidate`
- Draft PR: #1
- `candidate-checks.yml`: HTML and JS syntax checks, candidate downloadable Actions artifact.
- No hosted preview URL yet. No production Pages settings changed.
- Need explicit approval and deployment source inspection before switching Pages workflow.

## Privacy and storage
- Same-origin paths `/tabi/` and `/tabi/preview/` share localStorage because browser storage is origin-scoped, NOT path-scoped.
- Therefore **do not serve a live preview under /tabi/preview/** until the candidate code isolates storage keys (a CORE-01 exception needing separate approval), or preview uses a separate origin.
- Safest production-equivalent hosted test while preserving storage isolation: a separate GitHub Pages user/org or repo origin may be needed; another repository under the same github.io account does NOT isolate origin.
- Until a separate origin is confirmed, use test-only data and avoid logging in; offline candidate artifact plus isolated local test environment is safer than a shared-origin live preview.
