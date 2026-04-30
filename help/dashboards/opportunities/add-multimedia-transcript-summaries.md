---
title: Add Multimedia Transcript Summaries
description: Learn how LLM Optimizer identifies pages where key information is embedded in video without machine-readable text, and how to review and deploy AI-generated transcript summaries with Optimize at Edge.
feature: Opportunities
---

# Add Multimedia Transcript Summaries

>[!NOTE]
>
> **Early access** — Add Multimedia Transcript Summaries is available in Early Access. Availability, eligibility and parts of the workflow may change as the capability matures. Contact your Adobe account team or `llmo-at-edge@adobe.com` if you have questions about access.

The Add Multimedia Transcript Summaries opportunity identifies pages where important information lives in video or other media without transcripts or short text summaries that AI agents can read. It introduces **AI-generated transcript summaries** grounded in the media and surrounding page context. It helps recover key brand information that would otherwise be missed by making multimedia content understandable to AI agents.

For each affected URL, you can review the proposed **Content Patch**, **Implementation** details (for example, the target CSS selector and operation) and **Rationale**, then deploy with [Optimize at Edge](/help/dashboards/optimize-at-edge/overview.md) so agentic traffic receives the enriched HTML with no Content Management system (CMS) changes required.

## How it fixes the problem

Fixes are applied using [Optimize at Edge](/help/dashboards/optimize-at-edge/overview.md), which:

- Serves a pre-rendered HTML snapshot to AI agents.
- Enriches the page with transcript summary text in the HTML they retrieve (for example, near the relevant inline video).
- Works at the CDN layer (no CMS changes).
- Is AI-only — no impact on human visitors or SEO bots.
- Deploys in minutes and is **fully reversible** from the LLM Optimizer interface.

## How it works

LLM Optimizer flags high-traffic pages where machine-readable text is missing for embedded media, based on your configuration and page structure. Affected URLs appear in the **URLs with suggestions** table on the **Current Suggestions** tab, where you can expand a row to inspect each **Content Patch**, how it will be applied, and why it is recommended.

For each page, you have: 

**Multimedia Summary** –  Structured summaries derived from video content.
**Preview** – Before and after page comparison.

![URLs with suggestions on Current Suggestions, expanded row with Content Patch, Implementation details, and Rationale](/help/dashboards/opportunities/assets/add-multimedia-transcript-summaries-expand.png)

The **URLs with suggestions** table lists pages where transcript or summary text would help agentic discovery. Suggestions are organized into **Current Suggestions**, **Fixed Suggestions**, and **Ignored Suggestions**. For each URL you can:

- **Expand the row** to view the **Content Patch** text, **Implementation** details (including the planned DOM operation and CSS selector), and **Rationale** for the change.
- **Preview** the before and after comparison for agentic traffic.
- **Mark as Fixed** if you addressed the opportunity outside LLM Optimizer.
- **Ignore** suggestions that are not relevant.

You can edit patch text from the row when supported (pencil control), then use the row checkboxes to select what to deploy. The footer shows how many are selected and provides **Mark as Fixed**, **Ignore Suggestions**, and **Deploy optimizations**.

### Deploying the optimization

When you are ready to publish at the edge, click **Deploy optimizations**. A **Deploy to Edge** dialog lists the URLs, selectors and operations you are about to run. Review the list, then choose **Deploy** or **Cancel**.

![Deploy to Edge dialog for multimedia transcript summary content patches](/help/dashboards/opportunities/assets/add-multimedia-transcript-summaries-deploy-dialog.png)

After a successful deploy, **Deployment Complete** confirms how many optimizations went live. Close the dialog and open **Fixed Suggestions** to verify status.

![Deployment Complete confirmation](/help/dashboards/opportunities/assets/add-multimedia-transcript-summaries-deploy-confirm.png)

>[!NOTE]
>
> Deploying optimizations requires completing the Optimize at Edge onboarding process. If you have not yet onboarded, clicking **Deploy optimizations** will direct you to the onboarding process. For full details on how Optimize at Edge works, supported CDN providers, and the onboarding process, see the [Optimize at Edge](/help/dashboards/optimize-at-edge/overview.md) page.

### Fixed Suggestions and View Live

On **Fixed Suggestions**, deployed URLs show **Optimized** in the status column. Expand a row to review the live **Content Patch**, **Implementation** details and **Rationale** . Additionally, you can use **Details** for analytics or **View Live** where available to confirm what agentic traffic receives.

![Fixed Suggestions with Optimized status, expanded Content Patch, and Rollback](/help/dashboards/opportunities/assets/add-multimedia-transcript-summaries-fixed.png)

To roll back in bulk, select the optimized rows using the checkboxes, then use **Rollback** in the header.

![Fixed Suggestions with rows selected before Rollback](/help/dashboards/opportunities/assets/add-multimedia-transcript-summaries-select-in-fixed.png)

## Rollback

If you change your mind, you can roll back a deployed optimization. From **Fixed Suggestions**, select the rows to revert, then click **Rollback**.

The **Rollback** dialog lists the suggestions that will be rolled back and warns that deployed optimizations will be removed from the live path for agentic traffic. Confirm, then click **Rollback** or **Cancel**.

![Rollback dialog listing suggestions to revert](/help/dashboards/opportunities/assets/add-multimedia-transcript-summaries-rollback-dialog.png)

When the operation finishes, a **Successfully Rolled Back** summary appears; close it to return to the dashboard.

![Rollback complete — Successfully Rolled Back](/help/dashboards/opportunities/assets/add-multimedia-transcript-summaries-rollback-confirm.png)

## Try it in the demo

Explore the Add Multimedia Transcript Summaries workflow in the [Frescopa demo](https://play.llmo.now/org/demo-org).

## Frequently asked questions

<!-- **Will this optimization affect my human visitors or SEO bots?**

No. Optimize at Edge targets only AI user agents. Human visitors and SEO bots receive the original page as before.

**Do I need to change my CMS or involve developers?**

No. Transcript summaries are applied at the CDN edge. Once onboarded to Optimize at Edge, you can deploy and roll back from the LLM Optimizer interface. Implementation details in the product show how each patch is applied (for example, **insertAfter** relative to a CSS selector) for transparency.

**What happens if my page or media content changes after I deploy?**

For content opportunities such as Add Multimedia Transcript Summaries, LLM Optimizer monitors the source page for changes. If a change is detected, the optimization is paused and flagged for human review to prevent drift between the agent-visible page and the human-visible page. See the [Optimize at Edge](/help/dashboards/optimize-at-edge/overview.md) frequently asked questions for more detail.

**How do I get started with Optimize at Edge?**

See the [Optimize at Edge](/help/dashboards/optimize-at-edge/overview.md) page for onboarding, CDN configuration guides, and prerequisites.-->
