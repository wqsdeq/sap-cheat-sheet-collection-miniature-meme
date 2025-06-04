# 🚀 Designing and Implementing Policies in SAP API Management (APIM)
## 🌐 & Exposing External APIs for Cloud Use in Integration Suite

---

## 🧭 Overview

SAP API Management (APIM), part of the Integration Suite, enables you to design, secure, monitor, and expose APIs to external or internal consumers. This guide covers:

- Designing and implementing various policy types
- Exposing an external API using APIM
- Making the API consumable in the Integration Suite

---

## 🧱 Step 1: Import or Create an API Proxy

### 🔹 Options:
- **Import** an OpenAPI/Swagger specification
- **Create** a new API proxy manually

### 📍 Procedure:
1. Go to **SAP BTP Cockpit** → Select **Integration Suite** → Launch **API Management → API Portal**
2. Click **Develop → API Proxies → Create**
3. Choose **From URL** or **From Specification** (e.g., external REST API)
4. Provide a **name, base path, and target endpoint URL**

---

## 🛡 Step 2: Design & Implement Policies

Policies can be attached to:
- **ProxyEndpoint** (request from client)
- **TargetEndpoint** (response from backend)

### 🔒 Security Policies

#### ✅ API Key Verification

```xml
<VerifyAPIKey async="false">
  <APIKey ref="request.queryparam.apikey"/>
</VerifyAPIKey>
```

📌 **Use case**: Secures APIs by verifying API keys in requests.

---

#### ✅ OAuth 2.0 Validation

```xml
<OAuthV2 name="OAuth">
  <Operation>VerifyAccessToken</Operation>
  <AccessTokenPrefix>Bearer</AccessTokenPrefix>
</OAuthV2>
```

📌 **Use case**: Validates tokens issued by identity providers (e.g., XSUAA, IAS).

---

### 🔄 Transformation Policies

#### 🔁 Convert XML to JSON

```xml
<XMLToJSON/>
```

📌 **Use case**: Convert XML backend response to JSON for frontend compatibility.

---

#### 🔁 Add Custom Headers (AssignMessage)

```xml
<AssignMessage>
  <Set>
    <Headers>
      <Header name="X-Environment">Production</Header>
    </Headers>
  </Set>
</AssignMessage>
```

📌 **Use case**: Add headers for routing, debugging, or metadata purposes.

---

### 🚦 Traffic Management Policies

#### ⏳ Quota Policy

```xml
<Quota>
  <Allow count="1000"/>
  <Interval>1</Interval>
  <TimeUnit>month</TimeUnit>
  <Identifier ref="request.header.apikey"/>
</Quota>
```

📌 **Use case**: Limit the number of requests an app can make in a period.

---

#### 🚧 Spike Arrest

```xml
<SpikeArrest>
  <Rate>5ps</Rate>
</SpikeArrest>
```

📌 **Use case**: Prevent traffic spikes and DoS attacks.

---

### 🐞 Error Handling

#### Raise Custom Fault

```xml
<RaiseFault>
  <FaultResponse>
    <Set>
      <Payload>{"error":"Unauthorized"}</Payload>
      <StatusCode>401</StatusCode>
    </Set>
  </FaultResponse>
</RaiseFault>
```

📌 **Use case**: Send structured error responses when authentication fails.

---

## 🔌 Step 3: Expose External API for Cloud Use

### Steps:
1. **Secure** the API using API Key or OAuth policies.
2. **Add Traffic Control** to avoid overloading external systems.
3. **Customize Payloads** using transformation policies if needed.
4. **Save and Deploy** the API Proxy.

🔗 Your API is now exposed at:
```bash
https://<subdomain>.<region>.apimanagement.<btp-domain>/<base-path>
```

---

## 🔄 Step 4: Consume the API in Integration Suite

### In Cloud Integration:
1. Go to **Integration Suite → Design → Integrations**
2. Create or open an **iFlow**
3. Add an **HTTP Receiver Adapter**
4. Enter the exposed API URL from APIM
5. Configure **Authentication Method** (e.g., API Key Header or OAuth Token)
6. Deploy and test

---

## 🧠 Best Practices

- Always use **Spike Arrest + Quota** for public APIs
- Secure APIs using **OAuth** for enterprise-grade use
- Use **Message Logging** to monitor traffic in non-production
- Separate **business logic** in iFlows and **access control** in APIM

---

## 📚 References

- [SAP API Management - Help Portal](https://help.sap.com/docs/api-management)
- [SAP Integration Suite Overview](https://help.sap.com/docs/integration-suite)
- [Tutorial: Expose and Secure APIs](https://developers.sap.com/group.api-management.html)

