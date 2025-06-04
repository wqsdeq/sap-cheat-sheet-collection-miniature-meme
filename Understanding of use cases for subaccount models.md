# 📘 SAP BTP Subaccount Models: Use Cases & Examples

SAP BTP allows you to structure your landscape using different **subaccount models** based on business and technical needs. Choosing the right model impacts maintainability, security, and governance.

---

## 🔹 1. **Subaccount Model by Landscape**

### ✅ Use Case:
Separate environments for **Development**, **Testing**, and **Production**.

### 📌 Description:
Each subaccount represents a stage in the software lifecycle. Useful for CI/CD pipelines and controlled transport.

### 📍 Example:
- `dev-subaccount` – Developers test features
- `test-subaccount` – QA runs regression tests
- `prod-subaccount` – Hosts the live application

### 👍 Best For:
- Projects with multiple lifecycle stages
- Teams requiring environment isolation

---

## 🔹 2. **Subaccount Model by Project or Application**

### ✅ Use Case:
One subaccount per **business application** or **project**.

### 📌 Description:
Each application or solution has its own isolated environment, including services and security settings.

### 📍 Example:
- `sales-portal-subaccount`
- `supplier-onboarding-subaccount`

### 👍 Best For:
- Large organizations with many apps
- Independent teams working on separate solutions

---

## 🔹 3. **Subaccount Model by Region**

### ✅ Use Case:
Deploy applications closer to users for **performance or legal compliance**.

### 📌 Description:
Subaccounts are created based on geographic locations or data residency requirements.

### 📍 Example:
- `us-west-subaccount` – for North America
- `eu-central-subaccount` – for EU customers

### 👍 Best For:
- Global businesses
- GDPR, data localization needs

---

## 🔹 4. **Subaccount Model by Business Unit or Department**

### ✅ Use Case:
Different **departments** or **divisions** operate independently in BTP.

### 📌 Description:
Each business unit gets its own subaccount to manage budgets, resources, and apps.

### 📍 Example:
- `hr-subaccount` – for employee apps
- `finance-subaccount` – for accounting tools

### 👍 Best For:
- Decentralized IT governance
- Cross-departmental projects

---

## 🔹 5. **Subaccount Model by Service Usage**

### ✅ Use Case:
Separation based on **service type** or **runtime environment**.

### 📌 Description:
Group services (like Integration Suite, HANA Cloud) into dedicated subaccounts to simplify quota and billing tracking.

### 📍 Example:
- `integration-subaccount` – for SAP Integration Suite
- `data-subaccount` – for HANA Cloud and Data Intelligence

### 👍 Best For:
- Simplified service management
- Clear cost allocation

---

## 📌 Summary Table

| Model Type           | Best Use Case                              | Example Subaccounts                |
|----------------------|---------------------------------------------|------------------------------------|
| By Landscape         | Dev/Test/Prod isolation                    | `dev-subaccount`, `prod-subaccount` |
| By Project           | Isolated environments per app              | `sales-app-subaccount`             |
| By Region            | Geo-specific deployments                   | `us-east-subaccount`               |
| By Business Unit     | Independent department usage               | `hr-subaccount`, `it-subaccount`   |
| By Service           | Manage services and costs cleanly          | `integration-subaccount`           |

---

## 📚 Tips for Choosing a Model

- **Combine models** if needed (e.g., Project + Landscape)
- Use **Directories** to group related subaccounts
- Align with your **security**, **cost tracking**, and **governance** needs

