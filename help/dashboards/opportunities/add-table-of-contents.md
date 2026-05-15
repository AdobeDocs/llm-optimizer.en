---
title: Add Table of Contents
description: Learn how LLM Optimizer identifies high-traffic pages that lack a clear navigational structure for AI agents, and how to review and deploy a Table of Contents with Optimize at Edge.
feature: Opportunities
autotag-review: '2026-05-15T17:29:21.334Z'
TQID: 'https://experienceleague.adobe.com/A-Oxmmn-Cb4l9-iVx1TAKxvBTEOxRIAnRe1w1PqF6OI'
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

# Add Table of Contents

>[!NOTE]
>
> **Early access** — This capability is available in Early Access. Availability, eligibility and parts of the workflow may change as the capability matures. Contact your Adobe account team if you have questions about access.

The Add Table of Contents opportunity identifies high-traffic pages that lack a clear **Table of Contents** and structural guide, which makes it harder for AI agents to parse the page and map user queries to the right sections. It introduces a structured Table of Contents with **anchor-linked headings** that reflect the main sections of the page. This structure helps agents extract, map and cite relevant passages more reliably.

For each affected URL, you can review suggested Table of Contents entries, then deploy them with [Optimize at Edge](/help/dashboards/optimize-at-edge/overview.md) so agentic traffic receives clearer navigational context with no Content Management system (CMS) changes required.

## How it fixes the problem

Fixes are applied using [Optimize at Edge](/help/dashboards/optimize-at-edge/overview.md), which:

- Serves a pre-rendered HTML snapshot to AI agents.
- Adds a Table of Contents to the page.
- Works at the CDN layer (no CMS changes).
- Is AI-only — no impact on human visitors or SEO bots.
- Deploys in minutes and is **fully reversible** from the LLM Optimizer interface.

## How it works

LLM Optimizer identifies high-traffic pages where a **Table of Contents** would improve how AI agents navigate headings and sections. For each page, suggestions are grounded in headings already on the page so the Table of Contents reflects the page structure.

Affected URLs appear in the **URLs with suggestions** table on the **Current Suggestions** tab.

On **Current Suggestions**, for each URL you can:

- **Expand the row** to inspect the proposed Table of Contents (parsed from on-page headings and presented as anchor-linked entries).
- **Preview** a before and after comparison.
- **Mark as Fixed** if you addressed the opportunity outside LLM Optimizer.
- **Ignore** suggestions that are not relevant.

Suggestions are organized into **Current Suggestions**, **Fixed Suggestions**, and **Ignored Suggestions**, consistent with other Optimize at Edge opportunities.

### Deploying the optimization

When you are ready to publish at the edge, select the Table of Contents suggestions you want to deploy. The footer summarizes how many items are selected and typically offers **Mark as Fixed**, **Ignore Suggestions**, and **Deploy optimizations**.

Click **Deploy optimizations**. A **Deploy to Edge** dialog lists the selected URLs and optimization details. Review the list, then choose **Deploy** or **Cancel**.

After a successful deploy, **Deployment Complete** confirms how many optimizations went live. Close the dialog and open **Fixed Suggestions** to verify status.

>[!NOTE]
>
>Deploying optimizations requires completing the Optimize at Edge onboarding process. If you have not yet onboarded, clicking **Deploy optimizations** will direct you to the onboarding process. For full details on how Optimize at Edge works, supported CDN providers, and the onboarding process, see the [Optimize at Edge](/help/dashboards/optimize-at-edge/overview.md) page.

### Fixed Suggestions and View Live

On **Fixed Suggestions**, deployed URLs show **Optimized** in the status column. Expand a row to review the deployed Table of Contents, use **Details** for analytics where available, or click **View Live** to open a read-only view of **current page content** as served for verification (including the injected **Table of Contents**).

When you need to revert edge changes in bulk, select the optimized rows using the checkboxes, then use **Rollback** in the header.

## Rollback

If you change your mind, you can roll back a deployed optimization. From the **Fixed Suggestions** view, select the optimized rows you want to revert, then click **Rollback** in the header.

The **Rollback** dialog lists the suggestions that will be rolled back, with a short warning that deployed optimizations will be reverted. Confirm the list, then click **Rollback** or **Cancel**.

When the operation finishes, a **Successfully Rolled Back** summary appears; close it to return to the dashboard.
