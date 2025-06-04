# 🛠️ SAP BTP Troubleshooting Guide: Service Instance Provisioning

This guide helps identify and resolve common issues encountered while provisioning service instances in SAP Business Technology Platform (BTP).

---

## 🧩 Common Issues and How to Fix Them

---

### ❌ 1. **"Missing Entitlement" Error**

**🔍 Description**: The selected service or plan is not entitled to the subaccount.

**✅ Resolution**:
- Go to **Global Account → Entitlements**
- Click **Entity Assignments → Select Subaccount**
- Click **Configure Entitlements**
- Add the required **service** and **plan**
- Click **Save** and retry provisioning

---

### ❌ 2. **"Quota Exceeded" or "Plan Limit Reached"**

**🔍 Description**: You’ve reached the limit of the service plan quota.

**✅ Resolution**:
- Review quotas under **Global Account → Entitlements**
- Remove unused service instances to free up quota
- Request additional quota from your BTP administrator

---

### ❌ 3. **"Region or Plan Not Available"**

**🔍 Description**: Some services or plans are not available in the selected region.

**✅ Resolution**:
- Check the **SAP BTP Regional Availability Matrix**: [Link](https://discovery-center.cloud.sap/resources)
- Change your **subaccount region** or choose a different plan

---

### ❌ 4. **"Insufficient Permissions"**

**🔍 Description**: You do not have rights to create service instances.

**✅ Resolution**:
- Ensure your user has required roles:
  - `Subaccount Administrator`
  - `Service Instance Creator`
- Go to **Subaccount → Security → Role Collections**
- Assign the required role collection to your user

---

### ❌ 5. **"Service Broker Error" or Internal Failure**

**🔍 Description**: Backend provisioning failed due to internal system error.

**✅ Resolution**:
- Retry the operation after a few minutes
- Check the **"Instances and Subscriptions"** section for failed instances
- Delete the failed instance if retry fails
- Check **Subaccount → Service Marketplace → Instance Details → Logs**

---

### ❌ 6. **"Service Not Found" in Marketplace**

**🔍 Description**: The service doesn’t appear in the marketplace.

**✅ Resolution**:
- Confirm that the service is **entitled** and **available in your region**
- Check if **Cloud Foundry is enabled** in the subaccount
- Refresh entitlements or recreate subaccount if persistent

---

### ❌ 7. **Booster Fails During Execution**

**🔍 Description**: Booster provisioning stops midway or throws error.

**✅ Resolution**:
- Check **Booster Logs** for specific failure point
- Make sure all preconditions (roles, entitlements, CF enabled) are met
- Run booster again after fixing the root cause
- Refer to SAP Discovery Center troubleshooting tips

---

## 🧪 Troubleshooting Tools

| Tool/Section                          | Purpose                               |
|--------------------------------------|----------------------------------------|
| **Subaccount → Instances & Subscriptions** | View and manage all service instances |
| **Service Marketplace Logs**         | Error details from service provisioning |
| **Entitlements Configuration**       | Add or verify service access           |
| **Activity Logs**                    | Track subaccount actions and failures |
| **Booster Logs**                     | Check execution status of boosters    |

---

## 📝 Best Practices for Avoiding Issues

- ✅ Always check **entitlements and quotas** before provisioning
- ✅ Use **supported regions** and plans
- ✅ Enable **Cloud Foundry** early if required by the service
- ✅ Assign necessary **roles and permissions**
- ✅ Use **Boosters** when available to reduce manual errors

---

## 📚 References

- [SAP BTP Documentation](https://help.sap.com/btp)
- [SAP Discovery Center](https://discovery-center.cloud.sap)
- [SAP BTP Troubleshooting FAQs](https://help.sap.com/docs/btp/troubleshooting)

---

## 💬 Need More Help?

- Use **SAP Community** for peer support
- Create a **support ticket** in the SAP ONE Support Launchpad
- Reach out to your **SAP Customer Engagement Executive (CEE)**

