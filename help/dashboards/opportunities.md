---
title: Optimization opportunities
description: Learn how to use the opportunities dashboard to automatically detect how your site can be improved in order to increase brand visibility.
feature: Opportunities
---

# Optimization opportunities

Optimization opportunities are automatically detected insights that show where your site and external presence can be improved to increase brand visibility in AI search.

These optimizations include on-page fixes (adding structured content, canonicals, or summaries), technical adjustments (unblocking AI crawlers or resolving errors) and influencing content on third-party authoritative sites. Addressing these optimization opportunities helps your brand be accurately represented and more likely to be cited in generative responses.

![Optimization opportunities](/help/dashboards/assets/oport.png)

## Opportunities Dashboard

The optimization opportunities presented on the dashboard are prioritized based on player gaps, trending topics, and performance data and presented as a list. You can search for a specific opportunity by using the search field. Also, opportunities are grouped by tags, and you can click directly on a tag to show all the  opportunities grouped under that tag.

Clicking **Details** will open a separate window where more information and additional guidance is provided.

## Supported opportunities

Presented below is a table of currently supported opportunities:

| Opportunity | Type | Identified Issues | Fix Suggestions |
|---------|----------|----------|----------|
| Summarize Long Paragraphs | Content (Onsite) | Detects paragraphs exceeding recommended length thresholds. Shows affected URLs and oversized text snippets. | Create abstracts or split long text into shorter, scannable sections. |
| Recommend Structured Content | Content (Onsite) | Detects high-popularity prompts without matching FAQ entries. Shows related prompts, categories, and affected URLs. | Add FAQ schema blocks with concise answers to match common queries. |
| Traffic Blocked by robots.txt | Technical GEO | Analyzes your robots.txt file for rules that selectively block AI agents from content that is otherwise publicly accessible. Reports affected URLs and blocked agents. | Update your robots.txt file to allow access for supported AI crawlers where appropriate. |
| Agentic Traffic Errors | Technical GEO | Monitors CDN logs for 404, 403, and 5xx error responses returned to AI agents. Reports affected URLs and total hits lost. | Fix broken links, update permissions, and resolve server-side issues so key content returns 200 responses. |
| Simplify Complex Content | Content (Onsite) | Identifies long, complex paragraphs exceeding readability thresholds that can reduce AI comprehension. | Pre-render the pages so more content is available to AI agents without JavaScript execution. |
| Recover Content Visibility | Technical GEO | Flags pages where critical content is hidden from AI agents. Shows affected URLs and expected content that can be recovered. | Pre-render the pages at the CDN layer using Optimize at Edge so more content is available to AI agents without JavaScript execution. |
| [Wikipedia Analysis](/help/dashboards/opportunities/wikipedia-analysis.md) | Offsite | Analyzes your company's Wikipedia page against industry competitors across references, sections, content length, images, and infobox completeness. Identifies specific gaps where your page falls below industry benchmarks. | Review AI-generated strategic recommendations to improve your Wikipedia presence, including adding references, enriching your infobox, expanding sections, and improving article quality. |
| [YouTube Sentiment Analysis (Beta)](/help/dashboards/opportunities/youtube-sentiment-analysis.md) | Offsite, Social & Community | Analyzes YouTube videos cited for your Brand Presence prompt set for brand mentions, sentiment, share of voice, and recurring topics. Only appears when YouTube videos are detected as citations for your prompt set. | Review prioritized recommendations to improve brand perception across YouTube content, including suggested actions and the teams responsible for implementing them. |
| Reddit Sentiment Analysis (Beta) | Offsite, Social & Community | Analyzes Reddit threads cited for your Brand Presence prompt set for brand mentions, sentiment, share of voice, and recurring topics. Only appears when Reddit threads are detected as citations for your prompt set. | Review prioritized recommendations to improve brand perception across Reddit content, including suggested actions and the teams responsible for implementing them. |
| Cited Sentiment Analysis (Beta) | Offsite, Social & Community | Analyzes top-cited URLs detected for your Brand Presence prompt set for brand mentions, sentiment, share of voice, and recurring topics. | Review prioritized recommendations to improve brand perception across the pages AI systems cite most when responding to prompts about your brand. |

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
