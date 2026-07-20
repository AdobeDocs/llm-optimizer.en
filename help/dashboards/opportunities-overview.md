---
title: Optimization opportunities
description: Learn how to use the opportunities dashboard to automatically detect how your site can be improved in order to increase brand visibility.
feature: Opportunities
autotag-review: '2026-07-15T18:08:26.657Z'
TQID: 'https://experienceleague.adobe.com/nEVOXJiQZIqfs2Q-tpA3DeiBNwpZAjhMSyIVuNlACdM'
product_v2:
  - id: d830747e-f8f3-4fce-8eff-d53b333b1639
    internal-label: LLM Optimizer
feature_v2:
  - id: e1b649f0-0a61-46e4-9082-64d5cb2576c6
    internal-label: Opportunities
  - id: ef4e63f5-cb4d-462d-bf9a-1f617edf2a3a
    internal-label: Optimize at edge
subfeature_v2:
  - id: bbfc1b77-44c5-4fe8-b65f-ec160fe0d021
    internal-label: Content optimization
  - id: a6256a78-8814-462c-9627-86699b39cee1
    internal-label: Commerce
  - id: e0ec491f-fe51-42b6-801c-1c0dfcc0e64f
    internal-label: Technical GEO
  - id: fe92ae96-fc87-4fea-96a0-adc06310d4f4
    internal-label: Offsite
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
topic_v2:
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
    internal-label: Optimization
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
    internal-label: Insights
---

# Optimization opportunities

Optimization opportunities are automatically detected insights that show where your site and external presence can be improved to increase brand visibility in AI search.

These optimizations include on-page fixes (adding structured content, canonicals, or summaries), technical adjustments (unblocking AI crawlers or resolving errors) and influencing content on third-party authoritative sites. Addressing these optimization opportunities helps your brand be accurately represented and more likely to be cited in generative responses.

<!--![Optimization opportunities](/help/dashboards/assets/oport.png)-->

## Opportunities Dashboard

The optimization opportunities presented on the dashboard are prioritized based on player gaps, trending topics, and performance data and presented as a list. You can search for a specific opportunity by using the search field. Also, opportunities are grouped by tags, and you can click directly on a tag to show all the  opportunities grouped under that tag.

Clicking **Details** will open a separate window where more information and additional guidance is provided.

## Supported opportunities

Presented below is a table of currently supported opportunities:

