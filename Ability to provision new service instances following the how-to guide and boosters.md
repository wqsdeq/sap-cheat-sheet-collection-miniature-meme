# 🆕 SAP BTP Guide: Provisioning New Service Instances with How-To Guides and Boosters

This guide walks you through creating new service instances in SAP Business Technology Platform (BTP) using the Cockpit, How-To guides, and Boosters for accelerated setup.

---

## 🔹 What is a Service Instance?

A **service instance** is a provisioned and configured copy of a BTP service (e.g., SAP HANA Cloud, Integration Suite). It enables your applications to consume service capabilities like databases, integration, authentication, etc.

---

## 🧭 Step-by-Step Guide to Provision a New Service Instance

### Prerequisites:
- Access to SAP BTP Cockpit with relevant permissions
- A subaccount with assigned entitlements for the target service

---

## 1. **Access Your Subaccount**

- Log in to the [SAP BTP Cockpit](https://account.hana.ondemand.com).
- Navigate to your **Global Account** → **Subaccount** where you want to create the instance.

---

## 2. **Navigate to the Service Marketplace**

- Inside the subaccount, locate and click **Service Marketplace**.
- The marketplace lists all available services for which you have entitlements.

---

## 3. **Find and Select Your Service**

- Use the search bar or browse categories to find your desired service (e.g., **SAP HANA Cloud**, **Integration Suite**).
- Click on the service tile to open the service details.

---

## 4. **Create a New Service Instance**

- Click **Create Instance** or **New Instance** button.
- Fill in the required parameters:
  - **Service Plan**: Choose the plan (e.g., `standard`, `trial`, `lite`)
  - **Instance Name**: Provide a unique name for your instance
  - **Parameters**: Configure parameters (size, region, etc.) as needed
- Confirm and submit to provision the instance.

---

## 5. **Bind the Service Instance to an Application (Optional)**

- After instance creation, you can **bind** it to your deployed app.
- Go to your app → **Bindings** → **Create Binding**.
- Select the service instance and complete binding.

---

## 6. **Use Boosters for Faster Setup (If Available)**

### What are Boosters?
Boosters are guided wizards in the **SAP Launchpad / Discovery Center** that help automate complex setup tasks, including service provisioning, configuration, and sample app deployment.

### How to Use Boosters:
- Visit [SAP Discovery Center](https://discovery-center.cloud.sap).
- Search for boosters related to your service (e.g., "Integration Suite Booster").
- Follow the step-by-step guided flow:
  - Select your subaccount and region.
  - Configure service instances.
  - Deploy starter applications or artifacts.
- Boosters simplify best practices and automate multiple setup steps.

---

## ⚠️ Important Notes

- Make sure your subaccount has **entitlements** assigned for the service plan you want.
- Provisioning time varies by service; some instances may take several minutes.
- Check quotas and available resources before provisioning.
- Use boosters for best-practice configurations and quick starts.

---

## 📚 Additional Resources

- [SAP BTP Service Marketplace Documentation](https://help.sap.com/docs/btp/service-marketplace)
- [SAP Discovery Center & Boosters](https://discovery-center.cloud.sap)
- [SAP Integration Suite Provisioning Guide](https://help.sap.com/integration-suite)

---

## Summary

| Step                     | Action                                |
|--------------------------|-------------------------------------|
| 1. Access Subaccount      | Log in and select your subaccount   |
| 2. Open Service Marketplace | Find your target service          |
| 3. Create Service Instance| Choose plan, configure, and create  |
| 4. Bind to App (Optional) | Connect instance to your app        |
| 5. Use Boosters           | Leverage guided wizards for quick setup |

---

If you want, I can also prepare a checklist or visuals to complement this guide!
