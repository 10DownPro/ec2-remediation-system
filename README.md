# EC2 Remediation System (ServiceNow + AWS)

A scoped ServiceNow app that detects failed EC2 instances, alerts engineers, and enables one-click remediation via AWS REST API. Built to reduce downtime during large-scale outages and automate manual steps during incident response.

---

## Real-World Scenario: Netflix EC2 Outage

**Problem:**  
Imagine Netflix is experiencing a major EC2 instance failure in its streaming infrastructure—an edge server in us-west-2 goes dark. Viewers on the West Coast start reporting buffering issues, stream interruptions, and long load times.

In traditional workflows, Netflix’s DevOps engineers:
- Get pinged in Slack
- Manually dig through logs
- Search internal wikis for solutions
- SSH into the EC2 instance or use the AWS console to restart it

This process takes **10–15+ minutes**, leading to angry customers, revenue loss, and SLA violations.

---

## Business Need

Netflix needs a faster, centralized way to:
- Detect failed EC2 instances within seconds  
- Trigger instant Slack notifications  
- Recommend KBs via AI Search inside ServiceNow  
- Open an incident for audit/compliance tracking  
- Let engineers fix the issue in one click  
- Log the action for future review

---

## Solution Overview

This ServiceNow application delivers exactly that.

 **System Diagram:**  
Here's a high-level overview of the end-to-end process:  
![System Diagram](https://github.com/user-attachments/assets/c2a26958-089a-4f61-b052-8827b6b86207)

---

## How It Works

**Trigger:** AWS Integration Server pushes EC2 status to SNOW every 60 seconds.

**When status = OFF:**
1. Flow Designer initiates AI Search for remediation KBs  
2. Sends Slack alert to DevOps  
3. Creates a ServiceNow Incident  
4. Adds a “Trigger EC2 Remediation” button to the instance form  
5. Engineer clicks the button → REST call sent to AWS  
6. Action is logged in a custom Remediation Log table  

---

## Core System Components

### 1. EC2 Instance Table  
Stores instance metadata, region, AWS ID, and current health.  
<img width="790" height="374" alt="Screenshot 2025-09-13 at 12 43 56 AM" src="https://github.com/user-attachments/assets/2afe9097-20f7-42de-bf66-b9ce85503082" />

---

### 2. Remediation Log Table  
Audit log of all triggered remediation attempts for compliance & tracking.  
<img width="787" height="371" alt="Screenshot 2025-09-13 at 12 44 27 AM" src="https://github.com/user-attachments/assets/2aac69ee-4d34-46ce-9f04-3a97eb8e09e3" />


---

### 3. Script Include  
Contains logic to send restart request via REST to AWS Integration Server.  
![Script Include](https://github.com/user-attachments/assets/0855ce7a-47cb-42bb-96c1-486910df9a88)
![UI Action](https://github.com/user-attachments/assets/28ca1870-5d91-42f4-8d80-715104e375a3)

---

### 4. UI Action  
Adds a button to the EC2 Instance form in SNOW:  
**Trigger EC2 Remediation** 

<img width="1244" height="565" alt="Screenshot 2025-09-13 at 12 40 16 AM" src="https://github.com/user-attachments/assets/06bbd250-dd85-40dc-9b05-8e2bd6f03941" />
<img width="1190" height="565" alt="Screenshot 2025-09-13 at 12 40 41 AM" src="https://github.com/user-attachments/assets/1135bcdd-d660-4177-93bb-64447fa2de05"/>
<img width="784" height="245" alt="Screenshot 2025-09-13 at 12 41 17 AM" src="https://github.com/user-attachments/assets/6082d38e-74d6-48c8-ad24-3b9a397502c0" />
 

---

### 5. Flow Designer Logic  
Watches EC2 instance table for status changes → runs KB lookup, sends Slack, opens Incident.  
<img width="1021" height="551" alt="Screenshot 2025-09-13 at 12 35 20 AM" src="https://github.com/user-attachments/assets/e40531e2-438e-42a2-913b-22667e049738" />

---

### 6. AI Search + Knowledge Base  
Smart lookup of existing internal documentation (e.g., restart scripts, known issues).  
<img width="993" height="566" alt="Screenshot 2025-09-13 at 12 32 32 AM" src="https://github.com/user-attachments/assets/27b138ab-780d-4bca-a938-93b0aa240fd8" />

---

### 7. Studio App Packaging  
Scoped app includes all logic, fields, and APIs.  
<img width="793" height="384" alt="Screenshot 2025-09-13 at 12 45 39 AM" src="https://github.com/user-attachments/assets/2952cc9c-d0fa-426d-8ff1-6511e49c7079" />


