# Print247 — Editorial Quality Review

Deployable, static, dependency-free Vercel application for four writers and 18 audited Print247 articles.

## Deployment to Vercel

1. Extract the ZIP file into a folder, preserving all directories.
2. In Vercel, create a new project and import the folder from a GitHub repository (or deploy from the Vercel CLI).
3. Framework preset: **Other**. Root directory: folder containing `index.html` and `vercel.json`. Build command: leave empty. Output directory: leave empty (static project).
4. Deploy. Routes work as `/`, `/rankings`, `/writers/hassan`, `/writers/hassan/articles/1`, `/criteria`, and `/about`.

Vercel CLI alternate: run `npx vercel` from this folder and follow the prompts. A Vercel account and internet connection are required for deployment.

## Preview locally

Python 3: run `python -m http.server 8000` inside this folder, then visit `http://localhost:8000`. Note that deep-link refreshes on Python's default server are not SPA-rewritten; Vercel handles them via `vercel.json`.

## Routes and navigation

- `/` — management KPIs, writer ranking, cross-writer dimension matrix, priority findings.
- `/rankings` — ranked comparison, sampling caveats, CSV export.
- `/writers/{writer}` — writer-level 8-aspect diagnostics, strong points, repeated issue themes, five/three article links.
- `/writers/{writer}/articles/{number}` — original article score, all eight dimensions, issue-level evidence, 52 source checks, and local correction checklist.
- `/criteria` — eight original weights, all 52 original question definitions, suggested score threshold (default 70/100), status definitions, scoring formula.
- `/about` — sources, scope and limitations.

## Source & scoring integrity

- The application does not perform a new audit or independently recompute each dimension from 52 PASS/FAIL results. Original source ratings and provisional scores are shown unchanged.
- Writer score = mean of available article scores. Hassan 67.8, Mohsin 61.6, Fizza 57.6, Maryam 57.0. Maryam has **3** articles; others have **5**.
- 168 distinct issue IDs are displayed; a single issue can reference multiple checks without being independently penalized by each.
- "Strong points" = number of article × scoring dimension ratings 4 or 5 out of 5; does NOT mean 43 uniquely validated positive facts. The checklist PASS count is shown separately.
- Repeated writer-level themes are heuristic keyword groupings of issue titles/rationales. One issue may appear under more than one theme. They DO NOT modify scores or unique counts.
- At the eight-dimension level, PASS is defined by suggested display policy rating >=3/5; FAIL <3/5; N/A if truly unrated. It is *not* an official management policy.
- Suggested score benchmark 70/100 is editable (50-90). It is a proposal requiring management approval, not an original prescribed passing threshold, and it never changes the ranking or saved source scores.
- Critical issues are flagged for manual release review, not silently reweighted.
- 40 checks are `not_verified`; 1 check is `na`. Neither is treated as a FAIL.
- 33 failed checks do not currently link to a distinct recorded issue. The 52-check view explicitly flags this evidence/action-mapping gap; audit source records are not silently modified.
- 168 evidence PNGs are annotated source excerpt exhibits, NOT live webpage screenshots. No false screenshot claims are made.
- Writer assignments came from user-provided internal assignments and can differ from public site bylines.
- Corrections marked as reviewed are stored *only* in the browser localStorage; the source audit never changes. Export the correction progress JSON to share it.

## Files

- `index.html`, `styles.css`, `app.js` — browser app (no build dependencies).
- `vercel.json` — deep-link static SPA routing.
- `data/audits.js`, `data/audits.json` — normalized source data and counters.
- `data/original/{writer}-{article}.json` — original, unmodified input audit JSON.
- `assets/evidence/...` — original annotated source-excerpt PNGs from audit packages.

## Updating and access

This is a static report. To update shared scores, regenerate the source dataset from new versioned audit JSON files and redeploy. This app does **not** include authentication or a writable server. A production deployment containing employee evaluations should be restricted using Vercel's available deployment protection/access controls. Do not distribute a publicly accessible Vercel link without reviewing whether it exposes private staff evaluations.
