# 🔐 SAP BTP Access Management Guide (Global Account, Subaccount, and Services)

This guide explains how to manage user access and roles across **Global Accounts**, **Subaccounts**, and **Services** in SAP Business Technology Platform (BTP).

---

## 📁 1. Access Levels in SAP BTP

| Level            | Scope                              | Access Control Tool                        |
|------------------|-------------------------------------|---------------------------------------------|
| Global Account   | Overall account administration      | Global Account Directory → Members tab      |
| Subaccount       | Project or environment level access | Subaccount → Security → Users/Role Collections |
| Services         | Functional service access           | Role Collections + XSUAA/App-specific roles |

---

## 👤 2. Manage Users at the Global Account Level

### 🔸 Use Case:
- Manage administrators and quota managers at the **global level**.

### 🧭 Steps:
1. Go to [SAP BTP Cockpit](https://account.hana.ondemand.com)
2. Select your **Global Account**
3. Click **Security → Users**
4. Click **Add Member**
5. Provide the **Email Address** and select **Global Roles**:
   - `Global Account Administrator`
   - `Global Account Viewer`
   - `Quota Administrator`

---

## 🌐 3. Manage Users at the Subaccount Level

### 🔸 Use Case:
- Control who can develop, deploy, and manage apps in specific subaccounts.

### 🧭 Steps:
1. In the BTP Cockpit, open the **Subaccount**
2. Navigate to **Security → Users**
3. Click **Assign User**
4. Enter the user’s **email** and select one or more **role collections**
   - Example: `Subaccount Administrator`, `Developer`, `Viewer`

---

## 🗂 4. Create and Manage Role Collections

### 🔸 Purpose:
Group multiple roles (from services or apps) into collections and assign to users.

### 🧭 Steps:
1. Go to **Subaccount → Security → Role Collections**
2. Click **Create Role Collection**
3. Add roles using:
   - **Role Source**: e.g., `XSUAA`, `SAP Service`
   - **Role Name**: Choose predefined roles like `Integration_Developer`
4. Assign the collection to users via **Trust Configuration** or **Users tab**

---

## 🔗 5. Configure Trust Configuration (Identity Provider Setup)

### 🔸 Purpose:
Define where users log in from (SAP ID, Corporate IdP like Azure AD, etc.)

### 🧭 Steps:
1. Go to **Subaccount → Security → Trust Configuration**
2. Add or select your **Identity Provider (IdP)**
3. Assign default role collections based on groups or users
   - Use **SAML attributes** to map users or groups from IdP

---

## 🛠 6. Assign Roles for Services (e.g., Integration Suite)

### 🔸 Steps:
1. Navigate to **Subaccount → Instances and Subscriptions**
2. Click on the provisioned service (e.g., `Integration Suite`)
3. Open the **Application** via the Launchpad
4. **Roles → Create**
5. Assign predefined service roles (e.g., `Integration_Provisioner`, `MessagingSend`) to users

---

## 🧪 7. Test Access

- Ask the assigned user to log in via BTP or the relevant app
- Verify if they can access the required areas
- Use **BTP Audit Logs** (for Enterprise accounts) to review access issues

---

## 🧠 Tips & Best Practices

- 🔄 Use **Role Collections** instead of assigning individual roles
- 🧾 Document who has access to what level and why
- 🔐 Use **least privilege** principle — only assign what’s needed
- 🧪 Periodically review role assignments and access

---

## 📚 Resources

- [SAP BTP Security & Authorizations](https://help.sap.com/docs/btp/security)
- [SAP BTP Role Collections Guide](https://help.sap.com/docs/btp/role-collections)
- [SAP XSUAA Documentation](https://help.sap.com/docs/xsuaa)

---

## ✅ Summary

| Task                        | Where to Perform It               | Purpose                                  |
|-----------------------------|-----------------------------------|-------------------------------------------|
| Add global users            | Global Account → Security         | Manage admins and quota users             |
| Assign subaccount users     | Subaccount → Security → Users     | Give access to project environments       |
| Create role collections     | Subaccount → Security → Role Collections | Group and assign service/app roles   |
| Bind IdP to subaccount      | Subaccount → Trust Configuration  | Map corporate users to role collections   |
| Service-specific access     | Instances → App Settings → User Management | Control app-level roles            |
