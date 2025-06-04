# 📘 XML Coding Guide for SAP API Management

SAP API Management policies are defined and configured using **XML-based configuration files** within API proxies. Understanding how to write and modify XML for these policies is essential for controlling API behavior.

---

## 📦 Basic Structure of an API Proxy

Every API proxy contains these components:

- `ProxyEndpoint`: Defines how the API is exposed externally.
- `TargetEndpoint`: Defines the actual backend API the proxy calls.
- `Policies`: XML elements that define behaviors like security, transformation, and error handling.

---

## 🧱 XML Structure of an API Proxy

```xml
<APIProxy name="my-api">
  <Description>Sample Proxy</Description>
  <BasePaths>
    <BasePath>/v1/my-api</BasePath>
  </BasePaths>
  <ProxyEndpoints>
    <ProxyEndpoint>default</ProxyEndpoint>
  </ProxyEndpoints>
  <TargetEndpoints>
    <TargetEndpoint>default</TargetEndpoint>
  </TargetEndpoints>
</APIProxy>
```

---

## 🔗 ProxyEndpoint Example

```xml
<ProxyEndpoint name="default">
  <Description>External interface</Description>
  <PreFlow name="PreFlow">
    <Request>
      <Step>
        <Name>Verify-API-Key</Name>
      </Step>
    </Request>
    <Response/>
  </PreFlow>
  <RouteRule name="default">
    <TargetEndpoint>default</TargetEndpoint>
  </RouteRule>
</ProxyEndpoint>
```

---

## 🎯 TargetEndpoint Example

```xml
<TargetEndpoint name="default">
  <Description>Calls the backend</Description>
  <URL>https://backend.example.com/api</URL>
  <HTTPTargetConnection>
    <URL>https://backend.example.com/api</URL>
  </HTTPTargetConnection>
</TargetEndpoint>
```

---

## 🔒 Security Policies

### ✅ VerifyAPIKey

```xml
<VerifyAPIKey name="Verify-API-Key">
  <APIKey ref="request.queryparam.apikey"/>
</VerifyAPIKey>
```

- **Purpose**: Verifies API keys sent via query parameter or header.
- **Position**: Place in ProxyEndpoint → PreFlow → Request.

---

### ✅ OAuth2

```xml
<OAuthV2 name="OAuth-Policy">
  <Operation>VerifyAccessToken</Operation>
  <AccessTokenPrefix>Bearer</AccessTokenPrefix>
</OAuthV2>
```

- **Purpose**: Validates OAuth 2.0 tokens.
- **Tip**: Use with XSUAA, Azure AD, or SAP Identity Authentication.

---

## 🔄 Transformation Policies

### 🔁 XML to JSON

```xml
<XMLToJSON name="ConvertXMLToJSON"/>
```

### 🔁 JSON to XML

```xml
<JSONToXML name="ConvertJSONToXML"/>
```

### 🔁 XSLT Transformation

```xml
<XSLTransform name="XSLT-Transform">
  <Source>request</Source>
  <XSL ref="transform.xsl"/>
</XSLTransform>
```

---

## 🧪 Mediation & Utility Policies

### ✍️ AssignMessage

Used to create or modify payloads, headers, and query parameters.

```xml
<AssignMessage name="Add-Custom-Header">
  <Set>
    <Headers>
      <Header name="X-Environment">Production</Header>
    </Headers>
  </Set>
  <AssignTo type="request" createNew="false"/>
</AssignMessage>
```

---

### 🚫 RaiseFault

Used to stop execution and return a custom error message.

```xml
<RaiseFault name="Invalid-Key-Fault">
  <FaultResponse>
    <Set>
      <Headers>
        <Header name="Content-Type">application/json</Header>
      </Headers>
      <Payload>{"error":"Invalid API Key"}</Payload>
    </Set>
  </FaultResponse>
</RaiseFault>
```

---

## 🚦 Traffic Management

### ⏳ Quota

```xml
<Quota name="MonthlyQuota">
  <Allow count="1000"/>
  <Interval>1</Interval>
  <TimeUnit>month</TimeUnit>
  <Identifier ref="request.header.apikey"/>
</Quota>
```

### 🛡 Spike Arrest

```xml
<SpikeArrest name="LimitSpikeRate">
  <Rate>10ps</Rate> <!-- 10 requests per second -->
</SpikeArrest>
```

---

## 🐞 Fault Handling

Add error handling to your ProxyEndpoint:

```xml
<FaultRules>
  <FaultRule name="Invalid-Token">
    <Condition>(fault.name = "InvalidAccessToken")</Condition>
    <Step>
      <Name>RaiseFault</Name>
    </Step>
  </FaultRule>
</FaultRules>
```

---

## 🛠 Tips for XML in APIM

- Always **name your policies** for easy reference.
- Use **Condition tags** to apply policies selectively:
  ```xml
  <Step>
    <Name>VerifyAPIKey</Name>
    <Condition>request.verb = "GET"</Condition>
  </Step>
  ```
- Store sensitive data like credentials in **Key Value Maps** (KVMs).
- Use **Policy Templates** to standardize reusable XML logic.

---

## 📚 Resources

- [SAP API Management Help](https://help.sap.com/docs/api-management)
- [SAP API Portal (Trial)](https://cockpit.hanatrial.ondemand.com)
- [SAP Policy Reference Guide](https://help.sap.com/viewer/product/SAP_API_Management)
- [XML coding for beginners](https://www.youtube.com/watch?v=1JblVElt5K0&list=PLhW3qG5bs-L9DloLUPwC3GdFimY5Ce_gS)

