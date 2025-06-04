# 🛡️ SAP API Management: Policy Guide

Policies in SAP API Management (APIM) allow you to control, secure, transform, and analyze traffic between API consumers and backend services. Policies are reusable building blocks that can be applied to an API proxy.

---

## 📋 Policy Categories

| Category             | Purpose                                           |
|----------------------|---------------------------------------------------|
| **Security**         | Authentication, authorization, IP filtering      |
| **Traffic Management** | Throttle, spike arrest, quota enforcement      |
| **Mediation**        | Data transformation, content filtering           |
| **Routing**          | Conditional and dynamic backend routing          |
| **Extension**        | Script or logic injection                        |
| **Transformation** | XML to JSON, JSON to XML, XSLT, XSL                |
| **Analytics**        | Logging and monitoring of traffic                |
| **Error Handling**   | Custom error messages and behavior               |

---

## 🔐 Security Policies

### 🔑 OAuth2 Policy

- **Use Case**: Protect API using OAuth2 access tokens.
- **Features**: Token validation, introspection with XSUAA or external identity provider.
- **Setup**:
  - Add `VerifyOAuthToken` policy.
  - Set `tokenLocation`, `introspectionEndpoint`.

### 🔐 API Key Verification

- **Use Case**: Secure API with API Key authentication.
- **Features**: Header or query-based key lookup.
- **Setup**:
  - Add `VerifyAPIKey` policy under `PreFlow`.
  - Provide key location (header/query param).

### 📌 IP Allow/Deny List

- **Use Case**: Restrict access to specific client IPs.
- **Features**: Block or allow traffic based on IP.
- **Setup**:
  - Use `AccessControl` policy with IP lists.

---

## 📊 Traffic Management Policies

### 🚦 Quota

- **Use Case**: Set maximum number of calls for a time window.
- **Features**: Enforce per app/user plan limits.
- **Setup**:
  - Add `Quota` policy under `PreFlow`.
  - Define `allow`, `interval`, `timeUnit`.

### ⚡ Spike Arrest

- **Use Case**: Prevent sudden spikes in request rate.
- **Features**: Request rate smoothing.
- **Setup**:
  - Use `SpikeArrest` policy (e.g., 10 requests/second).

### ⏱️ Rate Limit

- **Use Case**: Restrict API access based on rate plans.
- **Features**: Works with API Plans/Products.
- **Setup**:
  - Add to API Product plan.

---

## 🔄 Mediation Policies

### 🔄 XML to JSON (and vice versa)

- **Use Case**: Convert data between XML and JSON.
- **Features**: Payload transformation.
- **Setup**:
  - Use `XMLToJSON` or `JSONToXML` policy under `Request` or `Response`.

### 🔧 Assign Message

- **Use Case**: Add/modify headers, query params, payload.
- **Features**: Flexible message construction.
- **Setup**:
  - Use `AssignMessage` policy to manipulate variables and flow.

### 🧪 XSLT/MessageTransform

- **Use Case**: Use XSLT to transform XML payloads.
- **Setup**:
  - Embed XSLT script or reference external file.

---

## 🧭 Routing Policies

### 🔁 Target Endpoint Routing

- **Use Case**: Change target backend dynamically.
- **Features**: Load balancing, failover.
- **Setup**:
  - Use `AssignMessage` to update `target.url`.

### 🔀 Conditional Flow Routing

- **Use Case**: Route based on request values (headers, paths).
- **Features**: Branching logic.
- **Setup**:
  - Define `FlowCondition` on `Flow` level in policy editor.

---

## 🧠 Extension Policies

### 💡 JavaScript Policy

- **Use Case**: Add custom logic or dynamic processing.
- **Features**: Full JS environment access.
- **Setup**:
  - Add `JavaScript` policy, embed or link script.

### 📜 Python (Not supported natively)

- Only JavaScript and Groovy scripts are supported natively.

### 🧱 Raise Fault

- **Use Case**: Terminate flow with custom error message.
- **Features**: Custom status codes, error payloads.
- **Setup**:
  - Add `RaiseFault` policy under `Request` or `Response`.

---

## 📈 Analytics and Logging

### 📊 StatisticsCollector

- **Use Case**: Capture traffic metrics.
- **Setup**:
  - Use `StatisticsCollector` policy to record metrics like latency, traffic.

### 📝 Message Logging

- **Use Case**: Log request/response payloads.
- **Setup**:
  - Use `MessageLogging` policy.
  - Requires destination configuration.

---

## 🔁 Transformation Policies

### 🔄 XML to JSON

- **Use Case**: Convert XML payload to JSON for clients.
- **Setup**:
  - Add `XMLToJSON` policy after response from target.

```xml
<XMLToJSON/>
```
---

### 🔄 JSON to XML

- **Use Case**: Convert JSON payload to XML before passing to legacy systems.
- **Setup**:
  - Use `JSONToXML` in PreFlow or PostFlow.

---

### 🔄 XSL / XSLT Transformation

- **Use Case**: Apply advanced transformation logic using XSLT.
- **Setup**:
  - Attach `.xsl` file and reference in `XSLTransform`.

---

## 🔁 Routing & Target Configuration

### 📍 Route Rule

- **Use Case**: Dynamically switch target endpoints based on logic.
- **Setup**:
  - Define `RouteRule` with multiple target endpoints.

---

### 🎯 TargetEndpoint

- **Use Case**: Define actual backend system/service endpoint.
- **Setup**:
  - Configure target base URL, path, credentials, etc.

---

## ❌ Error Handling

### ❗ Fault Rules

- **Use Case**: Catch policy failures and handle them.
- **Features**: Return custom error codes/messages.
- **Setup**:
  - Define `FaultRules` block in the API proxy XML.

---

## 🛠️ How to Apply a Policy

1. Go to **API Portal** in BTP Integration Suite.
2. Select an API Proxy.
3. Open **Policy Editor**.
4. Choose the flow: `PreFlow`, `PostFlow`, or conditional.
5. Click **+** to add a policy.
6. Select from policy list and configure it.
7. Deploy the proxy after saving changes.

---

## ✅ Example: Verify API Key + Quota + JSON Response

```xml
<PreFlow>
  <Request>
    <Step><Name>Verify-API-Key</Name></Step>
    <Step><Name>Apply-Quota</Name></Step>
  </Request>
  <Response>
    <Step><Name>XML-to-JSON</Name></Step>
  </Response>
</PreFlow>
```