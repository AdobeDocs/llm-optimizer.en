---
title: Optimize at Edge
description: Learn how to deliver optimizations in LLM Optimizer at the CDN edge without any authoring changes required.
feature: Opportunities
---

# Optimize at Edge

This section ...

## What is Optimize at Edge?

Optimize at Edge is an edge-based deployment capability in LLM Optimizer that can serve AI-friendly changes to LLM user agents. Because it delivers optimizations at the CDN edge, no authoring changes in the Content Management System (CMS) are required. It also targets only the agentic traffic and does not impact human users or SEO bots.

When LLM Optimizer detects opportunities to optimize a page, users can deploy fixes directly at the edge with no platform changes required.

This capability is currently in Early Access.

## Why should a customer be interested?

Optimize at Edge is a faster, leaner alternative to traditional fixes that demand complex engineering efforts. Once customers complete a one-time setup, no platform changes or long development cycles are required to apply the changes to the webpages. The user can publish improvements in minutes, not weeks, without requiring developer engagement. This is a low-risk, no-code way to optimize your website for AI agents.

### Key benefits & value proposition

* **AI-only delivery:** Serves optimized HTML to AI agents only with no impact on human visitors or SEO bots.
* **Faster cycles:** Publish changes in minutes, not weeks. No platform changes or long engineering cycles required.
* **Low-risk and reversible:** Supported with a one-click rollback capability that can revert the page in minutes.
* **No performance impact:** Edge-based optimizations and caching keep site latency unaffected.
* **CDN and CMS-agnostic:** Works with any CDN configuration and front-end setup regardless of CMS.

## Who should use it?

Optimize at Edge is designed for business users in marketing, SEO, content, and digital strategy teams. It can enable business users to complete the full journey in LLM Optimizer: identifying opportunities, understanding suggestions, and easily deploying the fixes. With Optimize at Edge, users can preview the changes, deploy them quickly at the edge, and validate that the optimizations are live. Performance can be tracked in the LLM Optimizer ecosystem.

## Which opportunities have Optimize at Edge?

Opportunities that can improve the agentic web experience are supported with Optimize at Edge. Learn more about each opportunity in [Opportunities](/help/dashboards/opportunities.md) section.

## Onboarding

Customers can enable Optimize at Edge after they have onboarded to LLM Optimizer and have completed forwarding their CDN logs. An CDN engineer is required to complete the initial setup to enable Optimize at Edge.

Requirements for Setup:

* Generate an API key
* Add Optimize at Edge routing rules in the CDN
* Allowlist user-defined paths or the entire domain
* Add a user-defined list of LLM user agents to target
* Ensure robots.txt doesn't block any user agents intended to target
* Confirm Optimize at Edge routing in LLM Optimizer UI

Adobe provides sample configuration snippets for most major CDNs to guide the setup process. The snippet examples included in our guideline should be adapted to the actual live configuration. Changes are recommended to be implemented in the lower environments first.

>[!BEGINTABS]

>[!TAB AEM Cloud Service Managed CDN (Fastly)]

Tokowaka BYOCDN - Adobe Managed CDN

Uses only originSelectors to select the Tokowaka origin.

The following example routes LLM agents requests on specific domain matching the the pattern "/es/*" or exact paths (only html pages are routed). The example is supposed to provide a starting point and in case you have multiple originSelectors in your config it is recommended to place this first.

Important notes:

* x-tokowaka-request needs to be checked before routing to Tokowaka backend. Only requests that do not have this header should be routed to Tokowaka backend.
* the originSelector rule that routes to Tokowaka backend should be first in the list if there are multiple rules.
* TOKOWAKA_API_KEY secret needs to be delpoyed before deploying the cdn.yaml

```
kind: "CDN"
version: "1"
data:
  # Origin selectors to route to Tokowaka backend
  originSelectors:
    rules:
      - name: route-to-tokowaka-backend
        when:
          allOf:
            - reqHeader: x-tokowaka-request
              exists: false # avoid loops when requests comes from Tokowaka
            - reqHeader: user-agent
              matches: "(?i)(Tokowaka-AI|ChatGPT-User|GPTBot|OAI-SearchBot|PerplexityBot|Perplexity-User)" # routed user agents
            - reqProperty: domain
              equals: "example.com" # routed domain
            - reqProperty: originalPath
              matches: '(/[^./]+|\.html|/)$' # routed extensions, with .html extension or without extension
            - anyOf:
              - { reqProperty: originalPath, in: [ "/page.html" ] } # routed pages, exact path matching
              - { reqProperty: originalPath, like: "/dir/*" } # routed pages, wildcard path matching
        action:
          type: selectOrigin
          originName: tokowaka-backend
          headers:
            x-tokowaka-api-key: "${{TOKOWAKA_API_KEY}}"
    origins:
      - name: tokowaka-backend
        domain: "edge.tokowaka.now"

```

