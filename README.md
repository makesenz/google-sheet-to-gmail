# Student Course Report Automation using n8n

## 📌 Project Overview

This project automates the process of sending individual student course performance reports through email using **n8n**, Google Sheets, and Gmail.

The workflow retrieves student details from Google Sheets, formats the information into a branded HTML email using JavaScript, and sends each student their own personalized course report.

## 🎯 Objectives

- Automate student report generation and email delivery.
- Retrieve student information from Google Sheets.
- Generate professional HTML emails with makeSenz branding.
- Send a separate report to each student's email address.
- Skip empty spreadsheet rows and invalid email entries.

## 🛠️ Technologies Used

- **n8n** — Workflow automation
- **Google Sheets** — Student data source
- **JavaScript** — Data processing and HTML email generation
- **Gmail** — Email delivery
- **HTML & CSS** — Email formatting and styling

## 🔄 Workflow Architecture

1. **Manual Trigger** — Starts the workflow when executed manually.
2. **Google Sheets: Get Row(s)** — Retrieves student records from the spreadsheet.
3. **Format Email (Code node)** — Processes each student record and generates a personalized HTML email.
4. **Gmail: Send Message** — Sends the report to the corresponding student's email address.

```text
Manual Trigger
      ↓
Google Sheets — Get Row(s)
      ↓
Format Email — JavaScript
      ↓
Gmail — Send Message
```

## 📊 Google Sheets Data Structure

The Google Sheet contains the following columns:

| Column | Description |
|---|---|
| `name` | Student's name |
| `course` | Course name |
| `course score` | Student's score |
| `status` | Course result, such as Passed or Failed |
| `email` | Student's email address |

### Sample Data

| Name | Course | Score | Status |
|---|---|---:|---|
| Zahir | English | 77 | Passed |
| Arun | Python | 85 | Passed |
| Priya | AI | 42 | Failed |

*The email column contains each student's individual email address.*

## ✉️ Email Features

Each student receives a separate email containing:

- Student name and course details
- Course score and result status
- makeSenz logo and green brand styling
- A personalized greeting
- An encouraging learning message
- The signature **Regards, Team makeSenz**

The workflow skips empty rows and records without a valid-looking email address.

## ⚙️ Setup Instructions

### 1. Prepare Google Sheets

Create a Google Sheet with the required columns:

`name`, `course`, `course score`, `status`, `email`

Add the student records and ensure each student's email address is correct.

### 2. Configure Google Sheets Credentials

In n8n, create or select Google Sheets credentials and connect the spreadsheet to the **Get Row(s)** node.

### 3. Configure the Code Node

Add a Code node named **Format Email** and select:

**Mode:** Run Once for All Items

Paste the JavaScript code that generates the personalized HTML emails.

### 4. Configure Gmail

Connect your Gmail account using the supported OAuth credential setup.

Configure the Gmail **Send Message** node as follows:

| Field | Value |
|---|---|
| To | `{{ $json.to }}` |
| Subject | `{{ $json.subject }}` |
| Email Type | HTML |
| Message | `{{ $json.message }}` |

### 5. Connect and Execute

Connect the nodes in the workflow order shown above. Execute the Code node first and verify the generated recipients and email content. Then execute the complete workflow to send the reports.

**Important:** The Gmail node sends real emails. Verify all recipient addresses before running the workflow.

## ✅ Expected Output

For three valid student records, the Code node generates three separate email items. The Gmail node then sends an individual course report to each corresponding student.

Each email displays that student's own name, course, score, and result.

## 🚀 Future Improvements

- Add a Schedule Trigger for automatic report delivery.
- Add email validation and error handling.
- Track email delivery results in Google Sheets.
- Generate PDF reports for students.
- Add workflow notifications and execution logging.

## 📁 Repository Contents

Suggested GitHub repository structure:

```text
assignment-9-student-report-automation/
├── README.md
├── assignment9-workflow.json
└── screenshots/
    └── workflow-overview.png
```

- `README.md` — Project documentation
- `assignment9-workflow.json` — Exported n8n workflow
- `screenshots/` — Workflow screenshots for documentation

Export your actual workflow from n8n and save it as `assignment9-workflow.json` before uploading it to GitHub.

## 👨‍💻 Project Information

**Project:** Assignment 9 — Student Course Report Automation  
**Platform:** n8n  
**Branding:** makeSenz  
**Purpose:** Automated, personalized student course report delivery

---

*Built with n8n to simplify student report generation and email communication.*
