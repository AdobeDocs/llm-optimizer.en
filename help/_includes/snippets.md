# Snippets

## Verify the setup - Adobe Managed CDN {#verify-setup-adobe-aem-cs-cdn}

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

## Verify the setup - BYOCDN {#verify-setup-byocdn}

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

![AI Traffic Routing status with routing enabled](/help/assets/optimize-at-edge/byocdn-CDN-traffic-routed-tick.png)

## API key retrieval steps {#retrieve-byocdn-api-key}

**Steps to retrieve your API key:**

1. Navigate to **Customer Configuration** and select the **CDN Configuration** tab.

   ![Navigate to Customer Configuration](/help/assets/optimize-at-edge/prereq-customer-config-nav.png)

2. Under **AI Traffic Routing to Deploy Optimizations**, tick the **Deploy Optimizations to AI Agents** checkbox.

   ![Tick Deploy Optimizations to AI Agents](/help/assets/optimize-at-edge/prereq-deploy-checkbox.png)

3. Copy the API key and proceed with the routing configuration steps below.

   ![Copy the API key](/help/assets/optimize-at-edge/prereq-copy-api-key.png)

   >[!NOTE]
   >At this stage, the status may show a red cross indicating that the setup is not yet completed. This is expected — once you complete the routing configuration below and AI bot traffic starts flowing, the status will update to a green checkmark confirming that routing is successfully enabled.

Additionally, if you require any help with the above steps, reach out to your Adobe account team or `llmo-at-edge@adobe.com`.

## Return to overview {#return-to-overview}

To learn more about Optimize at Edge, including available opportunities, auto-optimization workflows, and FAQs, return to the [Optimize at Edge overview](/help/dashboards/optimize-at-edge/overview.md).
