---
title: Add Relevant FAQs
description: Learn how LLM Optimizer identifies high-traffic pages that lack structured Q&A content for AI agents, and how to review and deploy AI-generated FAQs with Optimize at Edge.
feature: Opportunities
---

# Add Relevant FAQs

The Add Relevant FAQs opportunity identifies high-traffic pages that lack structured Q&A content that AI agents often rely on when generating responses. It introduces relevant, **intent-aligned FAQ** content grounded in your existing page material. This helps agents match user questions to your content more directly.

For each affected URL, you can review AI-generated FAQ suggestions, then deploy them with [Optimize at Edge](/help/dashboards/optimize-at-edge/overview.md) so agentic traffic receives clearer Q&A context with no Content Management system (CMS) changes required.

## How Optimize at Edge fixes the problem

Fixes are applied using [Optimize at Edge](/help/dashboards/optimize-at-edge/overview.md), which:

- Serves a **pre-rendered HTML snapshot** to AI agents.
- **Enriches the page** with FAQ content in the HTML they retrieve.
- Works at the **CDN layer** (no CMS changes).
- Is **AI-only**—no impact on human visitors or SEO bots.
- **Deploys in minutes** and is **fully reversible** from the LLM Optimizer interface.

## How it works

LLM Optimizer identifies high-traffic pages where Q&A content is missing or thin, based on your brand’s prompt set. Affected URLs appear in the **URLs with suggestions** table on the **Current Suggestions** tab, where you can expand a row to inspect each recommendation.

![URLs with suggestions on Current Suggestions, expanded row with FAQ prompts and AI-generated answers](/help/dashboards/opportunities/assets/add-relevant-faqs-expand.png)

Each expanded entry lists the FAQ **prompts**, **AI-generated** suggested answers, brief **reasoning**, and **sources** tied to the page. The table also shows how many FAQs are suggested per URL and **Agentic traffic (4 weeks)** to help you prioritize.

Click **Preview** on a row to open the optimization preview. The modal compares **how your page looks now** for agentic traffic with the **post-optimization** view (for example, the new **FAQs** block). Previews can span multiple steps when several items are in scope (for example **1 of 5** in the modal header).

![Preview optimizations modal comparing current vs post-optimization agent view with FAQs](/help/dashboards/opportunities/assets/add-relevant-faqs-ui-01.png)

## URLs with suggestions

The **URLs with suggestions** table lists pages where FAQs would help AI-driven discovery. For each URL you can:

- **Expand the row** to view the proposed FAQ content for that page.
- **Preview** the before-and-after comparison for agentic traffic.
- **Mark as Fixed** if you addressed the opportunity outside LLM Optimizer.
- **Ignore** suggestions that are not relevant.

Suggestions are organized into **Current Suggestions**, **Fixed Suggestions**, and **Ignored Suggestions**.

Select the FAQ suggestions you want to ship using the row checkboxes. The footer shows how many are selected and provides **Mark as Fixed**, **Ignore Suggestions**, and **Deploy optimizations**.

![Selected FAQ suggestions on Current Suggestions with Deploy optimizations](/help/dashboards/opportunities/assets/add-relevant-faqs-ui-02.png)

## Deploying the optimization

When you are ready to publish at the edge, click **Deploy optimizations**. A **Deploy to Edge** dialog lists the URLs, questions, and answers you are about to push. Review the list, then choose **Deploy** or **Cancel**.

![Deploy to Edge dialog](/help/dashboards/opportunities/assets/add-relevant-faqs-ui-03.png)

After a successful deploy, **Deployment Complete** confirms how many optimizations went live and notes that AI agents may take time to index the update. Close the dialog and open **Fixed Suggestions** to verify status.

![Deployment Complete confirmation](/help/dashboards/opportunities/assets/add-relevant-faqs-ui-04.png)

>[!NOTE]
>
>Deploying optimizations requires completing the Optimize at Edge onboarding process. If you have not yet onboarded, clicking **Deploy optimizations** will direct you to the onboarding process. For full details on how Optimize at Edge works, supported CDN providers, and the onboarding process, see the [Optimize at Edge](/help/dashboards/optimize-at-edge/overview.md) page.

## Fixed Suggestions and View Live

On **Fixed Suggestions**, deployed URLs show **Optimized** in the status column. Expand a row to review the live FAQ content, use **Details** for analytics, or click **View Live** to open a read-only view of **current page content** as served for verification (including the injected **FAQs** section).

![Fixed Suggestions with Optimized status, View Live, and Rollback](/help/dashboards/opportunities/assets/add-relevant-faqs-fixed.png)

The **View Live** window shows the page structure and FAQ copy as presented in that check (for example, **Frescopa Coffee** with **Bagged Coffee**, **Coffee Pods**, and **FAQs**).

![View Live — current page content including FAQs](/help/dashboards/opportunities/assets/add-relevant-faqs-ui-05.png)

From the same **Fixed Suggestions** view, select the optimized rows you want to revert, then click **Rollback** in the header.

## Rollback

The **Rollback** dialog lists the suggestions that will be removed from production, with a short warning that deployed optimizations will be reverted. Confirm the list, then click **Rollback** or **Cancel**.

![Rollback dialog listing suggestions to revert](/help/dashboards/opportunities/assets/add-relevant-faqs-ui-07.png)

When the operation finishes, a **Successfully Rolled Back** summary appears; close it to return to the dashboard.

![Rollback complete — Successfully Rolled Back](/help/dashboards/opportunities/assets/add-relevant-faqs-ui-08.png)

## Try it in the demo

Explore the Add Relevant FAQs workflow in the [Frescopa demo](https://play.llmo.now/org/demo-org).

## Frequently asked questions

**Will this optimization affect my human visitors or SEO bots?**

No. Optimize at Edge targets only AI user agents. Human visitors and SEO bots receive the original page as before.

**Do I need to change my CMS or involve developers?**

No. FAQs are applied at the CDN edge. Once onboarded to Optimize at Edge, you can deploy and roll back from the LLM Optimizer interface.

**What happens if my page content changes after I deploy?**

For content opportunities such as Add Relevant FAQs, LLM Optimizer monitors the source page for changes. If a change is detected, the optimization is paused and flagged for human review to prevent drift between the agent-visible page and the human-visible page. See the [Optimize at Edge](/help/dashboards/optimize-at-edge/overview.md) frequently asked questions for more detail.

**How do I get started with Optimize at Edge?**

See the [Optimize at Edge](/help/dashboards/optimize-at-edge/overview.md) page for onboarding, CDN configuration guides, and prerequisites.
