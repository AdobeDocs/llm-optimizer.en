---
title: Add LLM-friendly Summaries
description: Learn how LLM Optimizer identifies high-traffic pages that lack concise summaries and key points for AI agents, and how to review and deploy them with Optimize at Edge.
feature: Opportunities
---

# Add LLM-friendly Summaries

The Add LLM-friendly Summaries opportunity identifies high-traffic pages that lack concise structured summaries, which makes it harder for AI agents to quickly understand key information on the page. It introduces clear summaries and key points grounded in your existing page content. This helps agents interpret and capture important brand claims more efficiently and increases the likelihood that your content is included accurately in AI responses.

For each affected URL, you can review AI-generated suggestions, then deploy them with [Optimize at Edge](/help/dashboards/optimize-at-edge/overview.md) so agentic traffic gets clearer, scannable context with no Content Management system (CMS) changes required.

## How Optimize at Edge fixes the problem

Fixes are applied by using [Optimize at Edge](/help/dashboards/optimize-at-edge/overview.md), which:

- Serves a pre-rendered HTML snapshot to AI agents.
- Enriches the page with summaries and/or key points in the HTML they retrieve.
- Works at the CDN layer (no CMS changes).
- Is AI-only no impact on human visitors or SEO bots.
- Deploys in minutes and is fully reversible from the LLM Optimizer interface.

## How it works

LLM Optimizer flags high-traffic pages where summaries and structured key points would help AI comprehension. Affected URLs appear in the **URLs with suggestions** table, where you can select a URL to work with.

For each page, you have the following:

- A page or section-level summary and (when suggested) key points derived from the live content.
- A Preview side-by-side comparison of the current page versus the version with summaries applied.

![Select a URL with a summary suggestion](/help/dashboards/opportunities/assets/add-llm-friendly-summaries-select-url.png)

Expand a row to review the AI analysis and the proposed summary (and key points, if present) for that page.

![Expanded row with summary details](/help/dashboards/opportunities/assets/add-llm-friendly-summaries-expand.png)

## URLs with suggestions

The **URLs with suggestions** table lists pages with recommended summaries. For each URL you can:

- **Expand the row** to view the analysis and proposed summary text (and key points when included).
- **Preview** the side-by-side comparison of the current page versus the version with summaries applied.
- **Mark as Fixed** once the issue has been addressed outside LLM Optimizer, if applicable.
- **Ignore** suggestions that are not relevant.

Suggestions are organized into **Current Suggestions**, **Fixed Suggestions**, and **Ignored Suggestions**. After you deploy, optimized URLs appear under **Fixed Suggestions** with an **Optimized** status.

![Fixed suggestions with Optimized status](/help/dashboards/opportunities/assets/add-llm-friendly-summaries-fixed.png)

From **Fixed Suggestions**, you can select URLs to verify deployment, use **View Live** to confirm what agentic traffic receives, or start a rollback.

![Select URLs in Fixed Suggestions](/help/dashboards/opportunities/assets/add-llm-friendly-summaries-select-in-fixed.png)

## Deploying the optimization

When you are ready to publish summaries at the edge, select the URLs that have summary and/or key point suggestions, then click **Deploy optimizations**. A confirmation dialog lists the selected URLs and the optimization type before you confirm.

![Deploy to Edge dialog](/help/dashboards/opportunities/assets/add-llm-friendly-summaries-deploy-dialog.png)

After deployment, a confirmation screen shows which URLs were successfully optimized. The changes are live for AI agents and you can review deployed items anytime under **Fixed Suggestions**.

![Deploy confirmation](/help/dashboards/opportunities/assets/add-llm-friendly-summaries-deploy-confirm.png)

>[!NOTE]
>
>Deploying optimizations requires completing the Optimize at Edge onboarding process. If you have not yet onboarded, clicking **Deploy optimizations** will direct you to the onboarding process. For full details on how Optimize at Edge works, supported CDN providers and the onboarding process see the [Optimize at Edge](/help/dashboards/optimize-at-edge/overview.md) page.

## Rollback

If you change your mind, you can roll back a deployed summary optimization from **Fixed Suggestions**. Rollback uses a confirmation dialog so you can review the affected URLs before reverting to the previous agent-visible version.

![Rollback dialog](/help/dashboards/opportunities/assets/add-llm-friendly-summaries-rollback-dialog.png)

![Rollback confirmation](/help/dashboards/opportunities/assets/add-llm-friendly-summaries-rollback-confirm.png)

## Try it in the demo

Explore the Add LLM-friendly Summaries workflow in the [Frescopa demo](https://play.llmo.now/org/demo-org).

## Frequently asked questions

**Will this optimization affect my human visitors or SEO bots?**

No. Optimize at Edge targets only AI user agents. Human visitors and SEO bots receive the original page as before.

**Do I need to change my CMS or involve developers?**

No. Summaries are applied at the CDN edge. Once onboarded to Optimize at Edge, you can deploy and roll back from the LLM Optimizer interface.

**What happens if my page content changes after I deploy?**

For content opportunities such as Add LLM-friendly Summaries, LLM Optimizer monitors the source page for changes. If a change is detected, the optimization is paused and flagged for human review to prevent drift between the agent-visible page and the human-visible page. See the [Optimize at Edge](/help/dashboards/optimize-at-edge/overview.md) frequently asked questions for more detail.

**How do I get started with Optimize at Edge?**

See the [Optimize at Edge](/help/dashboards/optimize-at-edge/overview.md) page for onboarding, CDN configuration guides, and prerequisites.
