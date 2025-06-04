# 🧑‍💻 Guide: Provisioning Dev Spaces for Custom Implementation in SAP BTP

This guide explains how to create Dev Spaces in **SAP Business Application Studio (BAS)** and connect them to your BTP subaccount for building custom applications and extensions.

---

## 📌 Prerequisites

- An active **SAP BTP subaccount** with **Business Application Studio** entitlement assigned
- A **Cloud Foundry** environment enabled in the subaccount
- Your user must have appropriate roles (e.g., `Business_Application_Studio_Developer`)

---

## 🧭 Step-by-Step Guide

### 🔹 1. Assign Entitlements

1. Log in to [SAP BTP Cockpit](https://account.hana.ondemand.com)
2. Go to **Global Account** → **Entitlements**
3. Click **Entity Assignments** → select your **subaccount**
4. Click **Configure Entitlements**
5. Click **Add Service Plans**
6. Search for **Business Application Studio** and select the `standard` or `trial` plan
7. Click **Add** → **Save**

---

### 🔹 2. Enable Business Application Studio

1. Navigate to your **Subaccount**
2. Go to **Service Marketplace**
3. Search for **Business Application Studio**
4. Click the tile and choose **Create Instance**
   - Plan: `standard`
   - Instance name: e.g., `bas-instance`
   - Leave other configurations as default
5. Click **Create**

---

### 🔹 3. Open Business Application Studio

1. Once the instance is created, click **Go to Application**
2. You will be redirected to the **BAS Web IDE** environment
3. If prompted, authorize your access

---

### 🔹 4. Create a New Dev Space

1. In BAS, go to the **Welcome Page**
2. Click **Create Dev Space**
3. Enter:
   - **Name**: `custom-devspace`
   - **Type**: Choose the type depending on your development:
     - **SAP Fiori** – for UI5/Fiori apps
     - **Full Stack Cloud Application** – for CAP/Node.js apps
     - **SAP HANA Native** – for HANA-based apps
4. Optionally, enable **extensions** such as:
   - MTA Tools
   - CF Tools
   - UI5 Tools
5. Click **Create Dev Space**

> 🕐 It may take a few minutes to provision.

---

### 🔹 5. Connect to Cloud Foundry Subaccount

1. Open the dev space once it's ready
2. In the terminal, log in to Cloud Foundry:
```bash
   cf login
```
Enter the API endpoint (e.g., https://api.cf.eu10.hana.ondemand.com)

Provide your SAP BTP credentials

Target your org and space:

```bash
cf target -o <org-name> -s <space-name>
```

---

## ✅ Now You’re Ready to Build!
### You can now:

- Scaffold projects using wizards

- Deploy apps to Cloud Foundry

- Bind services like XSUAA, Destination, and HANA Cloud

## 📚 Tips
- Use Application Wizard for Fiori and CAP templates.

- Configure .env files for local testing.

- Use Cloud MTA Build Tool (mbt) for building deployable archives.

## 🧩 Troubleshooting
- Issue	Solution
- Dev Space stuck in "Starting"	Restart or delete and recreate
- CF Login fails	Check API endpoint and user role
- Services not visible	Ensure entitlements are assigned and instance created

## 📘 References
- SAP Business Application Studio Help

- SAP Discovery Center

- Cloud Foundry CLI