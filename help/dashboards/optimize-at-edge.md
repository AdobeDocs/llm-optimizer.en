---
title: Optimize at Edge
description: Learn how to deliver optimizations in LLM Optimizer at the CDN edge without any authoring changes required.
feature: Opportunities
---

# Optimize at Edge

This page provides a detailed overview on how to deliver optimizations at the CDN edge without any authoring changes. It covers the onboarding process, the available optimization opportunities and how to auto-optimize at edge.

>[!NOTE]
>This functionality is currently in Early Access. You can learn more about Early Access programs [here](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/release-notes/release-notes/release-notes-current#aem-beta-programs).

## What is Optimize at Edge?

Optimize at Edge is an edge-based deployment capability in LLM Optimizer that serves AI friendly changes to LLM user agents. In the current context, "Edge" means that the optimization is applied at the CDN layer. Because it delivers optimizations at the CDN layer, no authoring changes in the Content Management System (CMS) are required so your origin CMS remains unchanged. This separation lets you improve LLM visibility without altering your existing publishing workflows. It targets only agentic traffic and does not impact either human users or SEO bots. When LLM Optimizer detects opportunities to optimize a page, users can deploy fixes directly at the CDN edge.

Optimize at Edge is a faster, leaner alternative to traditional fixes that demand complex engineering efforts. As mentioned, once you complete a one-time setup, no platform changes or long development cycles are required to apply the changes. You can publish improvements in minutes without requiring developer engagement. It is a no-code way to optimize your website for AI agents.

Optimize at Edge is designed for business users in marketing, SEO, content and digital strategy teams. It can enable business users to complete the full journey in LLM Optimizer: identifying opportunities, understanding suggestions, and easily deploying the fixes. With Optimize at Edge, users can preview the changes, deploy them quickly at the CDN edge and validate that the optimizations are live. Performance can be tracked in the LLM Optimizer ecosystem.

### Key benefits

* **AI-only delivery:** Serves optimized HTML only to AI agents with no impact on either human visitors or SEO bots.
* **Faster cycles:** Publish changes in minutes not weeks. No platform changes or long engineering cycles required.
* **Reversible:** Supported with a one-click rollback capability that can revert the page in minutes.
* **No performance impact:** Edge based optimizations and caching keep the site latency unaffected.
* **CDN and CMS-agnostic:** Works with any CDN configuration and front-end setup regardless of the Content Management System.

### Which opportunities are supported with Optimize at Edge?

Opportunities that can improve the agentic web experience are supported with Optimize at Edge. Learn more about each opportunity both in the [Opportunities Dashboard](/help/dashboards/opportunities.md) page and the opportunities section in the current page.

## Onboarding

You should reach out to either your Adobe account team or the FDE team to start the onboarding process. Your IT or CDN team is also required to complete the pre-requisites and setup process. Additionally, you can also contact `llmo-at-edge@adobe.com` for further onboarding assistance.

Pre-requisites to onboard to Optimize at Edge:

* Complete the onboarding process to LLM Optimizer. 
* Complete the log forwarding process for your CDN logs.

Requirements for your IT/CDN team:
* Add `*AdobeEdgeOptimize/1.0*` user-agent to the Allowlist in your site’s robots.txt file or bot-traffic management rules.
* Ensure that pages are not blocked at the domain or CDN level. 
* Add Optimize at Edge routing rules in the CDN.
* Confirm Optimize at Edge routing in the LLM Optimizer interface.

To guide the setup process, select your CDN provider below and follow the corresponding configuration guide. Keep in mind that these examples should be adapted to your actual live configuration. We recommend applying changes in the lower environments first.

### CDN Configuration Guides

| CDN Provider | Type | Guide |
|---|---|---|
| AEM Cloud Service Managed CDN (Fastly) | Adobe Managed | [View setup guide](/help/dashboards/optimize-at-edge-aem-managed-cdn.md) |
| Fastly (BYOCDN) | Bring Your Own CDN | [View setup guide](/help/dashboards/optimize-at-edge-fastly-byocdn.md) |
| Akamai (BYOCDN) | Bring Your Own CDN | [View setup guide](/help/dashboards/optimize-at-edge-akamai-byocdn.md) |
| Cloudflare (BYOCDN) | Bring Your Own CDN | [View setup guide](/help/dashboards/optimize-at-edge-cloudflare-byocdn.md) |

>[!NOTE]
>For other CDN providers, please reach out to `llmo-at-edge@adobe.com` to assist your IT/CDN teams with onboarding. Once the setup configurations are complete, you can deploy suggestions for Optimize at Edge opportunities in LLM Optimizer.

### Verify the setup

After completing the CDN configuration, test the setup by running a curl with an agentic user-agent and look for the `x-edgeoptimize-request-id` header in the response:

```
curl -svo /dev/null https://www.example.com/page.html --header "user-agent: chatgpt-user"
< HTTP/2 200
< x-edgeoptimize-request-id: 50fce12d-0519-4fc6-af78-d928785c1b85
```

The status of the traffic routing can also be checked in the LLM Optimizer UI. Navigate to **Customer Configuration** and select the **CDN Configuration** tab.

For AEM Cloud Service Managed CDN (Fastly):

![AI Traffic Routing status with routing enabled](/help/assets/optimize-at-edge/adobe-CDN-traffic-routed-tick.png)

For BYOCDN configurations (Fastly, Akamai, Cloudflare):

![AI Traffic Routing status with routing enabled](/help/assets/optimize-at-edge/byocdn-CDN-traffic-routed-tick.png)

## Opportunities

Presented in the following table are opportunities that can improve the agentic web experience and are supported with Optimize at Edge.

| Opportunity | Type | Auto-Identify | Auto-suggest | Auto-optimize |
|---------|----------|----------|----------|----------|
|Recover Content Visibility | Technical GEO | Detects pages where critical content is hidden from AI agents. Shows affected URLs and expected content that can be recovered.| Highlights content that can be made available for AI agents and recommends enabling pre-rendering for those pages. | Serves a fully rendered, AI-friendly HTML snapshot to agentic traffic that recovers the previously hidden content.|
| Optimize Headings for LLMs | Content Optimization | Scans headings to detect empty, duplicate, missing or ambiguous headings that can reduce machine readability.| Proposes a cleaner heading hierarchy and improved labels and shows a preview of the updated structure for each page.| Injects the improved heading structure for AI agents, preserving your visual design while making the page more readable for LLMs.|
| Add LLM-Friendly Summaries | Content Optimization | Identifies long or complex pages that lack concise summaries at the page or section level, making them harder for AI to quickly scan and understand.| Recommends short, AI-generated summaries at the page and section level that capture key content.| Inserts the summaries into the relevant HTML sections, improving how models interpret and describe the page content.|
| Add Relevant FAQs | Content Optimization | Detects intent gaps in the existing page content that could benefit from FAQs. | Suggests AI-generated FAQ content aligned to the user intent and existing topics. | Injects FAQ content into the HTML, making pages more discoverable and relevant in AI-driven answers.|
| Simplify Complex Content | Content Optimization | Flags pages with complex text that can hinder AI comprehension. | Provides AI-generated simplified versions of complex text while preserving the original meaning. | Rewrites complex sections in the page, improving AI readability. |

### Additional Tools

The [Adobe LLM Optimizer: Is your webpage citable?](https://chromewebstore.google.com/detail/adobe-llm-optimizer-is-yo/jbjngahjjdgonbeinjlepfamjdmdcbcc) Chrome extension shows how much of your webpage content LLMs can access and what stays hidden. Designed as a free, standalone diagnostic tool, it requires no product license or setup.

With a single-click, you can evaluate any site's machine readability. You can view a side-by-side comparison of what AI agents see versus what human users see, and estimate how much content could be recovered by using LLM Optimizer. See the [Can AI read your website?](https://business.adobe.com/blog/introducing-the-llm-optimizer-chrome-extension) page for more information.

## Opportunities detailed

In the sections that follow, you can view additional details for each opportunity that is supported with Optimize at Edge.

### Recover Content Visibility

This opportunity flags pages where key content is hidden for AI agents due to client-side rendering. For each identified page, it shows you exactly which content is missing from the AI agent view, highlights visibility gaps, and enables you to directly apply changes to recover the hidden content. When you deploy this opportunity with Optimize at Edge, a pre-rendered, AI-optimized version of the page is served to LLM user agents so they can access the full context without executing Javascript.
This ensures the page is first fully visible to AI agents. Additional enhancements are applied on top of that pre-rendered HTML.

>[!IMPORTANT]
>This pre-rendering capability automatically applies to all opportunities presented below when deployed with Optimize at Edge to ensure the page is fully visible to AI agents.

### Optimize Headings for LLMs

This opportunity detects pages where the heading structure makes it hard for AI agents to understand the page due to empty, duplicate, missing or ambiguous headings. For each affected page, the opportunity surfaces the suboptimal headings and recommends a clearer hierarchy. When deployed with Optimize at Edge, the improved headings are applied in the HTML served to agentic traffic. This helps machine readability while leaving your human facing layout the same.

### Add LLM-Friendly Summaries

This opportunity identifies pages that can benefit from concise summaries to help LLMs quickly understand what the page content is about. For each page, the opportunity detects where a summary is most needed and creates AI-generated summaries either at the page level or section level. When you deploy with Optimize at Edge these summaries are inserted into the HTML that AI agents retrieve, improving the chances of having your content be described more accurately.

### Add Relevant FAQs

This opportunity flags pages where additional Q&A content could better match the user intent and prompts in AI-driven discovery. For each page, it proposes AI-generated FAQ blocks tied to user intent and content on the page. With Optimize at Edge, these FAQs are injected into the HTML, making your page more AI-friendly and increasing the likelihood that AI answers directly reflect your guidance.

### Simplify Complex Content

This opportunity finds pages with long, complex paragraphs that can reduce AI comprehension. For each page that exceeds the readability thresholds, it creates AI-generated content that is simpler and easier to scan while preserving the original meaning. When deployed at the edge, the simplified content delivered to agentic traffic helps LLMs interpret and summarize your content more faithfully.

## Auto-Optimize at Edge

For each opportunity, you can preview, edit, deploy, view live, and roll back the optimizations at the edge.

>[!VIDEO](https://video.tv.adobe.com/v/3477983/?learn=on&enablevpops)

### Preview

**Preview** lets you see the impact of a suggestion before it goes live. It surfaces a side-by-side difference between the current page and the AI-optimized version expected after applying the suggestion. This view uses the same Optimize at Edge logic that will power live traffic, but in an isolated preview mode. This does not impact live traffic as it is a read-only simulation for review.

![Preview](/help/assets/optimize-at-edge/preview.png)

### Edit

**Edit** allows you to refine or rewrite altogether the auto-generated suggestion before deploying it. Instead of accepting the suggestion, you maintain full control through the edit workflow. The view displays proposed changes in a structured editor, where you can modify the text to better match your original intent. The edited version will then be served to AI agents once deployed.

![Edit](/help/assets/optimize-at-edge/edit.png)

### Deploy

**Deploy** publishes the selected suggestions so the optimized experiences can be served from the edge to AI agents. If the CDN is fully routed, all pages in the domain usually go live with the new changes within minutes. If routing has been configured for select paths only, only the allowlisted pages go live with the optimizations.

![Deploy](/help/assets/optimize-at-edge/deploy.png)

### View Live

**View Live** lets you verify that the optimization is live and behaving as expected for agentic traffic, a view that would otherwise be hard to access. You can view the live page under Fixed Suggestions, which renders the page as shown to AI agents.

![View Live](/help/assets/optimize-at-edge/view-live.png)

### Rollback

Rollback safely reverts a previously deployed optimization. The AI-only version of the page is typically returned to its previous state within minutes, making it safe to experiment with optimizations when needed.

![Rollback](/help/assets/optimize-at-edge/rollback.png)

## Frequently Asked Questions

Q. What kind of LLMs do you target with Optimize at Edge?

The list of user agents to target is defined by you during the onboarding process.

<!--Q. What does "Edge" in Optimize at Edge mean?

In our context, "Edge" means that the optimization is applied at the CDN layer and not inside your CMS.

Q. Why does this optimization require a CDN?

The CDN is where the optimized version of the page is assembled and delivered to AI agents. We leverage the CDN to ensure your origin CMS remains unchanged. This separation lets you improve LLM visibility without altering your existing publishing workflows.-->

Q. What happens if I'm not onboarded to Optimize at Edge yet?

If you click **Deploy optimizations** before completing the required setup, nothing will be applied to your site. Instead, a pop-up dialog prompts you to contact our team at `llmo-at-edge@adobe.com` for onboarding assistance. Until onboarding is complete, you can still explore the detected opportunities and suggestions, but the one-click deployment workflow will remain inactive.

Q: What happens when the content is updated at source?

We serve the optimized version of the page from cache as long as the underlying source page hasn't changed. However, when the source does change, our system automatically refreshes so AI agents always receive the most up-to-date content. This is because we use low cache time to live (TTL) settings (by order of minutes) so that any content update on your site triggers a new optimization within that window. <!--As there is no universal TTL that fits every site, we can configure this TTL based on your cache invalidation rules to ensure both systems stay in sync.-->

Q. Is Optimize at Edge only for sites using Adobe Edge Delivery Service (EDS)?

No. Optimize at Edge is CDN-agnostic and works with any front-end architecture, not just the ones deployed on Adobe's EDS Stack.

Q. How is Optimize at Edge pre-rendering different from traditional server-side rendering (SSR)?

Both solve different problems and can work together. Traditional SSR renders server-side content but doesn't include content loaded later in the browser. Optimize at Edge pre-rendering captures the page after JavaScript and client-side data has loaded, producing the fully assembled version at the CDN edge. SSR focuses on improving the human experience and Optimize at Edge improves the web experience for LLMs.
