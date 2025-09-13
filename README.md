# ⚙️ EC2 Remediation System (ServiceNow + AWS)

A scoped ServiceNow app that monitors EC2 instance health, automates incident response, and enables one-click remediation via AWS REST API. Designed to cut down on manual steps, reduce downtime, and streamline DevOps workflows.

---

## 🧠 Why This Matters

Manual cloud remediation wastes time. This app automates the entire response process—detect, alert, remediate—while logging every action for audit & compliance. It's fast, secure, and extendable.

---

## 🔧 How It Works

**Heartbeat:** AWS Integration Server polls EC2 instance status & pushes data to ServiceNow every 60 seconds.

**When instance is `OFF`:**
1. Flow triggers AI Search for KB recommendations
2. Slack alert sent to DevOps team
3. ServiceNow Incident is auto-created
4. Dev clicks “Trigger EC2 Remediation” button
5. Script Include sends remediation command to AWS
6. Action is recorded in the Remediation Log table

---

## 🧱 Core System Components

### 1. EC2 Instance Table  
Tracks instance name, status, region, instance ID, and last check timestamp.

![EC2 Instance Table](https://github.com/user-attachments/assets/b3b59d16-ec19-424f-a18a-c94d0d2e1b77)

---

### 2. Remediation Log Table  
Captures details of every remediation event (who triggered it, when, for which instance).

![Remediation Log Table](https://github.com/user-attachments/assets/3ab49854-7b9a-4f25-b856-44b25e2374bc)

---

### 3. Script Include  
Core logic that forms & sends REST requests to the AWS integration endpoint.

![Script Include](https://github.com/user-attachments/assets/0855ce7a-47cb-42bb-96c1-486910df9a88)
![Script Include](https://github.com/user-attachments/assets/28ca1870-5d91-42f4-8d80-715104e375a3)

---

### 4. UI Action  
“Trigger EC2 Remediation” button on the instance record form.

<img width="1233" height="559" alt="Screenshot 2025-09-13 at 12 14 53 AM" src="https://github.com/user-attachments/assets/c8fbddda-44c4-4354-965f-f17ee07b037b" />
<img width="1236" height="576" alt="Screenshot 2025-09-13 at 12 15 48 AM" src="https://github.com/user-attachments/assets/3409ff02-2cce-4e24-a63f-41b63f0a905c" />
<img width="790" height="250" alt="Screenshot 2025-09-13 at 12 21 42 AM" src="https://github.com/user-attachments/assets/dc3d8e37-ff34-4ae1-83d9-7aeda6a42d02" />



---

### 5. Flow Designer  
Orchestrates the detection → alerting → ticket creation process.

<img width="1234" height="571" alt="Screenshot 2025-09-13 at 12 17 49 AM" src="https://github.com/user-attachments/assets/2ccf12ff-b590-49a3-8721-41c86ab67aec" />
<img width="985" height="537" alt="Screenshot 2025-09-13 at 12 18 37 AM" src="https://github.com/user-attachments/assets/08d4972d-fd05-4d85-a611-56ff934ee869" />



---

### 6. AI Search + KB Integration  
AI Search uses keywords & tags to fetch relevant KBs for the error type.

<img width="984" height="571" alt="Screenshot 2025-09-13 at 12 20 54 AM" src="https://github.com/user-attachments/assets/2add6c35-76ec-466b-bf64-92f6be29507a" />


---

### 7. Scoped App in Studio  
All logic is packaged in a scoped app for portability, testing, and future upgrades.

<img width="795" height="383" alt="Screenshot 2025-09-13 at 12 22 27 AM" src="https://github.com/user-attachments/assets/9bc36b00-5e1b-4123-820e-95e96d63dc5a" />

---

### Workflow Diagram

Here’s the full workflow at a glance:

<img width="810" height="505" alt="Screenshot 2025-09-13 at 12 25 25 AM" src="https://github.com/user-attachments/assets/c2a26958-089a-4f61-b052-8827b6b86207" />