>[!TAB Akamai (BYOCDN)]

This content appears in the Android tab.

>[!TAB Fastly (BYOCDN)]

This content appears in the Windows tab.

>[!ENDTABS]


For other CDN providers, please reach out to llmo-at-edge@adobe.com to assist your IT/CDN teams with onboarding.

<!--This should probably be in Opportunities dashboard content-->

After the configurations are complete, business users can deploy suggestions for Optimize at Edge opportunities in LLM Optimizer.

## Opportunities

| Opportunity | Type | Auto-Identify | Auto-suggest | Auto-optimize |
|---------|----------|----------|----------|----------|
|Recover Content Visibility | Technical GEO | Detects pages where critical content is hidden from AI agents. Shows affected URLs and expected content that can be recovered.| Highlights content that can be made available for AI agents and recommends enabling pre-rendering for those pages. | Serves a fully rendered, AI-friendly HTML snapshot to agentic traffic that recovers the previously hidden content.|
| Optimize Headings for AI | Content Optimization | Scans headings to detect empty, duplicate, missing, or ambiguous headings that can reduce machine-readability.| Proposes a cleaner heading hierarchy and improved labels and shows a preview of the updated structure for each page.| Injects the improved heading structure for AI agents, preserving your visual design while making the page more understandable for LLMs.|
| Add AI-Friendly Summaries | Content Optimization | Identifies long or complex pages that lack concise summaries at the page or section level, making them harder for AI to quickly scan and understand.| Recommends short, AI-generated summaries at the page-level and section-level that capture key content.| Inserts the summaries into the relevant HTML sections, improving how models interpret and describe the page content.|
| Add Relevant FAQs | Content Optimization | Detects intent gaps in the existing page content that could benefit from FAQs. | Suggests AI-generated FAQ content aligned to user intents and existing topics. | Injects FAQ content into the HTML, making pages more discoverable and relevant in AI-driven answers.|
| Simplify Complex Content | Content Optimization | Flags pages with complex text that can hinder AI comprehension. | Provides AI-generated simplified versions of complex test while preserving the original meaning. | Rewrites complex sections in the page, improving AI readability. |

### Recover Content Visibility

This opportunity flags pages where key content is hidden for AI agents due to client-side rendering. For each identified page, it shows you exactly which content is missing from AI agent view, highlights visibility gaps, and enables you to directly apply changes to recover the hidden content. When you deploy this opportunity with Optimize at Edge, a pre-rendered, AI-optimized version of the page is served to LLM user agents so they can access the full context without executing Javascript.

**This pre-rendering capability automatically applies to all opportunities that follow when deployed with Optimize at Edge.** This ensures the page is fully visible to AI agents first. Additional enhancements are applied on top of that pre-rendered HTML.

#### Additional Tools