| Opportunity | Type | Identified Issues | Fix Suggestions |
|---------|----------|----------|----------|
| [Add LLM-friendly Summaries](/help/dashboards/opportunities/add-llm-friendly-summaries.md) | Content (Onsite) | Identifies high-traffic pages that lack concise summaries and structured key points at the page or section level, making them harder for AI agents to scan and interpret brand claims. Shows affected URLs and where summaries are recommended. | Review AI-generated summaries and key points grounded in existing content, then deploy at the CDN edge with Optimize at Edge so agents receive clearer, scannable context. |
| [Add Relevant FAQs](/help/dashboards/opportunities/add-relevant-faqs.md) | Content (Onsite) | Identifies high-traffic pages that lack structured Q&A content aligned to your prompt set, making it harder for AI agents to match user questions to your page. Shows affected URLs and where FAQs are recommended. | Review AI-generated, intent-aligned FAQ content grounded in existing page material, then deploy at the CDN edge with Optimize at Edge so agents receive clearer Q&A context. |
| [Add Multimedia Transcript Summaries](/help/dashboards/opportunities/add-multimedia-transcript-summaries.md) | Content (Onsite) | Identifies pages where key information is embedded in video or other media without machine-readable transcripts or summaries, making that content hard for AI agents to use. Shows affected URLs and recommended text. | Review AI-generated transcript summaries grounded in the media and page, then deploy at the CDN edge with Optimize at Edge so agents receive machine-readable text (for example, near the relevant video). |
| [Traffic Blocked by robots.txt](/help/dashboards/opportunities/traffic-blocked-by-robots.md) | Technical GEO | Analyzes your robots.txt file for rules that selectively block AI agents from content that is otherwise publicly accessible. Reports affected URLs and blocked agents. | Update your robots.txt file to allow access for supported AI crawlers where appropriate. |
| [Agentic Traffic Errors](/help/dashboards/opportunities/agentic-traffic-errors.md) | Technical GEO | Monitors CDN logs for 404, 403, and 5xx error responses returned to AI agents. Reports affected URLs and total hits lost. | Fix broken links, update permissions, and resolve server-side issues so key content returns 200 responses. |
| [Simplify Complex Content](/help/dashboards/opportunities/simplify-complex-content.md) | Content (Onsite) | Identifies high-traffic pages where dense or complex copy sits below readability thresholds, making it harder for AI agents to interpret key information. Shows affected URLs and where simplified text is recommended. | Review AI-generated Improved Text grounded in existing page content, then deploy at the CDN edge with Optimize at Edge so agents receive clearer, easier-to-scan passages. |
| [Recover Content Visibility](/help/dashboards/opportunities/recover-content-visibility.md) | Technical GEO | Flags pages where critical content is hidden from AI agents. Shows affected URLs and expected content that can be recovered. | Pre-render the pages at the CDN layer using Optimize at Edge so more content is available to AI agents without JavaScript execution. |
| [Add Table of Contents](/help/dashboards/opportunities/add-table-of-contents.md) | Technical GEO | Detects pages that lack clear structural organization or navigational headings, making it difficult for AI agents to parse and map content to user queries. Shows affected URLs and where a structured Table of Contents is recommended. | Review the suggested structured Table of Contents with anchor-linked headings that reflect the main sections of the page, then deploy at the CDN edge with Optimize at Edge so a Table of Contents is injected into the HTML, improving page structure so models can more easily extract, map, and cite relevant sections. |
| [Wikipedia Analysis](/help/dashboards/opportunities/wikipedia-analysis.md) | Offsite | Analyzes your company's Wikipedia page against industry competitors across references, sections, content length, images, and infobox completeness. Identifies specific gaps where your page falls below industry benchmarks. | Review AI-generated strategic recommendations to improve your Wikipedia presence, including adding references, enriching your infobox, expanding sections, and improving article quality. |
| [YouTube Sentiment Analysis (Beta)](/help/dashboards/opportunities/youtube-sentiment-analysis.md) | Offsite, Social & Community | Analyzes YouTube videos cited for your Brand Presence prompt set for brand mentions, sentiment, share of voice, and recurring topics. Only appears when YouTube videos are detected as citations for your prompt set. | Review prioritized recommendations to improve brand perception across YouTube content, including suggested actions and the teams responsible for implementing them. |
| [Reddit Sentiment Analysis (Beta)](/help/dashboards/opportunities/reddit-sentiment-analysis.md) | Offsite, Social & Community | Analyzes Reddit threads cited for your Brand Presence prompt set for brand mentions, sentiment, share of voice, and recurring topics. Only appears when Reddit threads are detected as citations for your prompt set. | Review prioritized recommendations to improve brand perception across Reddit content, including suggested actions and the teams responsible for implementing them. |
| [Cited Sentiment Analysis (Beta)](/help/dashboards/opportunities/cited-sentiment-analysis.md) | Offsite, Social & Community | Analyzes top-cited URLs detected for your Brand Presence prompt set for brand mentions, sentiment, share of voice, and recurring topics. | Review prioritized recommendations to improve brand perception across the pages AI systems cite most when responding to prompts about your brand. |
| [Enrich Product Catalog (Beta)](/help/dashboards/opportunities/enrich-product-catalog.md) | Content (Onsite), Adobe Commerce | Identifies Commerce catalog products whose names or descriptions are too generic, technically dense, or ambiguous for LLMs to interpret. Shows evaluated PDPs, agentic traffic context, and AI-generated narrative enrichments. | Review and edit proposed product names and descriptions, then deploy optimizations to publish updates directly to your Adobe Commerce catalog (with rollback from Fixed Suggestions). |
| [Enrich Product Detail Pages](/help/dashboards/opportunities/enrich-product-detail-pages.md) | Technical GEO, Adobe Commerce | For Adobe Commerce storefronts, compares full catalog data to what AI agents can access on each product detail page; surfaces PDPs where variants, specifications, attributes, and related catalog fields are missing from the agent-visible HTML, prioritized by agentic traffic. | Highlights recoverable catalog information missing from the agent view and why it matters for LLM-driven product discovery; deploy with Optimize at Edge to serve a fully pre-rendered, AI-friendly HTML snapshot to agentic traffic at the CDN edge so agents receive rich product context from your catalog without CMS or catalog changes. |

## Auto-optimization {#auto-optimization}

Auto-optimization enables one-click deployment of recommended optimizations, reducing manual effort and time to value. Optimizations can be applied either at the content source or at the CDN edge. Edge based auto-optimization is currently available in Early Access for select opportunities. For more details, see the [Optimize at Edge](/help/dashboards/optimize-at-edge/overview.md) page.

<!--
### Recover Content Visibility Opportunity {#recover-contet}

As stated above, the content visibility opportunity, flags pages where key content is lost for AI agents due to client-side rendering. For each identified page, it shows you exactly which content is missing from the AI agent view, helping you pinpoint visibility gaps. It's also supported by an edge-based pre-rendering capability that can serve more HTML content to agentic traffic without requiring Content Management System (CMS) changes. This functionality is currently in Early Access and requires setup from the LLM Optimizer team. Please contact `llmo-at-edge@adobe.com` to activate the content visibility opportunity.
-->

### Additional Tools

The [LLM visibility checker](https://chromewebstore.google.com/detail/is-your-webpage-citable/jbjngahjjdgonbeinjlepfamjdmdcbcc) is a Chrome extension that lets you see exactly how much of your webpage content LLMs can access and also what stays hidden. Designed as a free, standalone diagnostic tool, it requires no product license or setup. With a single-click, users can evaluate any site's machine-readability, view a side-by-side comparison of what AI agents see versus what human users see. Also, estimates how much content could be recovered by using LLM Optimizer.

<!--
| Detect Missing Hreflang | Content (Onsite)| Flags pages missing hreflang attributes. Provides affected URLs and expected coverage by language/region.| Implement hreflang tags to indicate correct localized versions. |
| Detect Missing Canonicals | Content (Onsite) | Scans for pages without canonical tags or with conflicting tags. Lists affected URLs and duplicates. | Add canonical tags pointing to the preferred version of each page. Ensure consistent usage across variants. |
-->
