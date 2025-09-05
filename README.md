# EC2 Remediation System (ServiceNow + AWS + Slack + AI Search)

## 📖 Project Story  
Last week, Netflix faced a critical issue: an AWS EC2 instance in the **US-East region** failed during peak streaming hours. The monitoring system wasn’t integrated with ServiceNow, so the outage went undetected for 45 minutes. That gap meant **millions of subscribers experienced buffering**, complaints poured in, and Twitter/X lit up with criticism.  

As a **ServiceNow Admin & Jr Developer at Netflix**, I was tasked with building a solution that DevOps could trust. The goal was clear:  
- Detect failing EC2 instances immediately.  
- Give engineers instant remediation guidance without hunting docs.  
- Notify teams in Slack where they live.  
- Enable **one-click remediation** directly from ServiceNow.  
- Keep a complete **audit log** for compliance & post-mortems.  

This project turned a painful incident into an opportunity to prove how ServiceNow, AWS, Slack, & AI could work together to protect streaming quality for over **260 million subscribers worldwide**.

---

## ⚙️ System Overview  
The **EC2 Remediation System** integrates AWS health monitoring, ServiceNow workflows, and Slack notifications to enable fast, semi-automated incident response.  

**Core Flow:**  
1. **AWS Integration Server** pushes EC2 instance health into ServiceNow every minute.  
2. If an instance flips to `OFF`, a **Flow Designer workflow** is triggered.  
3. The workflow:  
   - Runs **AI Search** to surface remediation runbooks.  
   - Sends a **Slack alert** to DevOps with KB links.  
   - Creates a **ServiceNow Incident**.  
4. DevOps can open the EC2 record & hit the **Trigger EC2 Remediation** button.  
5. The **Script Include** calls AWS Integration Server via REST API.  
6. All actions are logged in the **Remediation Log** for audit trails.

<img width="1239" height="589" alt="Screenshot 2025-09-04 at 9 59 04 PM" src="https://github.com/user-attachments/assets/3cf6ba12-bc28-45ad-a3cd-443d698e0f05" />


---

## 🏗️ Implementation Steps  
- Built a scoped app: **EC2 Monitoring and Remediation**  
- Created **two custom tables**: `EC2 Instance` & `Remediation Log`  
- Configured **Connection & Credential Store** (alias, HTTP connection, basic auth)  
- Developed a **Script Include** + **UI Action** for one-click remediation  
- Designed a **Flow Designer workflow**: OFF → AI Search → Slack webhook → Incident  
- Authored **Knowledge Base articles** (with EC2 keywords) for AI retrieval  
- Applied **ACLs** to secure access for DevOps & admins  
- Exported everything into an **update set** for version control  

---

## 🗺️ Architecture Diagram  
![Architecture Diagram](Diagram.png)  

*Flow: AWS EC2 → AWS Integration Server → ServiceNow EC2 Table → Flow Designer (AI Search + Slack + Incident) → DevOps remediation button → Script Include → AWS → Remediation Log*

---

## 🚀 DevOps Usage  
1. Watch Slack for EC2 OFF alerts & quick KB links.  
2. Open the linked Incident in ServiceNow.  
3. Navigate to the EC2 Instance record.  
4. Click **Trigger EC2 Remediation** → request sent to AWS Integration Server.  
5. Check **Remediation Log** for success/failure details & response time.  

---

## 📊 Optimization Highlights  
- **Force Save** in Flow Designer ensured every sub-artifact landed in the update set.  
- Moved API credentials to **Connection & Credential Store** for security.  
- Added **AI Search keywords** so KB retrieval was instant & relevant.  
- Slack messages included **instance ID, name, & KB links** for immediate triage.  

---

## ✅ Evidence & Testing  
- **EC2 Instance table** auto-populated with ON/OFF statuses  
- **Remediation Log entries** created after button clicks  
- **Incidents** auto-generated for OFF statuses  
- **AI Search logs** verified KB retrieval  
- **Slack notifications** successfully delivered (before webhook removed for repo security)  

---

## 🔑 Interview Spotlight  
This project demonstrates:  
- **End-to-end systems thinking**: tied AWS, ServiceNow, Slack, & AI Search into one flow.  
- **Business impact awareness**: solved a real problem that cost Netflix trust with users.  
- **Hands-on ServiceNow expertise**: custom tables, flows, UI actions, script includes, ACLs.  
- **Automation mindset**: reduced manual lookup/remediation time from 45 minutes to <5.  

---

## 📂 Repository Structure  

/ec2-remediation-system<br>
├── README.md<br>
├── ec2-remediation-system.xml # Update set export<br>
└── Diagram.png # System architecture diagram

---

## 📌 Takeaway  
This wasn’t just about fixing an outage. It was about **proving the value of automation** in protecting customer experience. With this system, Netflix’s DevOps team moved from **reactive firefighting** to **proactive, AI-assisted incident response**.  
