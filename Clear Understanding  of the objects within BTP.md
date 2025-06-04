# 🚀 SAP BTP Objects Cheat Sheet

## 🔷 Global Account
- **Function**: Top-level structure provided by SAP.
- **Use Case**: Manages subaccounts, entitlements, and regions.

## 🔹 Subaccount
- **Function**: Logical container within a global account.
- **Use Case**: Organize Dev/Test/Prod environments, services, users.

## 📁 Directory
- **Function**: Group multiple subaccounts.
- **Use Case**: Organize by region, department, or project.

## 🎫 Entitlements
- **Function**: Control service availability.
- **Use Case**: Allocate service plans (e.g., HANA Cloud, Integration Suite).

## ⚙️ Service Instances
- **Function**: Provisioned services.
- **Use Case**: Create instances of services like HANA, BAS, Integration Suite.

## 🔗 Service Bindings
- **Function**: Connect apps to services.
- **Use Case**: Bind apps to HANA DB or Destination services.

## 🌐 Destinations
- **Function**: Define external connections.
- **Use Case**: Connect to S/4HANA, third-party APIs, on-prem systems.

## 🧱 Spaces (Cloud Foundry)
- **Function**: Runtime container for apps/services.
- **Use Case**: Deploy and manage apps in isolated areas.

## 🧩 Applications
- **Function**: Deployed app logic or UI.
- **Use Case**: CAP or UI5 apps running in Cloud Foundry/Kyma.

## 🛠 Environments
- **Function**: Runtime options (CF, Kyma, ABAP).
- **Use Case**: Choose based on app type (microservice, container, classic ABAP).

## 👥 Roles & Role Collections
- **Function**: Access control.
- **Use Case**: Assign permissions to users for services and apps.

## 🔐 Identity Provider (IdP)
- **Function**: User authentication.
- **Use Case**: Use SAP ID or corporate IdP with SSO.

## 💻 Business Application Studio (BAS)
- **Function**: Cloud IDE.
- **Use Case**: Develop Fiori, CAP, or extension apps.

## 🔄 SAP Integration Suite
- **Function**: Integration platform.
- **Use Case**: Build APIs, workflows, and system connections.

## 🧩 SAP Extension Suite
- **Function**: App extension tools.
- **Use Case**: Extend SAP apps with custom business logic/UI.

## 🧠 SAP HANA Cloud
- **Function**: In-memory cloud database.
- **Use Case**: Store and process business data for apps.

## 🌉 Cloud Connector
- **Function**: Secure tunnel to on-premise systems.
- **Use Case**: Expose internal SAP services securely to BTP.

