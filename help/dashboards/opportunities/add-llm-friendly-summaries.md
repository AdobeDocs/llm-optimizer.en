---
title: Add LLM-friendly Summaries
description: Learn how LLM Optimizer identifies pages that lack concise summaries for AI agents and how to add AI-generated summaries using Optimize at Edge.
feature: Opportunities
---

# Add LLM-friendly Summaries

AI systems work best when they can quickly grasp what a page is about. Long or complex pages without clear page or section-level summaries are harder for models to scan, interpret and cite accurately.

The Add LLM-friendly Summaries opportunity identifies those pages and recommends short, AI-generated summaries that capture the essential content. For each URL, you can review the suggestion, deploy it at the CDN edge with [Optimize at Edge](/help/dashboards/optimize-at-edge/overview.md), and validate the live experience for agentic traffic—with no Content Management system (CMS) changes required.

This opportunity can be optimized by using [Optimize at Edge](/help/dashboards/optimize-at-edge/overview.md). Optimizations are delivered exclusively to AI agents with no impact on human visitors (bot-only delivery). Summaries are inserted into the HTML that agents retrieve, improving how models interpret and describe your content.

## How it works

LLM Optimizer flags pages where summaries would help AI comprehension. Affected URLs appear in the **URLs with suggestions** table on **Current Suggestions**. Expand a row to review the AI analysis and the proposed page- or section-level summary text.

![Expanded row with page and section summary suggestions](/help/dashboards/opportunities/assets/add-llm-friendly-summaries-expand.png)

Select the URL row and the individual suggestions you want to deploy. The footer shows how many suggestions are selected and enables **Deploy optimizations** when you are ready.

![Select suggestions and Deploy optimizations](/help/dashboards/opportunities/assets/add-llm-friendly-summaries-select-url.png)

## URLs with suggestions

The **URLs with suggestions** table lists pages with recommended summaries. For each URL you can:

- **Expand the row** to view the analysis and proposed summary text.
- **Preview** the side-by-side comparison of the current page versus the version with summaries applied.
- **Mark as Fixed** once the issue has been addressed outside LLM Optimizer, if applicable.
- **Ignore** suggestions that are not relevant.

Suggestions are organized into **Current Suggestions**, **Fixed Suggestions**, and **Ignored Suggestions**.

## Deploying the optimization

When you are ready to publish summaries at the edge, click **Deploy optimizations**. A confirmation dialog lists the selected URLs, optimization type (for example Full Page or Section), and summary text before you confirm.

![Deploy to Edge dialog](/help/dashboards/opportunities/assets/add-llm-friendly-summaries-deploy-dialog.png)

After deployment, a **Deployment Complete** message confirms which URLs were successfully optimized and reminds you that you can review them under **Fixed Suggestions**.

![Deployment complete confirmation](/help/dashboards/opportunities/assets/add-llm-friendly-summaries-deploy-confirm.png)

>[!NOTE]
>
>Deploying optimizations requires completing the Optimize at Edge onboarding process. If you have not yet onboarded, clicking **Deploy optimizations** will direct you to the onboarding process. For full details on how Optimize at Edge works, supported CDN providers and the onboarding process, see the [Optimize at Edge](/help/dashboards/optimize-at-edge/overview.md) page.

## Fixed Suggestions and live verification

After you deploy, optimized URLs appear under **Fixed Suggestions** with an **Optimized** status. Expanded rows show each deployed summary with a **Deployed** (or similar) status so you can confirm what is live at the edge.

![Fixed suggestions with Optimized status](/help/dashboards/opportunities/assets/add-llm-friendly-summaries-fixed.png)

Select URLs or suggestions here to use **View Live** (verify agentic traffic) or **Rollback** when you want to revert.

![Select URLs in Fixed Suggestions](/help/dashboards/opportunities/assets/add-llm-friendly-summaries-select-in-fixed.png)

## Rollback

Open **Rollback** to see which deployed suggestions will be removed from production, then choose **Rollback** or **Cancel**.

![Rollback dialog listing suggestions to revert](/help/dashboards/opportunities/assets/add-llm-friendly-summaries-rollback-dialog.png)

After a successful rollback, a summary modal confirms what was reverted. **Fixed Suggestions** may show no rows for that URL until new suggestions are available.

![Successfully rolled back summary](/help/dashboards/opportunities/assets/add-llm-friendly-summaries-rollback-confirm.png)

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
