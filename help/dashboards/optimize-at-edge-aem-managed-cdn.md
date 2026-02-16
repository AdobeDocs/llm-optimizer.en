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

After completing the setup, [verify the configuration](/help/dashboards/optimize-at-edge.md#verify-the-setup) to confirm that traffic is being routed correctly.
