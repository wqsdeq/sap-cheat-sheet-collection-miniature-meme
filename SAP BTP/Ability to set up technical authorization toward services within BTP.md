# 🔐 SAP BTP: Setting Up Technical Authorization Toward Services

This guide explains how to enable secure **technical access (machine-to-machine)** to SAP BTP services (e.g., Destination, Connectivity, Integration Suite, XSUAA) using proper roles, scopes, and bindings.

---

## 📌 Use Case

Technical authorization is needed when:
- A backend service needs to consume another BTP service (e.g., app accessing Destination or Connectivity)
- Applications need to communicate securely without a user context (M2M)
- External systems (like CI/CD pipelines or APIs) need limited BTP access

---

## 🧱 Overview of Key Concepts

| Concept             | Description                                                                 |
|---------------------|-----------------------------------------------------------------------------|
| **XSUAA**           | Authorization & Trust service (OAuth 2.0 provider in BTP)                   |
| **Service Instance**| A provisioned BTP service (e.g., Destination, HANA, Integration Suite)      |
| **Service Key**     | Credentials (client ID/secret, tokens, endpoints) for programmatic access   |
| **Role Template**   | Definition of a role with scopes (in `xs-security.json`)                    |
| **JWT Token**       | Used to grant secure access to a service                                    |

---

## 🔧 Step-by-Step: Enable Technical Access

---

## 🥇 Step 1: Create Service Instances

1. Go to **Subaccount → Service Marketplace**
2. Search for your service (e.g., `Destination`, `Connectivity`, `XSUAA`)
3. Click the service → **Create Instance**
4. Provide configuration parameters (if required)

Example: XSUAA Instance (for technical client)

```json
{
  "xsappname": "my-tech-client",
  "tenant-mode": "dedicated",
  "oauth2-configuration": {
    "grant-types": ["client_credentials"]
  }
}
```

> ✅ This enables the instance to use the `client_credentials` grant type for technical access.

---

## 🥈 Step 2: Create Service Key (for programmatic access)

1. Go to **Subaccount → Instances and Subscriptions**
2. Click on the XSUAA or Destination instance
3. Click **Create Service Key**
4. Name it (e.g., `tech-access-key`)
5. Save the credentials shown (especially `clientid`, `clientsecret`, `url`)

---

## 🥉 Step 3: Get Access Token via OAuth 2.0

Use the service key credentials to get a token using `client_credentials` grant type.

```bash
curl --location --request POST 'https://<oauth-url>/oauth/token' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'grant_type=client_credentials' \
--data-urlencode 'client_id=<clientid>' \
--data-urlencode 'client_secret=<clientsecret>'
```
> 🔐 This returns a JWT token which you can use to access services.

---

## 🏅 Step 4: Use Token to Access BTP Service

Now, use the token to authenticate API calls or service requests.

```bash
curl --location --request GET 'https://<destination-service-url>/destination-configuration/v1/destinations' \
--header 'Authorization: Bearer <access_token>'
```
---

## 📂 Optional: Use Role Collections for Fine-Grained Scoping

If your service (e.g., CAP app or Integration Suite) defines **custom scopes** in its `xs-security.json`, create a role collection and assign scopes accordingly.

1. Go to **Subaccount → Security → Role Collections**
2. Create collection (e.g., `Integration_Access`)
3. Add roles from the app (e.g., `integration-app!t0.TechAccess`)
4. Use XSUAA's `authorities` claim to map scopes into the JWT.

---

## 🔄 Step 5: Bind Services to Applications

If you're developing an app (CAP, Node.js, Java), bind services during deployment.

###bash
cf bind-service my-app xsuaa-instance
cf restage my-app

Or, in `mta.yaml`:

```yaml
resources:
  - name: xsuaa-instance
    type: org.cloudfoundry.managed-service
    parameters:
      service: xsuaa
      service-plan: application
      config: ./xs-security.json
```
---

## 🧪 Step 6: Test and Validate Technical Authorization

1. Call your service endpoint with the access token
2. Use tools like:
   - [Postman](https://postman.com)
   - `curl` or scripts
   - JWT.io to decode the access token and verify scopes

---

## ✅ Summary Checklist

| Task                              | Description                                    |
|-----------------------------------|------------------------------------------------|
| Create service instance           | Destination / XSUAA / Connectivity             |
| Define security config            | Use `xs-security.json`                         |
| Generate service key              | For client ID & secret                         |
| Get access token                  | Via OAuth `client_credentials`                |
| Bind services to apps             | For runtime environment                        |
| Verify scopes and roles           | Via decoded JWT or log inspection              |

---

## 📚 References

- [XSUAA OAuth2 Configuration](https://help.sap.com/docs/xsuaa)
- [SAP BTP Service Keys](https://help.sap.com/docs/btp/service-keys)
- [SAP BTP Security Best Practices](https://community.sap.com/topics/btp/security)

