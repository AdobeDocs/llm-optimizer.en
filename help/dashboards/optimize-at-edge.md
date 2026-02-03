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

* Generate an API key.
* Add Optimize at Edge routing rules in the CDN.
* Allowlist user-defined paths or the entire domain.
* Add a user-defined list of LLM user agents to target.
* Ensure `robots.txt` does not block any user agents intended to target.
* Confirm Optimize at Edge routing in the LLM Optimizer interface.

To guide the setup process, presented below, are sample configurations for a number of CDN setups. Keep in mind that these examples should be adapted to your actual live configuration. We recommend applying changes in the lower environments first.

>[!BEGINTABS]

>[!TAB Adobe Managed CDN]

**Adobe Managed CDN**

The purpose of this configuration is to configure requests with agentic user agents that will be routed to the Optimizer service (`live.edgeoptimize.net` backend). To test the configuration, after the setup is complete look for the header `x-edgeoptimize-request-id` in the response.

```
curl -svo page.html https://frescopa.coffee/about-us --header "user-agent: chatgpt-user"
< HTTP/2 200
< x-edgeoptimize-request-id: 50fce12d-0519-4fc6-af78-d928785c1b85

```

The routing configuration is done by using an [originSelector CDN rule](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn-configuring-traffic#origin-selectors). The prerequisites are as follows:

* decide the domain to be routed
* decide the paths to be routed
* decide the user agents to be routed (recommended regex)

In order to deploy the rule, you need to:

* create a [configuration pipeline](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/operations/config-pipeline)
* commit the `cdn.yaml` configuration file in your repository
* run the configuration pipeline


```
kind: "CDN"
version: "1"
data:
  # Origin selectors to route to Edge Optimize backend
  originSelectors:
    rules:
      - name: route-to-edge-optimize-backend
        when:
          allOf:
            - reqHeader: x-edgeoptimize-request
              exists: false # avoid loops when requests comes from Edge Optimize
            - reqHeader: user-agent
              matches: "(?i)(AdobeEdgeOptimize-AI|ChatGPT-User|GPTBot|OAI-SearchBot|PerplexityBot|Perplexity-User)" # routed user agents
            - reqProperty: domain
              equals: "example.com" # routed domain
            - reqProperty: originalPath
              matches: '(/[^./]+|\.html|/)$' # routed extensions, with .html extension or without extension
            - anyOf:
              - { reqProperty: originalPath, in: [ "/page.html" ] } # routed pages, exact path matching
              - { reqProperty: originalPath, like: "/dir/*" } # routed pages, wildcard path matching
        action:
          type: selectOrigin
          originName: edge-optimize-backend
    origins:
      - name: edge-optimize-backend
        domain: "live.edgeoptimize.net"

```

To test the setup, run a curl and expect the following:

```
curl -svo page.html https://www.example.com/page.html --header "user-agent: chatgpt-user"
< HTTP/2 200
< x-edgeoptimize-request-id: 50fce12d-0519-4fc6-af78-d928785c1b85

```

>[!TAB Fastly (BYOCDN)]

**Edge Optimize BYOCDN - Fastly - VCL**

![Fastly VCL](/help/assets/optimize-at-edge/fastly-vcl.png)

![Add VCL snippets](/help/assets/optimize-at-edge/add-vcl-snippets.png)

**vcl_recv snippet**

```
unset req.http.x-edgeoptimize-url;
unset req.http.x-edgeoptimize-config;
unset req.http.x-edgeoptimize-api-key;

if (!req.http.x-edgeoptimize-request
    && req.http.user-agent ~ "(?i)(AdobeEdgeOptimize-AI|ChatGPT-User|GPTBot|OAI-SearchBot|PerplexityBot|Perplexity-User)") {
  set req.http.x-fowarded-host = req.http.host; # required for identifying the original host
  set req.http.x-edgeoptimize-url = req.url; # required for identifying the original url
  set req.http.x-edgeoptimize-config = "LLMCLIENT=true"; # required for cache key
  set req.http.x-edgeoptimize-api-key = "<YOUR API KEY>"; # required for identifying the client
  set req.backend = F_EDGE_OPTIMIZE;
}
```

**vcl_hash snippet**

```
if (req.http.x-edgeoptimize-config) {
  set req.hash += "edge-optimize";
  set req.hash += req.http.x-edgeoptimize-config;
}
```

**vcl_deliver snippet**

```
if (req.http.x-edgeoptimize-config && resp.status >= 400) {
  set req.http.x-edgeoptimize-request = "failover";
  set req.backend = F_Default_Origin;
  restart;
}

if (!req.http.x-edgeoptimize-config && req.http.x-edgeoptimize-request == "failover") {
  set resp.http.x-edgeoptimize-fo = "1";
}
```

>[!TAB Akamai (BYOCDN)]

**Edge Optimize BYOCDN - Akamai**

The purpose of this configuration is to route requests from agentic user agents to the Edge Optimize service (`live.edgeoptimize.net` backend). To test the configuration, after the setup is complete look for the header `x-edgeoptimize-request-id` in the response.


**The following Akamai Property Manager JSON rule routes LLM user agents to Edge Optimize:**

The configuration includes the following steps:

**1. Set routing criteria (User-Agent matching)**

![Set routing criteria](/help/assets/optimize-at-edge/akamai-step1-routing.png)

**2. Set Origin and SSL behavior**

![Set Origin and SSL behavior](/help/assets/optimize-at-edge/akamai-step2-origin.png)

**3. Set Cache Key Variable**

![Set Cache Key Variable](/help/assets/optimize-at-edge/akamai-step3-cachekey.png)

**4. Caching Rules**

![Caching Rules](/help/assets/optimize-at-edge/akamai-step4-rules.png)

**5. Modify Incoming Request Headers**

![Modify Incoming Request Headers](/help/assets/optimize-at-edge/akamai-step5-request.png)

**6. Modify Incoming Response Headers**

![Modify Incoming Response Headers](/help/assets/optimize-at-edge/akamai-step6-response.png)

**7. Cache ID Modification**

![Cache ID Modification](/help/assets/optimize-at-edge/akamai-step7-cacheid.png)

**8. Site Failover**

![Site Failover](/help/assets/optimize-at-edge/akamai-step8-failover.png)

![Failover Behaviors](/help/assets/optimize-at-edge/akamai-step8-failover-behaviors.png)

![Failover Rules](/help/assets/optimize-at-edge/akamai-step8-failover-rules.png)

![Behaviors Response](/help/assets/optimize-at-edge/akamai-step8-behaviors-response.png)


The complete Akamai Property Manager JSON configuration:

```
{
    "name": "Edge Optimize CDN Rule",
    "children": [
        {
            "name": "Connection settings",
            "children": [],
            "behaviors": [
                {
                    "name": "advanced",
                    "options": {
                        "description": "",
                        "xml": "<forward:availability.health-detect.status>off</forward:availability.health-detect.status>\n<forward:availability>\n<max-reforwards>1</max-reforwards>\n<max-reconnects>1</max-reconnects>\n</forward:availability>\n<match:forward.server-type value=\"CUSTOMER_ORIGIN\">\n<network:http.read>%(PMUSER_HTTP_READ)</network:http.read>\n<network:http.first-byte-timeout>%(PMUSER_FIRST_BYTE_TIMEOUT)</network:http.first-byte-timeout>\n<network:http.connect-timeout>%(PMUSER_HTTP_CONNECT_TIMEOUT)</network:http.connect-timeout> \n</match:forward.server-type>"
                    },
                    "uuid": "4a8c027b-1b23-44a7-8e12-f8d07e453679",
                    "templateUuid": "41c77091-419f-43f2-9a84-0b406b050cc8"
                }
            ],
            "uuid": "4759571b-8036-4c16-9b60-d3aeb84958f1",
            "criteria": [],
            "criteriaMustSatisfy": "all"
        },
        {
            "name": "Site Failover Behavior",
            "children": [],
            "behaviors": [
                {
                    "name": "failAction",
                    "options": {
                        "actionType": "RECREATED_CO",
                        "contentCustomPath": false,
                        "contentHostname": "www.adobe.com",
                        "enabled": true
                    }
                },
                {
                    "name": "advanced",
                    "options": {
                        "description": "",
                        "xml": "<forward:availability.fail-action2>\n<add-header>\n<status>on</status>\n<name>x-edgeoptimize-request</name>\n<value>fo</value>\n</add-header>\n</forward:availability.fail-action2>"
                    }
                }
            ],
            "uuid": "b3000c12-1ab8-49b1-a5d0-75e58bb18c9c",
            "criteria": [
                {
                    "name": "matchResponseCode",
                    "options": {
                        "lowerBound": 400,
                        "matchOperator": "IS_BETWEEN",
                        "upperBound": 599
                    }
                },
                {
                    "name": "originTimeout",
                    "options": {
                        "matchOperator": "ORIGIN_TIMED_OUT"
                    }
                }
            ],
            "criteriaMustSatisfy": "any",
            "comments": "If Edge Optimize origin returns a 4xx or 5xx error (or times out), failover condition is to send the request back to Akamai and set the x-edgeoptimize-request header so we don't re-send the request to Edge Optimize"
        }
    ],
    "behaviors": [
        {
            "name": "origin",
            "options": {
                "cacheKeyHostname": "ORIGIN_HOSTNAME",
                "compress": true,
                "customValidCnValues": [
                    "{{Origin Hostname}}",
                    "{{Forward Host Header}}",
                    "*.edgeoptimize.net"
                ],
                "enableTrueClientIp": true,
                "forwardHostHeader": "ORIGIN_HOSTNAME",
                "hostname": "live.edgeoptimize.net",
                "httpPort": 80,
                "httpsPort": 443,
                "ipVersion": "IPV4",
                "minTlsVersion": "DYNAMIC",
                "originCertificate": "",
                "originCertsToHonor": "STANDARD_CERTIFICATE_AUTHORITIES",
                "originSni": true,
                "originType": "CUSTOMER",
                "ports": "",
                "standardCertificateAuthorities": [
                    "akamai-permissive",
                    "THIRD_PARTY_AMAZON"
                ],
                "tlsVersionTitle": "",
                "trueClientIpClientSetting": true,
                "trueClientIpHeader": "True-Client-IP",
                "verificationMode": "CUSTOM"
            }
        },
        {
            "name": "setVariable",
            "options": {
                "transform": "NONE",
                "valueSource": "EXPRESSION",
                "variableName": "PMUSER_LLMCLIENT",
                "variableValue": "TRUE"
            }
        },
        {
            "name": "setVariable",
            "options": {
                "caseSensitive": false,
                "extractLocation": "CLIENT_REQUEST_HEADER",
                "globalSubstitution": false,
                "headerName": "Accept-Language ",
                "regex": "^([a-zA-Z]{2}).*",
                "replacement": "$1",
                "transform": "SUBSTITUTE",
                "valueSource": "EXTRACT",
                "variableName": "PMUSER_LANG"
            }
        },
        {
            "name": "setVariable",
            "options": {
                "transform": "NONE",
                "valueSource": "EXPRESSION",
                "variableName": "PMUSER_X_FORWARDED_HOST",
                "variableValue": "{{builtin.AK_HOST}}"
            }
        },
        {
            "name": "setVariable",
            "options": {
                "transform": "NONE",
                "valueSource": "EXPRESSION",
                "variableName": "PMUSER_EDGEOPTIMIZE_CACHE_KEY",
                "variableValue": "LLMCLIENT=TRUE;X_FORWARDED_HOST={{builtin.AK_HOST}}"
            }
        },
        {
            "name": "caching",
            "options": {
                "behavior": "CACHE_CONTROL_AND_EXPIRES",
                "cacheControlDirectives": "",
                "defaultTtl": "1d",
                "enhancedRfcSupport": false,
                "honorMustRevalidate": false,
                "honorPrivate": false,
                "mustRevalidate": false
            }
        },
        {
            "name": "modifyIncomingRequestHeader",
            "options": {
                "action": "MODIFY",
                "avoidDuplicateHeaders": true,
                "customHeaderName": "x-edgeoptimize-api-key",
                "newHeaderValue": "<your api-key here>",
                "standardModifyHeaderName": "OTHER"
            }
        },
        {
            "name": "modifyIncomingRequestHeader",
            "options": {
                "action": "MODIFY",
                "avoidDuplicateHeaders": true,
                "customHeaderName": "x-edgeoptimize-config",
                "newHeaderValue": "LLMCLIENT={{user.PMUSER_LLMCLIENT}};LANG={{user.PMUSER_LANG}}",
                "standardModifyHeaderName": "OTHER"
            }
        },
        {
            "name": "modifyIncomingRequestHeader",
            "options": {
                "action": "MODIFY",
                "avoidDuplicateHeaders": true,
                "customHeaderName": "x-edgeoptimize-url",
                "newHeaderValue": "{{builtin.AK_URL}}",
                "standardModifyHeaderName": "OTHER"
            }
        },
        {
            "name": "cacheId",
            "options": {
                "rule": "INCLUDE_VARIABLE",
                "variableName": "PMUSER_EDGEOPTIMIZE_CACHE_KEY"
            }
        },
        {
            "name": "modifyIncomingResponseHeader",
            "options": {
                "action": "DELETE",
                "customHeaderName": "Age",
                "standardDeleteHeaderName": "OTHER"
            }
        },
        {
            "name": "prefreshCache",
            "options": {
                "enabled": true,
                "prefreshval": 90
            }
        },
        {
            "name": "modifyOutgoingRequestHeader",
            "options": {
                "action": "MODIFY",
                "avoidDuplicateHeaders": true,
                "customHeaderName": "X-Forwarded-Host",
                "newHeaderValue": "{{builtin.AK_HOST}}",
                "standardModifyHeaderName": "OTHER"
            }
        }
    ],
    "criteria": [
        {
            "name": "userAgent",
            "options": {
                "matchCaseSensitive": false,
                "matchOperator": "IS_ONE_OF",
                "matchWildcard": true,
                "values": [
                    "*AdobeEdgeOptimize-AI*",
                    "*ChatGPT-User*",
                    "*GPTBot*",
                    "*OAI-SearchBot*",
                    "*PerplexityBot*",
                    "*Perplexity-User*"
                ]
            }
        },
        {
            "name": "path",
            "options": {
                "matchCaseSensitive": false,
                "matchOperator": "MATCHES_ONE_OF",
                "normalize": false,
                "values": [
                ]
            }
        },
        {
            "name": "requestHeader",
            "options": {
                "headerName": "x-edgeoptimize-request",
                "matchOperator": "DOES_NOT_EXIST",
                "matchWildcardName": false
            }
        },
        {
            "name": "matchVariable",
            "options": {
                "matchCaseSensitive": true,
                "matchOperator": "IS",
                "matchWildcard": false,
                "variableExpression": "FALSE",
                "variableName": "PMUSER_EDGEOPTIMIZE_DISABLE"
            }
        }
    ],
    "criteriaMustSatisfy": "all"
}
```

Important considerations:

* Edge Optimize Rule will be ON based on User-Agent + Path + x-edgeoptimize-request (if not present) + EDGEOPTIMIZE_DISABLE variable (to allow switch off using a single variable toggle)
* Set up rules to **Modify Incoming Request Headers** rule to set custom headers
* Set cache-key in Akamai using user defined variable through Cache-ID modification mechanism. Only a single user defined variable is allowed, so create a separate variable for cache_key and set it accordingly.
* With Cache ID Modification within a match on User Agent, the content can't be purged by URL (just FYI)
* Site failover mechanism: With the match on User-Agent rule, Akamai does not allow failover based on health check, but only on the basis of origin response/connectivity per request. Set **x-edgeoptimize-fo:true**  resp header in case of failover response.
* SWR is not supported by Akamai. So, only TTL based caching is there. So, configure a rule in Akamai to strip Age header from origin response else TTL based caching would not work.
* Ensure that the Edge Optimize rule is the bottom most rule in the rule hierarchy (so that it overrides all other rules).

To test the setup, run a curl and expect the following:
```
curl -svo page.html https://www.example.com/page.html --header "user-agent: chatgpt-user"
< HTTP/2 200
< x-edgeoptimize-request-id: 50fce12d-0519-4fc6-af78-d928785c1b85

```

>[!ENDTABS]

>[!NOTE]
>For other CDN providers, please reach out to `llmo-at-edge@adobe.com` to assist your IT/CDN teams with onboarding. Once the setup configurations are complete, you can deploy suggestions for Optimize at Edge opportunities in LLM Optimizer.

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
