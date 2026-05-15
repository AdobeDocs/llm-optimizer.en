---
title: Simplify Complex Content
description: Learn how LLM Optimizer identifies high-traffic pages with dense copy that is hard for AI agents to interpret, and how to review and deploy simplified text with Optimize at Edge.
feature: Opportunities
autotag-review: '2026-05-15T17:58:39.879Z'
TQID: 'https://experienceleague.adobe.com/wO3ZY-fEgOi7cD4dq0kCltk-YJSD431bkA6-9PW42Lo'
product_v2:
  - id: d830747e-f8f3-4fce-8eff-d53b333b1639
    internal-label: LLM Optimizer
feature_v2:
  - id: c0713b97-4af8-4c41-b742-5afcc6ced468
    internal-label: Insights
subfeature_v2:
  - id: e1b649f0-0a61-46e4-9082-64d5cb2576c6
    internal-label: Opportunities
topic_v2:
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
    internal-label: Optimization
---

# Simplify Complex Content

The Simplify Complex Content opportunity identifies high-traffic pages where dense or complex text which makes it harder for AI agents to interpret key information. It introduces clearer, easier-to-scan versions of the existing copy while preserving the original meaning. This helps agents parse, summarize, and extract important information more reliably.

For each affected URL, you can review **Improved Text** suggestions, compare them with **Preview**, then deploy them with [Optimize at Edge](/help/dashboards/optimize-at-edge/overview.md) so agentic traffic receives clearer HTML with no Content Management system (CMS) changes required.

## How it fixes the problem

Fixes are applied using [Optimize at Edge](/help/dashboards/optimize-at-edge/overview.md), which:

- Serves a pre-rendered HTML snapshot to AI agents.
- Updates the agent-visible page so complex passages are replaced or augmented with **Improved Text** aligned to the live page.
- Works at the CDN layer (no CMS changes).
- Is AI-only — no impact on human visitors or SEO bots.
- Deploys in minutes and is **fully reversible** from the LLM Optimizer interface.

## How it works

LLM Optimizer identifies pages that receive high agentic traffic and where content scores below readability thresholds, then suggests rewrites of the copy. For each page you have:

**Improved Text** - simplified content grounded in what is already on the page.
**Preview** - a before and after comparison for agentic traffic.

Affected URLs appear in the **URLs with suggestions** table on the **Current Suggestions** tab, where you can expand a row to inspect each recommendation.

![URLs with suggestions on Current Suggestions, expanded row with Improved Text and Preview](/help/dashboards/opportunities/assets/simplify-complex-content-expand.png)

The **URLs with suggestions** table lists pages where simplified content would help agentic comprehension. Suggestions are organized into **Current Suggestions**, **Fixed Suggestions**, and **Ignored Suggestions**. For each URL you can:

- **Expand the row** to view **Improved Text** suggestions for that page.
- **Preview** the before and after comparison for agentic traffic.
- **Mark as Fixed** if you addressed the opportunity outside LLM Optimizer.
- **Ignore** suggestions that are not relevant.

**Views** include **Current Suggestions**, **Fixed Suggestions** (status **Optimized** when deployed), and **Ignored Suggestions**. You can verify live deployment using **View Live** on **Fixed Suggestions** and roll back anytime.

Select the URLs or line items with **Improved Text** you want to ship using the checkboxes, then use **Mark as Fixed**, **Ignore Suggestions**, or **Deploy optimizations** in the **Opportunity plan** header. The demo UI also shows a selection count and related actions with the list.

![Opportunity plan, Current Suggestions, expanded row, and Deploy optimizations in the plan header](/help/dashboards/opportunities/assets/simplify-complex-content-select.png)

### Deploying the optimization

When you are ready to publish at the edge, click **Deploy optimizations**. A **Deploy to Edge** dialog lists the selected URLs and optimization details. Review the list, then choose **Deploy** or **Cancel**.

![Deploy to Edge dialog](/help/dashboards/opportunities/assets/simplify-complex-content-deploy-dialog.png)

After a successful deploy, **Deployment Complete** confirms how many optimizations went live and notes that AI agents may take time to index the update. Close the dialog and open **Fixed Suggestions** to verify status.

![Deployment Complete confirmation](/help/dashboards/opportunities/assets/simplify-complex-content-deploy-confirm.png)

>[!NOTE]
>
>Deploying optimizations requires completing the Optimize at Edge onboarding process. If you have not yet onboarded, clicking **Deploy optimizations** will direct you to the onboarding process. For full details on how Optimize at Edge works, supported CDN providers, and the onboarding process, see the [Optimize at Edge](/help/dashboards/optimize-at-edge/overview.md) page.

### Fixed Suggestions and View Live

On **Fixed Suggestions**, deployed URLs show **Optimized** in the status column. Expand a row to review deployed **Improved Text** and instructions.

![Fixed Suggestions tab with Optimized status, expanded simplified copy, View Live, and Details](/help/dashboards/opportunities/assets/simplify-complex-content-fixed.png)

Click **View Live** on the row to open a read-only view of **current page content** as served for verification (including simplified passages where applied). Use **Details** for analytics.

![View Live — current page content including simplified text for agents](/help/dashboards/opportunities/assets/simplify-complex-content-view-live.png)

When you need to revert edge changes in bulk, select the optimized rows using the checkboxes, then use **Rollback** in the header.

![Fixed Suggestions with the deployed row expanded, Optimized status, and Rollback in the header](/help/dashboards/opportunities/assets/simplify-complex-content-rollback.png)

## Rollback

If you change your mind, you can roll back any deployed optimization. From the **Fixed Suggestions** view, select the optimized rows you want to revert, then click **Rollback** in the header.

The **Rollback** dialog lists the suggestions that will be rolled back, with a short warning that deployed optimizations will be reverted. Confirm the list, then click **Rollback** or **Cancel**.

![Rollback dialog listing suggestions to revert](/help/dashboards/opportunities/assets/simplify-complex-content-rollback-dialog.png)

When the operation finishes, a **Successfully Rolled Back** summary appears; close it to return to the dashboard.

![Rollback complete — Successfully Rolled Back](/help/dashboards/opportunities/assets/simplify-complex-content-rollback-confirm.png)

## Try it in the demo

Explore the Simplify Complex Content workflow in the [Frescopa demo](https://play.llmo.now/org/demo-org).