Is your webpage citable? The [Adobe LLM Optimizer: Is your webpage citable?](https://chromewebstore.google.com/detail/adobe-llm-optimizer-is-yo/jbjngahjjdgonbeinjlepfamjdmdcbcc) Chrome extension lets you see exactly how much of your webpage content LLMs can access and what stays hidden. Designed as a free, standalone diagnostic tool, it requires no product license or setup.

With a single-click, you can evaluate any site's machine-readability, view a side-by-side comparison of what AI agents see versus what human users see, and estimate how much content could be recovered using LLM Optimizer. See [Can AI read your website?](https://business.adobe.com/blog/introducing-the-llm-optimizer-chrome-extension) for more information.

### Optimize Headings for LLMs

This opportunity detects pages where the heading structure makes it hard for AI agents to understand the page due to empty, duplicate, missing or ambiguous headings. For each affected page, the opportunity surfaces the suboptimal headings and recommends a clearer hierarchy. When deployed with Optimize at Edge, the improved headings are applied in the HTML served to agentic traffic, which can help improve machine readability while leaving your human-facing layout the same.

### Add LLM-Friendly Summaries

This opportunity identifies pages that can benefit from concise summaries to help LLMs quickly understand what the page is about. For each page, the opportunity detects where a summary is most needed and creates AI-generated summaries at the page-level and/or section-level. When you deploy with Optimize at Edge these summaries are inserted into the HTML that AI agents retrieve, improving the chances of having your content be described more accurately.

### Add Relevant FAQs

This opportunity flags pages where additional Q&A content could better match user intent and prompts in AI-driven discovery. For each page, it proposes AI-generated FAQ blocks tied to user intent and content on the page. With Optimize at Edge, these FAQs are injected into the HTML, making your page more AI-friendly and increasing the likelihood that AI answers directly reflect your guidance.

### Simplify Complex Content

This opportunity finds pages with long, complex paragraphs that can reduce AI comprehension. For each page that exceeds readability thresholds, it creates AI-generated content that is simpler and more scannable while preserving the original meaning. When deployed at the edge, the simplified content delivered to agentic traffic helps LLMs interpret and summarize your content more faithfully.

## Suggestions

For each opportunity, you can preview, edit, deploy, live preview, and roll back the optimizations at the edge.

### Preview

Preview lets users see the impact of a suggestion on the page before anything goes live. It surfaces a side-by-side difference between the current page and the AI-optimized version expected after applying the suggestion. This view uses the same Optimize at Edge logic that will power live traffic, but in a safe, isolated preview mode. This does not impact live traffic as it is a read-only simulation for review.

![Preview](/help/assets/optimize-at-edge/preview.png)

### Edit

Edit allows users to refine or rewrite altogether the auto-generated suggestion before deploying it. Instead of passively accepting the suggestion, users maintain full control through this human-in-the-loop workflow. The view displays proposed changes in a structured editor, where users can modify the text to better match their intent. The edited version will then be served to AI agents once deployed.

![Edit](/help/assets/optimize-at-edge/edit.png)

### Deploy

Deploy publishes the selected suggestions so the optimized experiences can be served from the edge to AI agents. If the CDN is fully routed, all pages in the domain go live with the new changes typically within minutes. If routing has been configured for select paths only, only the allowlisted pages go live with the optimizations.

![Deploy](/help/assets/optimize-at-edge/deploy.png)

### View Live

View Live lets users verify that the optimization is live and behaving as expected for agentic traffic, a view that would otherwise be hard to access. Users can view the live page under Fixed Suggestions, which renders the page as shown to AI agents.

![View Live](/help/assets/optimize-at-edge/view-live.png)

### Rollback

Rollback safely reverts a previously deployed optimization. The AI-only version of the page is typically returned to its previous state within minutes, making it safe for users to experiment with optimizations if needed.

![Rollback](/help/assets/optimize-at-edge/rollback.png)

## Frequently Asked Questions

Q. What kind of LLMs do you target with Optimize at Edge?

The list of user agents to target is completely defined by the customer at onboarding.

Q. What does "Edge" in Optimize at Edge mean?

In our context, "Edge" means the optimization is applied at the CDN layer and not inside your CMS.

Q. Why does this optimization require a CDN?

The CDN is where the optimized version of the page is assembled and delivered to AI agents. We leverage the CDN to ensure your origin CMS remains unchanged. This separation lets you improve LLM visibility without altering your existing publishing workflows.

Q. What happens if I'm not onboarded to Optimize at Edge yet?

If you click "Deploy optimizations" before completing the required setup, nothing will be applied to your site. Instead, a pop-up dialog prompts you to contact our team at llmo-at-edge@adobe.com for onboarding assistance. Until onboarding is complete, you can still explore the detected opportunities and suggestions, but the one-click deployment workflow will remain inactive.

Q: What happens when the content is updated at source?

We serve the optimized version of the page from cache as long as the underlying source page hasn't changed. However, when the source does change, our system automatically refreshes so AI agents always receive the most up-to-date content. This is because we use low cache TTLs in order of minutes so that any content update on your site triggers a new optimization within that window. As there is no universal TTL that fits every site, we can configure this TTL based on your cache invalidation rules to ensure both systems stay in sync.

Q. Is Optimize at Edge only for sites using Adobe Edge Delivery Service (EDS)?

No. Optimize at Edge is CDN-agnostic and works with any front-end architecture, not just ones deployed on Adobe's EDS Stack.

Q. How is Optimize at Edge pre-rendering different from traditional server-side rendering (SSR)?

The two solve different problems and can work together. Traditional SSR renders server-side content but doesn't include content loaded later in the browser. Optimize at Edge pre-rendering captures the page after JavaScript and client-side data have loaded, producing the fully assembled version at the CDN edge. SSR focuses on improving the human experience and Optimize at Edge improves the web experience for LLMs.


















