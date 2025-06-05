# 🔐 Knowledge of Technical Authorization Types for System Connectivity

---

## 🧭 What Are Technical Authorizations?

Technical authorizations define **how systems authenticate and authorize** themselves (not end-users) when connecting to each other. These are crucial for **API calls, data integrations, service invocations**, and **secure system-to-system communication**.

---

## 🔑 Common Technical Authorization Types

---

### 1. **Basic Authentication**

#### 🔍 Description:
Uses a combination of **username and password** passed in the HTTP header, encoded in Base64.

#### ✅ Use Cases:
- Simple API integrations
- Test systems
- Legacy systems

#### ⚠️ Limitations:
- Weak security (if not used with HTTPS)
- Not recommended for production
- No session control or token lifecycle

---

### 2. **Client Certificate Authentication**

#### 🔍 Description:
Uses **X.509 certificates** for mutual TLS (mTLS). The client presents a certificate to prove its identity to the server.

#### ✅ Use Cases:
- Secure integration between trusted systems
- On-premise ↔ cloud via SAP Cloud Connector
- SAP Integration Suite secure APIs

#### 🛡 Benefits:
- Strong cryptographic validation
- Certificate revocation and lifecycle control
- Used for **principal propagation**

---

### 3. **OAuth 2.0 Client Credentials Grant**

#### 🔍 Description:
A standard protocol that issues **access tokens** to clients based on their **Client ID and Client Secret**, without user interaction.

#### ✅ Use Cases:
- Service-to-service communication (e.g., SAP Integration Suite → S/4HANA)
- API Management secured API calls
- External apps accessing SAP BTP APIs

#### 🛡 Benefits:
- Time-limited access tokens
- Scopes for permission control
- Modern and secure industry standard

---

### 4. **SAML 2.0 (Security Assertion Markup Language)**

#### 🔍 Description:
Used for **federated identity** and single sign-on (SSO). Can also be used for **technical user assertion** in enterprise integrations.

#### ✅ Use Cases:
- SAP BTP ↔ SAP S/4HANA (user propagation)
- Integration flows requiring identity forwarding

#### 🛡 Benefits:
- Enforces trust via Identity Providers (IdP)
- Used in Principal Propagation

---

### 5. **Principal Propagation**

#### 🔍 Description:
Allows forwarding the identity of the **original user** across systems (e.g., from SAP BTP to S/4HANA) using a secure identity chain.

#### ✅ Use Cases:
- End-to-end auditing and authorization
- Cloud workflows invoking on-premise services
- SAP Launchpad or Fiori apps

#### ⚙️ Requirements:
- Trust between Identity Providers (SAP ID service ↔ Corporate IdP)
- Cloud Connector configuration
- Backend system must accept propagated users

---

### 6. **OAuth 2.0 Authorization Code Grant (User-Based)**

#### 🔍 Description:
Used when a user logs in to a client app, which then receives a token to access protected resources.

#### ✅ Use Cases:
- Hybrid apps (Fiori/UI5)
- Workflow apps on SAP BTP
- User-initiated integration flows

#### 🛡 Benefits:
- Tokens can be refreshed
- Scoped access
- Industry standard for web/mobile apps

---

### 7. **API Key Authentication**

#### 🔍 Description:
A simple token (string) passed in the header or query parameter to authenticate a client.

#### ✅ Use Cases:
- Prototyping or internal APIs
- API Management in sandbox/test stages

#### ⚠️ Limitations:
- No user identity context
- No expiry or lifecycle management
- Harder to audit or revoke

---

## 🧩 SAP Tools and Where They Apply

| Tool | Recommended Auth Types |
|------|------------------------|
| SAP Integration Suite | OAuth 2.0 (Client Credentials), Certificate, Basic Auth |
| SAP API Management | API Key, OAuth 2.0, SAML, Certificate |
| SAP Cloud Connector | Certificate, Principal Propagation |
| SAP Destination Service | OAuth 2.0, Basic Auth, Certificate |
| SAP Workflow & Fiori Launchpad | OAuth (Auth Code), Principal Propagation |
| On-Premise S/4HANA | Basic Auth, Certificate, SAML |

---

## 🔐 Best Practices

- ✅ Prefer **OAuth 2.0** or **Certificates** over Basic Auth
- ✅ Use **Principal Propagation** for secure identity handover
- ✅ Use **short-lived tokens** (OAuth) with refresh flows
- ✅ Keep credentials in **secure credential stores** (e.g., SAP BTP destinations, SAP Secrets Manager)
- ✅ Rotate and revoke credentials regularly
- ✅ Audit and log access to backend systems

---

## 📘 Summary Table

| Authorization Type        | Secure | Best For                           | Notes                                  |
|---------------------------|--------|------------------------------------|----------------------------------------|
| Basic Authentication      | ⚠️     | Simple, legacy integrations         | Use only over HTTPS                    |
| Certificate Authentication| ✅     | Internal trusted communication     | mTLS support required                  |
| OAuth 2.0 (Client Cred.)  | ✅     | App-to-App APIs, BTP services       | Token-based, modern and scalable      |
| OAuth 2.0 (Auth Code)     | ✅     | User-authenticated apps             | Requires user interaction              |
| API Key                   | ⚠️     | Internal or test APIs               | No user context, no expiration         |
| SAML 2.0                  | ✅     | SSO, federated identity             | Useful in Principal Propagation        |
| Principal Propagation     | ✅     | Full user identity traceability     | Requires trust configuration           |

---

> 🔑 **Choose the authorization type based on system capabilities, security level needed, and operational context.**

