# 🔧 SAP BTP: Setting Up Custom User Roles

This guide explains how to define and assign **custom user roles** in SAP BTP using **XSUAA (Authorization & Trust)** service and application-specific role templates.

---

## 🧱 Key Concepts

| Term             | Description                                                                 |
|------------------|-----------------------------------------------------------------------------|
| Role Template    | Defines a reusable role inside a security descriptor (e.g., `xs-security.json`) |
| Role             | A specific instance of a role assigned to a user                            |
| Role Collection  | A group of roles that can be assigned to users                              |
| XSUAA            | SAP service that handles authentication & authorization                    |

---

## ✏️ 1. Define Custom Roles in `xs-security.json`

Define your roles using a role template file in your project.

```json
{
  "xsappname": "my-app-name",
  "tenant-mode": "dedicated",
  "scopes": [
    {
      "name": "$XSAPPNAME.ReadData",
      "description": "Read access to data"
    },
    {
      "name": "$XSAPPNAME.ManageData",
      "description": "Manage access to data"
    }
  ],
  "role-templates": [
    {
      "name": "Viewer",
      "description": "Read-only access",
      "scope-references": [
        "$XSAPPNAME.ReadData"
      ]
    },
    {
      "name": "Admin",
      "description": "Full access",
      "scope-references": [
        "$XSAPPNAME.ReadData",
        "$XSAPPNAME.ManageData"
      ]
    }
  ]
}
```

> 📝 `$XSAPPNAME` is replaced by your actual app name during deployment.

---

## 🚀 2. Deploy `xs-security.json` to BTP

```bash
cf login
cf target -o <your-org> -s <your-space>
cf create-service xsuaa application xsuaa-myapp -c xs-security.json
```
> You can also use the `mta.yaml` descriptor to bind the XSUAA service to your app during `cf deploy`.

---

## 🧭 3. Create Role Collections in BTP Cockpit

1. Go to your **Subaccount → Security → Role Collections**
2. Click **Create Role Collection** (e.g., `MyApp_Admin`)
3. Add roles from your app (e.g., `my-app-name!t0.Admin`)
4. Save the collection

---

## 👤 4. Assign Role Collections to Users

- Go to **Subaccount → Security → Users**
- Click **Assign User**
- Select user email
- Assign relevant role collection (e.g., `MyApp_Admin`)

---

## 🌐 5. Optional: Map Role Collections to IdP Groups

- Go to **Subaccount → Trust Configuration**
- Select your IdP (e.g., Azure AD)
- Assign role collections to IdP groups (e.g., group `AppAdmins` → `MyApp_Admin`)

---

## 🔍 6. Verify Role Access in Your App

In your application logic, check for scopes using JWT or application framework (e.g., CAP, Node.js, Java).

```js
if (req.user.is("Admin")) {
  // show admin UI
}
```

```java
if (jwt.getClaim("scope").contains("my-app-name.ManageData")) {
  // allow data changes
}
```
---

## ✅ Summary

| Task                           | Tool / Location                |
|--------------------------------|--------------------------------|
| Define roles                   | `xs-security.json`             |
| Deploy security config         | `cf create-service xsuaa`      |
| Create role collections        | BTP Cockpit → Role Collections |
| Assign users or IdP groups     | BTP Cockpit → Users / Trust    |
| Use in app logic               | JWT claims or framework access |

---

## 📚 References

- [SAP XSUAA Documentation](https://help.sap.com/docs/xsuaa)
- [SAP BTP Role Collections](https://help.sap.com/docs/btp/role-collections)
- [CAP Authorization Guide](https://cap.cloud.sap/docs/advanced/authorization)

