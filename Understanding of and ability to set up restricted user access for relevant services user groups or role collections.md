# 🔐 SAP BTP: Setting Up Restricted User Access with Role Collections and User Groups

This guide covers how to restrict access to SAP BTP services using **role collections**, **user groups**, and **identity provider (IdP) integration**.

---

## 📌 Why Restrict Access?

- Ensure **least privilege** access based on user roles.
- Protect sensitive services (e.g., Integration Suite, HANA Cloud).
- Align access with team responsibilities (e.g., Developer, Admin, Viewer).

---

## 🧱 Key Concepts

| Term               | Description                                                                 |
|--------------------|-----------------------------------------------------------------------------|
| **Role**           | A permission set defined by a service (e.g., `Integration_Viewer`)          |
| **Role Collection**| A group of roles assigned to users                                           |
| **User Group**     | Logical group of users (from IdP or directory)                              |
| **Trust Configuration** | Connects your subaccount to an Identity Provider (e.g., Azure AD)   |

---

## 🧭 Step-by-Step: Restrict Access Using Role Collections

### 1️⃣ Create Role Collections

1. Navigate to **Subaccount → Security → Role Collections**
2. Click **Create Role Collection**
3. Give it a name (e.g., `Integration_ReadOnly`)
4. Click **Add Role**:
   - Choose **Role Source** (e.g., `sap.integration.suite`)
   - Choose **Role Name** (e.g., `Integration_Viewer`)
   - Save

> 💡 You can add multiple roles to a collection to match complex needs.

---

### 2️⃣ Create or Use User Groups in Identity Provider

- If using **SAP ID**, create manual mappings.
- If using **Corporate IdP (like Azure AD)**:
  - Create groups (e.g., `BTP_Developers`, `BTP_Viewers`)
  - Add users to the correct groups

---

### 3️⃣ Configure Trust & Role Mapping

1. Go to **Subaccount → Security → Trust Configuration**
2. Select your identity provider (e.g., Azure AD)
3. Click **Role Collection Assignment**
4. Add a mapping:
   - **Attribute**: `groups` or `email`
   - **Value**: e.g., `BTP_Viewers`
   - **Role Collection**: `Integration_ReadOnly`

> ✅ This auto-assigns the role collection when users from that group log in.

---

### 4️⃣ Assign Individual Users (Alternative Method)

1. Go to **Subaccount → Security → Users**
2. Click **Assign User**
3. Enter the user’s email
4. Select one or more **Role Collections**
5. Click **Assign**

> ⚠️ Use this only if IdP-based automation is not configured.

---

## 🧪 Test Access

- Have a user log in to the **service UI** (e.g., Integration Suite)
- Confirm that access is **limited** to the capabilities defined in the role
- If access is too broad or denied, check:
  - Role Collection
  - Mapping rules
  - Assigned roles in the service

---

## 🔐 Example: Restricting Access to Integration Suite

| User Type     | User Group       | Role Collection              | Roles Inside                     |
|---------------|------------------|-------------------------------|---------------------s-------------|
| Developer     | `BTP_Dev`        | `Integration_Dev`             | `Integration_Developer`          |
| Viewer        | `BTP_Viewer`     | `Integration_ReadOnly`        | `Integration_Viewer`             |
| Admin         | `BTP_Admins`     | `Integration_Admin`           | `Integration_Provisioner`, `Admin` |

---f

## ✅ Best Practices

- 🎯 Use **Role Collections** for modular access control
- 👥 Prefer **IdP Group Mapping** over individual user assignment
- 🔄 Review access regularly
- 🧾 Document all role collections and assignments for audit/compliance

---

## 📚 Resources

- [SAP BTP Security Overview](https://help.sap.com/docs/btp/security)
- [SAP Integration Suite Roles](https://help.sap.com/docs/integration-suite)
- [XSUAA Role Management](https://help.sap.com/docs/xsuaa)

