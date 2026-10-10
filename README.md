# 🔎 Lost & Found Item Resolution System

An intelligent **Lost & Found automation system** built using **UiPath Agents, Maestro, Action Apps, and RPA**.

The system automatically analyzes lost-item reports, compares them with recovered-item records, handles uncertain matches through human verification, and sends the final result to the owner by email.

---

## 📌 Overview

Managing lost-and-found items manually can be time-consuming, especially when there are many recovered items to compare.

This project automates the process using AI and workflow orchestration while keeping a **human-in-the-loop** for uncertain cases.

The system can classify a reported lost item into:

- ✅ **Likely Match**
- 👤 **Manual Verification**
- ❌ **No Match**

---

## 🚀 Workflow

```text
Lost Item Report
       ↓
Lost Item Analysis Agent
       ↓
Match & Context Grounding Agent
       ↓
    Match Status
   /      |       \
Likely   Manual   No Match
Match    Verify
  |        ↓         |
  |    Action App    |
  |        ↓         |
  └────────┼─────────┘
           ↓
Notification Generation Agent
           ↓
      Notification RPA
           ↓
      Owner Email
```

## 🤖 Components

1. Lost Item Analysis Agent

The first agent processes the lost-item report.
It takes information such as:
- Owner Name
- Email
- Lost Location
- Approximate Time
- Item Category
- Item Description
- Distinguishing Features
- Last Known Location
It organizes the information and identifies the important attributes that should be considered during matching.
This agent does not decide whether a match exists.

2. Match & Context Grounding Agent

This is the main matching component.
The agent compares the analyzed lost-item information with recovered-item records stored in an Excel dataset.
It considers:
- Item category
- Item description
- Distinguishing features
- Location
- Time
- Identification rules
- Overall contextual consistency
The agent produces one of three results:
Match Status	                  Meaning
------------------------------------------------------------------------------------------
Likely Match	                  Strong evidence supports the recovered item
Manual Verification	            A possible match exists, but human confirmation is needed
No Match	                      No plausible recovered item was identified


3. Recovered Items Dataset

Recovered-item information is stored in an Excel file and connected to the Agent through a UiPath Storage Bucket and Context Grounding Index.
The dataset contains fields such as:
- RecoveredID
- Location
- Timestamp
- ItemCategory
- ItemDescription
- DistinguishingFeatures
- IdentificationRules
- Status
Example:
RecoveredID: R002
Location: Cafeteria
ItemCategory: Phone
ItemDescription: Black Samsung smartphone
DistinguishingFeatures: Cracked screen; transparent case

4. Human Verification – Action App

When the AI identifies a possible but uncertain match, the case is sent to a UiPath Action App.
The reviewer can see:
- Owner information
- Lost item description
- Match status
- Recovered item ID
- Reason for the suggested match
- Recommended action
The reviewer can choose:
- ✅ Confirm Match
- ❌ Reject Match
- ℹ️ Request More Information
They can also add reviewer comments.
This provides a human-in-the-loop step instead of forcing the AI to make uncertain decisions automatically.
5. Notification Generation Agent
After the match decision is completed, the Notification Generation Agent creates a clear and professional notification for the owner.
The notification is generated according to the final outcome and available information.

6. Notification RPA

The final RPA workflow sends the generated notification to the owner's email.
It handles:
- Recipient email
- Owner name
- Lost item description
- Verification outcome
- Notification content
The email contains a formatted Lost & Found Resolution Update.
🎯 Example Scenarios
✅ Likely Match
Reported item:
- Black Samsung smartphone
- Cracked screen
- Transparent case
- Lost in the Cafeteria
The system identifies R002 as a strong match.
Result:
Match Status: Likely Match
Recovered ID: R002

No manual verification is required.
👤 Manual Verification
Reported item:
- Black smartphone
- Lost in the Cafeteria
- No distinctive features provided
The system identifies R002 as a plausible candidate, but there isn't enough distinctive evidence for an automatic match.
Result:
Match Status: Manual Verification
Recovered ID: R002

The case is sent to the Action App for human review.
❌ No Match
For example, if a user reports:
Blue over-ear wireless headphones
Lost at Main Gate

and no relevant recovered headphone record exists:
Match Status: No Match
Recovered ID: None

The case skips manual verification and proceeds to notification.

🛠️ Technologies Used
- UiPath Maestro – Workflow orchestration
- UiPath Agents – AI-based analysis, matching, and notification generation
- UiPath Context Grounding – Retrieval of relevant recovered-item records
- UiPath Storage Bucket – Recovered-item data storage
- Excel – Recovered-item dataset
- UiPath Action App – Human verification
- UiPath RPA – Automated email notification

🔄 Complete Process
* Step 1:
The user submits a lost-item report.
* Step 2:
The Lost Item Analysis Agent organizes and analyzes the report.
* Step 3:
The Match & Context Grounding Agent retrieves and compares relevant recovered-item records.
* Step 4:
The system determines:
Likely Match
     OR
Manual Verification
     OR
No Match

* Step 5:
If manual verification is required, the reviewer makes a decision through the Action App.
* Step 6:
The Notification Generation Agent creates the final notification.
* Step 7:
The Notification RPA sends the notification to the owner.

🌟 Key Features
- 🤖 AI-powered lost-item analysis
- 🔎 Context-based item matching
- 📊 Excel-based recovered-item database
- 🧠 Context Grounding for relevant record retrieval
- 👤 Human-in-the-loop verification
- 🔀 Automated decision routing
- 📧 Automated email notifications
- ⚙️ End-to-end workflow orchestration with Maestro

📂 Project Structure
```text
Lost & Found Item Resolution System
│
├── Lost Item Analysis Agent
├── Match & Context Grounding Agent
├── Notification Generation Agent
├── Lost & Found Verification Action App
├── Lost & Found Notification RPA
├── Maestro Process
└── Lost_and_Found_Recovered_Items.xlsx
```

🎓 Project Objective
The objective of this project is to demonstrate how AI agents, workflow orchestration, human verification, and RPA can work together to automate a practical real-world process.
Instead of completely replacing human decision-making, the system uses AI for repetitive analysis and matching while involving a human when the available evidence is uncertain.

👩‍💻 Project
Lost & Found Item Resolution System
Built using UiPath Automation Cloud and UiPath Maestro.
