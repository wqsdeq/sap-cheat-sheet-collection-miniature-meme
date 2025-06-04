# 📘 SAP BTP Guide: Understanding Subaccounts and Services

## 🔹 What is a Subaccount?

A **Subaccount** is a logical container within a Global Account in SAP BTP. It allows you to:
- Organize environments (Dev, Test, Prod)
- Assign services and entitlements
- Deploy applications and manage user access
- Use different regions or environments (e.g., Cloud Foundry, Kyma)

Each subaccount is isolated and can be independently configured.

---

## 🔸 What are Services?

**Services** in SAP BTP provide specific technical or business capabilities. Examples include:
- **SAP Integration Suite** – for integrating systems and APIs
- **SAP HANA Cloud** – database as a service
- **SAP Business Application Studio (BAS)** – cloud IDE
- **Destination Service** – manage external connections

Services are provisioned and assigned at the subaccount level.

---

## 🧭 Guide: How to Create a Subaccount and Assign Integration Suite

### ✅ Prerequisites:
- Access to SAP BTP Cockpit: [https://account.hana.ondemand.com](https://account.hana.ondemand.com)
- A Global Account with available **entitlements** for Integration Suite

---

### 📁 Step 1: Create a Subaccount

1. Log in to **SAP BTP Cockpit**
2. Navigate to your **Global Account**
3. Click **"Create"** → **Subaccount**
4. Fill in the details:
   - **Display Name**: e.g., `integration-dev`
   - **Region**: Choose one close to your users (e.g., `Europe (Frankfurt)`)
   - **Subdomain**: Auto-generated or custom
   - **Environment**: Select `Cloud Foundry`
5. Click **"Create"**

---

### 📦 Step 2: Enable Cloud Foundry

1. Open your new **Subaccount**
2. Click **"Enable Cloud Foundry"**
3. Choose an **Org Name**
4. Click **"Create"**
5. After provisioning, create a **Space** (e.g., `dev`) inside the org

---

### 🎫 Step 3: Assign Entitlements (Add Integration Suite)

1. Go back to the **Global Account**
2. Click **Entitlements** → **Entity Assignments**
3. Select your **Subaccount**
4. Click **"Configure Entitlements"**
5. Click **"Add Service Plans"**
6. Search for **Integration Suite**
7. Add the desired **service plan** (e.g., `standard`)
8. Click **Save**

---

### 🔧 Step 4: Subscribe to Integration Suite

1. Go to the **Subaccount**
2. Click **"Subscriptions"**
3. Search for **Integration Suite**
4. Click **"Subscribe"**
5. Wait until the status shows **Subscribed**

---

### 🔑 Step 5: Assign Roles (Optional but Recommended)

1. Go to **Security** → **Role Collections**
2. Create or modify a role collection for Integration Suite
3. Assign it to your user under **Trust Configuration** → **Users**

---

## 📌 Tips

- Use directories to group related subaccounts.
- Always check if the service plan is available in your region.
- Use meaningful names for subaccounts and spaces.

---

## 📚 Additional Resources

- [SAP BTP Documentation](https://help.sap.com/btp)
- [SAP Integration Suite Overview](https://help.sap.com/docs/integration-suite)

