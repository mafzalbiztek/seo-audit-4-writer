# Print247 · Balanced Editorial Review (Vercel static app)

A management-facing, read-only review platform for the latest Print247 content assessments of **Hassan, Mohsin, Maryam, and Fizza**.

## What you will see

- **Home** (`/`): 4-writer summary, current ranking, score metrics, writer strengths and retained issue counts.
- **Writer rankings** (`/rankings`): side-by-side current score and all eight scoring dimensions.
- **Writer profiles** (`/writers/hassan`, `/writers/mohsin`, `/writers/maryam`, `/writers/fizza`): personal mini-guide, article scores, strengths, retained issues and direct workbook download.
- **Individual articles** (`/writers/{writer}/articles/{number}`): article score, eight dimension ratings with rationale, exact current issues, correction recommendations, visual evidence exhibits, and the **52 diagnostic checks** with PASS / ACCEPTABLE / NEEDS IMPROVEMENT / FAIL / N/A / NOT VERIFIED filtering.
- **Evidence library** (`/evidence`): all 31 current workbooks' annotated excerpt exhibits; filters by writer, finding and search term.
- **Scoring policy** (`/criteria`): fixed weights, six status categories, proposed passing benchmark, non-penalizing safeguards, and limitations.
- **Downloads** (`/downloads`): four final Excel workbooks plus the unified current JSON dataset and individual writer JSON exports.

## Source-of-truth data (latest reviewed individual files)

| Writer | Score | Articles | Material FAIL | Needs improvement |
|:--|--:|--:|--:|--:|
| Hassan | 85.5 | 5 | 1 | 9 |
| Mohsin | 85.5 | 5 | 4 | 1 |
| Maryam | 82.8 | 3 | 2 | 3 |
| Fizza | 82.1 | 5 | 5 | 5 |

The site preserves the agreed balanced framework. **Do not import the previous strict audit JSON files into this site** or merge their scores with the current data. The old evaluation scores were superseded.

The scores are current editorial assessments, **not employment decisions**. Maryam's article sample is smaller (3 vs 5). The 70/100 threshold shown on the methodology page is a **proposed** management benchmark, not a Google SEO requirement or a formal HR policy.

## Evidence integrity

`assets/evidence/` contains 31 **newly generated annotated excerpt images** based only on current retained workbook issues and one approved non-scoring Pantone safeguard. These are **not actual webpage screenshots**, which could not be captured from the available environment.

Each exhibit includes the issue ID, named writer, original quoted excerpt from the current workbook, rationale, and link to the published article. The article itself is the source to inspect when more context is required. Removed findings and old evidence exhibits are not included.

## How to deploy this replacement to your existing Vercel project

1. Unzip this package on your computer. It already contains `index.html`, `app.js`, `styles.css`, `vercel.json`, `data/`, `assets/`, `downloads/`.
2. Open **GitHub Desktop** and select the repository **`seo-audit-4-writer`** on `main`. Choose **Repository → Show in Explorer**.
3. In the cloned repository, **remove old `data/`, `assets/` and old audit evidence folders** so that superseded strict data cannot remain publicly accessible. Leave `.git` in place. (Make a backup if you need old history.)
4. Copy **the contents of this unzipped package** (not its containing folder) into that repository. You should see `index.html` at the repository root.
5. In GitHub Desktop, inspect the changed files and confirm that `data/approved.js`, `data/approved.json`, `assets/evidence/*.png`, and all four `downloads/*.xlsx` files are present.
6. Commit as **`Replace strict content audits with finalized balanced review`** and click **Push origin**.
7. Vercel should automatically create a new deployment from `main`. On Vercel → **Deployments**, check that the source commit matches your new commit and status shows **Ready**. Visit the project domain and test the Writer, Article, Criteria, and Evidence pages.

For a new Vercel project: import the GitHub repository, use framework **Other**, root directory `./`, leave the build command unset, and deploy. `vercel.json` provides rewrites for direct article and writer URLs. This is a zero-dependency static website; there is no npm build step.

## Confidentiality — required before sharing with management

**This application includes named employee evaluations and downloadable workbooks.** It does **not** implement user authentication or authorization. A public GitHub repository, public Vercel deployment, or a “noindex” meta tag is NOT sufficient access control. Protect the repository and enable an appropriate Vercel deployment access-control method before sharing. Do not assume changing the repository to Private automatically restricts the deployed website.

## Files

```text
index.html
app.js
styles.css
vercel.json
README.md
data/
  approved.js     # browser-ready current dataset
  approved.json   # readable unified current dataset
assets/
  favicon.svg
  evidence/       # 31 annotated current-workbook exhibits
downloads/
  Hassan_Latest_Evaluation.xlsx
  Mohsin_Latest_Evaluation.xlsx
  Maryam_Latest_Evaluation.xlsx
  Fizza_Latest_Evaluation.xlsx
```

## Audit checks performed

- JavaScript syntax verified with Node.js.
- All **18 article routes** and **four writer routes** exist in the data.
- **936 diagnostic checks** verified (Hassan 260, Mohsin 260, Fizza 260, Maryam 156).
- Eight dimensions per article and weighted score consistency verified against the workbook data.
- Current issues: **12 material FAIL**, **18 NEEDS IMPROVEMENT**, **1 acceptable non-scoring safeguard**.
- All 31 evidence paths and all four source workbook downloads included.
- Page-content generation for all principal routes verified using a non-browser JavaScript test.

**Limitation:** A full graphical browser acceptance test was unavailable because the browser environment blocked even local navigation. The app is syntactically and structurally validated but should be smoke-tested on Vercel after deployment.
