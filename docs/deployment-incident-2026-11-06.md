# GitHub Pages deployment incident — 2026-11-06

## Outcome
The November 6 newsletter issue was committed at `site/issues/2026-11-06.html` and the archive was updated. After several failed GitHub Pages deployments, **workflow run [42288326440](https://github.com/bobbygrdn/AI-and-Agentic-Development-Newsletter/actions/runs/42288326440)** completed successfully on November 6, 2026 (20:26 UTC). The site owner subsequently confirmed that the [public issue page](https://bobbygrdn.github.io/AI-and-Agentic-Development-Newsletter/issues/2026-11-06.html) was live. This is user confirmation, not an independently recorded HTTP check.

## Timeline and evidence

| Run | Result | Evidence |
| --- | --- | --- |
| [42266464884](https://github.com/bobbygrdn/AI-and-Agentic-Development-Newsletter/actions/runs/42266464884), attempt 1 | Failed | Checkout, Pages configuration and artifact upload succeeded. The deployment remained `deployment_queued` for several minutes, then emitted `Deployment failed, try again later.` |
| 42266464884, attempt 2 | Failed | Re-running failed jobs within the same workflow run produced `Multiple artifacts named "github-pages" were unexpectedly found for this workflow run. Artifact count is 2.` |
| [42268053476](https://github.com/bobbygrdn/AI-and-Agentic-Development-Newsletter/actions/runs/42268053476) | Failed | Fresh run avoided the duplicate-artifact error, but Pages again remained `deployment_queued` before failing with `Deployment failed, try again later.` |
| [42288326440](https://github.com/bobbygrdn/AI-and-Agentic-Development-Newsletter/actions/runs/42288326440) | **Succeeded** | Fresh run from commit `c0cf05cc4ee571af72b4c142fc4c8efe8494d3e1` completed successfully. |

## Changes made

- Kept the existing newsletter issue and archive entries intact.
- Added a `workflow_dispatch` trigger to `.github/workflows/pages.yml`, allowing a **fresh workflow run** without changing newsletter content. Existing `push` trigger remains.
- Upgraded `actions/checkout@v4` to `actions/checkout@v5` in commit `c0cf05cc4ee571af72b4c142fc4c8efe8494d3e1`. Checkout v5 uses a Node.js 24 action runtime, addressing the observed Node.js 20 compatibility/deprecation warning for checkout.
- Retained `actions/configure-pages@v5`, `actions/upload-pages-artifact@v4`, and `actions/deploy-pages@v4`; no evidence established these version references were incorrect.

**Causality caveat:** The successful run followed the checkout upgrade and a fresh workflow invocation, but this does **not** prove that the checkout upgrade fixed the Pages queue failure. The first and third failures occurred after successful artifact uploads, suggesting a Pages deployment-service/queue issue; the underlying cause was not conclusively established.

## Recovery runbook for future issues

1. Inspect the **latest** workflow run and the failed job's step logs; distinguish build/artifact failures from `Deploy to GitHub Pages` failures.
2. If `deployment_queued` stalls and then fails, check [GitHub Status](https://www.githubstatus.com/) for Pages/Actions incidents and review the deployment logs. Do not assume a newsletter HTML or Node.js error without evidence.
3. **Do not re-run failed jobs in the same run** if it has already uploaded a `github-pages` artifact: this workflow may upload a second artifact with the same name and cause the duplicate-artifact error.
4. Instead, trigger a **new** run using the workflow's `workflow_dispatch` entry, or make a necessary workflow fix on `main` that starts a new run. Avoid dummy edits to published issues or archive pages.
5. Ensure `contents: read`, `pages: write`, and `id-token: write` remain present. Keep action versions current and compatible with GitHub's supported action runtimes.
6. Confirm the new run concludes `success`, then verify the exact public issue URL returns the expected dated issue content. A successful Actions run alone is not a substitute for public-page verification.
7. Before emailing subscribers, check whether that issue's notification has already been sent; send only once after successful deployment **and** live-page verification.
8. If failures recur, record the new run ID, timestamp, exact failing step, and error message here rather than blindly retrying.

## Operational note

This incident does not establish that Node.js runtime warnings are fatal. Treat such warnings as maintenance signals, and evaluate them separately from the actual failed step.
