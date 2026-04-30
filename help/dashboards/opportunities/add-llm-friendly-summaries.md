---
title: Add LLM-friendly Summaries
description: Learn how LLM Optimizer identifies high-traffic pages that lack concise summaries and key points for AI agents, and how to review and deploy them with Optimize at Edge.
feature: Opportunities
---

# Add LLM-friendly Summaries

The Add LLM-friendly Summaries opportunity identifies high-traffic pages that lack concise structured summaries, which makes it harder for AI agents to quickly understand key information on the page. It introduces clear summaries and key points grounded in your existing page content. This helps agents interpret and capture important brand claims more efficiently and increases the likelihood that your content is included accurately in AI responses.

For each affected URL, you can review AI-generated suggestions, then deploy them with [Optimize at Edge](/help/dashboards/optimize-at-edge/overview.md) so agentic traffic gets clearer, scannable context with no Content Management system (CMS) changes required.

## How it fixes the problem

Fixes are applied using [Optimize at Edge](/help/dashboards/optimize-at-edge/overview.md), which:

- Serves a pre-rendered HTML snapshot to AI agents.
- Enriches the page with summaries and/or key points in the HTML they retrieve.
- Works at the CDN layer (no CMS changes).
- Is AI-only — no impact on human visitors or SEO bots.
- Deploys in minutes and is **fully reversible** from the LLM Optimizer interface.

## How it works

LLM Optimizer identifies high-traffic pages where page or section-level **summaries** and **key points** would help AI comprehension. Affected URLs appear in the **URLs with suggestions** table on the **Current Suggestions** tab, where you can expand a row to inspect each recommendation.

![URLs with suggestions on Current Suggestions, expanded row with page and section summary suggestions](/help/dashboards/opportunities/assets/add-llm-friendly-summaries-expand.png)

The **URLs with suggestions** table lists pages where summaries would help agentic discovery. Suggestions are organized into **Current Suggestions**, **Fixed Suggestions**, and **Ignored Suggestions**. For each URL you can:

- **Expand the row** to view the analysis and proposed summary text (and key points when included).
- **Preview** the before and after comparison for agentic traffic.
- **Mark as Fixed** if you addressed the opportunity outside LLM Optimizer.
- **Ignore** suggestions that are not relevant.

Each expanded entry shows page-level and section-level summary instructions, **AI-generated** copy, edit controls and context tied to the live page.

Click **Preview** in the **Actions** column to open the optimization preview. It compares how your page looks now for agentic traffic with the post-optimization view (for example, injected **summary** and **key point** content aligned to the suggested placements). You can open or dismiss that preview at any time before you deploy.

When you are ready to publish, select the summary and key point line items using the checkboxes. The footer shows how many are selected and provides **Mark as Fixed**, **Ignore Suggestions**, and **Deploy optimizations**.

![Current Suggestions with summary line items selected and Deploy optimizations in the footer](/help/dashboards/opportunities/assets/add-llm-friendly-summaries-select-url.png)

### Deploying the optimization

When you are ready to publish at the edge, click **Deploy optimizations**. A **Deploy to Edge** dialog lists the selected URLs and optimization details. Review the list, then choose **Deploy** or **Cancel**.

![Deploy to Edge dialog](/help/dashboards/opportunities/assets/add-llm-friendly-summaries-deploy-dialog.png)

After a successful deploy, **Deployment Complete** confirms how many optimizations went live and notes that AI agents may take time to index the update. Close the dialog and open **Fixed Suggestions** to verify status.

![Deployment Complete confirmation](/help/dashboards/opportunities/assets/add-llm-friendly-summaries-deploy-confirm.png)

>[!NOTE]
>
>Deploying optimizations requires completing the Optimize at Edge onboarding process. If you have not yet onboarded, clicking **Deploy optimizations** will direct you to the onboarding process. For full details on how Optimize at Edge works, supported CDN providers, and the onboarding process, see the [Optimize at Edge](/help/dashboards/optimize-at-edge/overview.md) page.

### Fixed Suggestions and View Live

On **Fixed Suggestions**, deployed URLs show **Optimized** in the status column. Expand a row to review deployed summary copy and instructions.

![Fixed Suggestions tab with Optimized status, expanded deployed summaries, View Live, and Details](/help/dashboards/opportunities/assets/add-llm-friendly-summaries-fixed.png)

Click **View Live** on the row to open a read-only view of **current page content** as served for verification (including injected **summary** and **key point** blocks where applied). Use **Details** for analytics. When you need to revert edge changes in bulk, select the optimized rows using the checkboxes, then use **Rollback** in the header.

![Fixed Suggestions with checkboxes for bulk selection before Rollback](/help/dashboards/opportunities/assets/add-llm-friendly-summaries-select-in-fixed.png)

## Rollback

If you change your mind, you can roll back any deployed optimization. From the **Fixed Suggestions** view, select the optimized rows you want to revert, then click **Rollback** in the header.

The **Rollback** dialog lists the suggestions that will be rolled back, with a short warning that deployed optimizations will be reverted. Confirm the list, then click **Rollback** or **Cancel**.

![Rollback dialog listing suggestions to revert](/help/dashboards/opportunities/assets/add-llm-friendly-summaries-rollback-dialog.png)

When the operation finishes, a **Successfully Rolled Back** summary appears; close it to return to the dashboard.

![Rollback complete — Successfully Rolled Back](/help/dashboards/opportunities/assets/add-llm-friendly-summaries-rollback-confirm.png)

## Try it in the demo

Explore the Add LLM-friendly Summaries workflow in the [Frescopa demo](https://play.llmo.now/org/demo-org).

<!-- ## Frequently asked questions

**Will this optimization affect my human visitors or SEO bots?**

No. Optimize at Edge targets only AI user agents. Human visitors and SEO bots receive the original page as before.

**Do I need to change my CMS or involve developers?**

No. Summaries are applied at the CDN edge. Once onboarded to Optimize at Edge, you can deploy and roll back from the LLM Optimizer interface.

**What happens if my page content changes after I deploy?**

For content opportunities such as Add LLM-friendly Summaries, LLM Optimizer monitors the source page for changes. If a change is detected, the optimization is paused and flagged for human review to prevent drift between the agent-visible page and the human-visible page. See the [Optimize at Edge](/help/dashboards/optimize-at-edge/overview.md) frequently asked questions for more detail.

**How do I get started with Optimize at Edge?**

See the [Optimize at Edge](/help/dashboards/optimize-at-edge/overview.md) page for onboarding, CDN configuration guides, and prerequisites.-->
