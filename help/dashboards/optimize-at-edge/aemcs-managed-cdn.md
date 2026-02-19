---
title: Optimize at Edge - AEM Cloud Service Managed CDN (Fastly)
description: Learn how to configure the AEM Cloud Service Managed CDN (Fastly) for Optimize at Edge in LLM Optimizer.
feature: Opportunities
---

# AEM Cloud Service Managed CDN (Fastly)

This configuration routes agentic traffic (requests from AI bots and LLM user agents) to the Edge Optimize backend service (`live.edgeoptimize.net`). Human visitors and SEO bots continue to be served from your origin as usual. To test the configuration, after the setup is complete, look for the header `x-edgeoptimize-request-id` in the response.

**Prerequisites**

To start routing agentic traffic to Edge Optimize:

1. Navigate to **Customer Configuration** and select the **CDN Configuration** tab.

   ![Navigate to Customer Configuration](/help/assets/optimize-at-edge/prereq-customer-config-nav.png)

2. Under **AI Traffic Routing to Deploy Optimizations**, tick the **Deploy Optimizations to AI Agents** checkbox. The Adobe team will handle the routing configuration on your behalf.

   ![Tick Deploy Optimizations to AI Agents](/help/assets/optimize-at-edge/prereq-deploy-checkbox.png)

3. After enabling the checkbox, the status will show that the setup is in progress. The Adobe team will complete the routing configuration for you.

   ![AI Traffic Routing setup in progress](/help/assets/optimize-at-edge/prereq-traffic-routing-progress.png)

   Once the routing is configured and active, the status will update to show a green checkmark indicating that routing is successfully enabled. No further action is required on your end.

Additionally, if you require any help with the above steps, reach out to your Adobe account team or `llmo-at-edge@adobe.com`.

**Self-service routing via Cloud Manager Pipeline**

If you prefer to configure the routing yourself through the Cloud Manager Pipeline, follow the steps below. The routing configuration is done by using an [originSelector CDN rule](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn-configuring-traffic#origin-selectors). The prerequisites are as follows:

* Decide the domain to be routed.
* Decide the paths to be routed.
* Decide the user agents to be routed (recommended regex).

In order to deploy the rule, you need to:

* Create a [configuration pipeline](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/operations/config-pipeline).
* Commit the `cdn.yaml` configuration file in your repository.
* Run the configuration pipeline.

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

**Verify the setup**

After completing the setup, verify that bot traffic is being routed to Edge Optimize and that human traffic remains unaffected.

**1. Test bot traffic (should be optimized)**

Simulate an AI bot request using an agentic user-agent:

```
curl -svo /dev/null https://www.example.com/page.html \
  --header "user-agent: chatgpt-user"
```

A successful response includes the `x-edgeoptimize-request-id` header, confirming that the request was routed through Edge Optimize:

```
< HTTP/2 200
< x-edgeoptimize-request-id: 50fce12d-0519-4fc6-af78-d928785c1b85
```

**2. Test human traffic (should NOT be affected)**

Simulate a regular human browser request:

```
curl -svo /dev/null https://www.example.com/page.html \
  --header "user-agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36"
```

The response should **not** contain the `x-edgeoptimize-request-id` header. The page content and response time should remain identical to before enabling Optimize at Edge.

**3. How to differentiate between the two scenarios**

| Header | Bot traffic (optimized) | Human traffic (unaffected) |
|---|---|---|
| `x-edgeoptimize-request-id` | Present — contains a unique request ID | Absent |
| `x-edgeoptimize-fo` | Present only if failover occurred (value: `1`) | Absent |

The status of the traffic routing can also be checked in the LLM Optimizer UI. Navigate to **Customer Configuration** and select the **CDN Configuration** tab.

![AI Traffic Routing status with routing enabled](/help/assets/optimize-at-edge/adobe-CDN-traffic-routed-tick.png)

{{return-to-overview}}
