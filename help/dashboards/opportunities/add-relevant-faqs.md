---
title: Add Relevant FAQs
description: Learn how LLM Optimizer identifies high-traffic pages that lack structured Q&A content for AI agents, and how to review and deploy AI-generated FAQs with Optimize at Edge.
feature: Opportunities
---

# Add Relevant FAQs

The Add Relevant FAQs opportunity identifies high-traffic pages that lack structured Q&A content that AI agents often rely on when generating responses. It introduces relevant, **intent-aligned FAQ** content grounded in your existing page material. That helps agents match user questions to your content more directly.

For each affected URL, you can review AI-generated FAQ suggestions, then deploy them with [Optimize at Edge](/help/dashboards/optimize-at-edge/overview.md) so agentic traffic receives clearer Q&A context with no Content Management system (CMS) changes required.

## How it fixes the problem

Fixes are applied using [Optimize at Edge](/help/dashboards/optimize-at-edge/overview.md), which:

- Serves a pre-rendered HTML snapshot to AI agents.
- Enriches the page with FAQ content in the HTML they retrieve.
- Works at the CDN layer (no CMS changes).
- Is AI-only—no impact on human visitors or SEO bots.
- Deploys in minutes and is fully reversible from the LLM Optimizer interface.

## How it works

LLM Optimizer identifies high-traffic pages where Q&A content is missing or thin, based on your brand’s prompt set. Affected URLs appear in the **URLs with suggestions** table, where you can select a URL to work with.

For each page, you have the following:

- **Q&A content** (FAQ-style questions and answers) scoped to that page and your tracked intents.
- **Preview** a side-by-side comparison of the current page versus the version with suggested FAQs applied.

![URLs with FAQ suggestions](/help/dashboards/opportunities/assets/add-relevant-faqs-ui-01.png)

Expand a row to review the analysis and the proposed FAQ content for that page.

![Expanded row with FAQ details](/help/dashboards/opportunities/assets/add-relevant-faqs-expand.png)

Use **Preview** to compare the live page with the proposed FAQ experience before you deploy.

![Preview of FAQ suggestions](/help/dashboards/opportunities/assets/add-relevant-faqs-ui-02.png)

## URLs with suggestions

The **URLs with suggestions** table lists pages where FAQs would help AI-driven discovery. For each URL you can:

- **Expand the row** to view the proposed FAQ content for that page.
- **Preview** the before and after comparison.
- **Mark as Fixed** mark pages that have been optimized outside of LLM Optimizer.
- **Ignore** suggestions that are not relevant.

Suggestions are organized into **Current Suggestions**, **Fixed Suggestions**, and **Ignored Suggestions**. After you deploy, optimized URLs appear under **Fixed Suggestions** with an **Optimized** status.

![Fixed suggestions with Optimized status](/help/dashboards/opportunities/assets/add-relevant-faqs-fixed.png)

From **Fixed Suggestions**, you can select URLs to verify deployment, use **View Live** to confirm what agentic traffic receives or start a rollback.

![Select URLs in Fixed Suggestions](/help/dashboards/opportunities/assets/add-relevant-faqs-ui-03.png)

## Deploying the optimization

When you are ready to publish FAQs at the edge, select the URLs that have Q&A suggestions, optionally **Preview** the expected outcome, then click **Deploy optimizations**. A confirmation dialog lists the selected URLs and the optimization type before you confirm.

![Deploy to Edge dialog](/help/dashboards/opportunities/assets/add-relevant-faqs-ui-04.png)

After deployment, a confirmation screen shows which URLs were successfully optimized. The changes are live for AI agents; review deployed items under **Fixed Suggestions**.

![Deploy confirmation](/help/dashboards/opportunities/assets/add-relevant-faqs-ui-05.png)

>[!NOTE]
>
>Deploying optimizations requires completing the Optimize at Edge onboarding process. If you have not yet onboarded, clicking **Deploy optimizations** will direct you to the onboarding process. For full details on how Optimize at Edge works, supported CDN providers, and the onboarding process, see the [Optimize at Edge](/help/dashboards/optimize-at-edge/overview.md) page.

After deployment, you can confirm what agents see from **Fixed Suggestions** using **View Live**.

![View Live from Fixed Suggestions](/help/dashboards/opportunities/assets/add-relevant-faqs-ui-06.png)

## Rollback

If you change your mind, you can roll back a deployed FAQ optimization from **Fixed Suggestions**. Rollback uses a confirmation dialog so you can review the affected URLs before reverting to the previous agent-visible version.

![Rollback dialog](/help/dashboards/opportunities/assets/add-relevant-faqs-ui-07.png)

![Rollback confirmation](/help/dashboards/opportunities/assets/add-relevant-faqs-ui-08.png)

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
