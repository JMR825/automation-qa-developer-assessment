# Automation & QA Developer — Take-Home Assessment

**Candidate:** Janhavi Rathod  
**Assessment:** Automation & QA Developer  
**Repository:** `automation-qa-developer-assessment`

## Overview

This repository contains my submission for the Automation & QA Developer take-home assessment.

The assessment focuses on two primary areas:

1. **Web Application QA:** Testing a web application, identifying functional and usability issues, documenting bugs, and analysing potential root causes.
2. **Workflow Automation:** Building an n8n workflow that integrates third-party APIs, transforms data, applies conditional logic, sends notifications, and handles errors.

An optional uptime-monitoring workflow is included as an additional automation exercise.

---

## Project Structure

```text
automation-qa-developer-assessment/
│
├── Task1-QA-Report/
│   ├── Task1_QA_Report_Janhavi_Rathod.pdf
│   └── screenshots/
│
├── Task2-n8n-Workflow/
│   ├── Task2_Workflow_Janhavi_Rathod.json
│   ├── README.md
│   └── screenshots/
│       ├── workflow-canvas.png
│       └── successful-execution.png
│
├── Bonus-Uptime-Monitor/
│   ├── Bonus_UptimeMonitor_Janhavi_Rathod.json
│   └── screenshots/
│
└── README.md
```

---

# Task 1 — Web Application QA & Debug Report

**Application:** [RealWorld Demo](https://demo.realworld.show/)

### Objective

Evaluate a web application by testing its primary user flows, identifying potential defects, and documenting reproducible issues with expected and actual behaviour.

### Testing Areas

- User registration and form validation
- Login and authentication
- Account settings and password management
- Article creation and publication
- Article visibility and persistence
- Logout behaviour

### Identified Issues

| # | Issue | Area | Severity |
|---|---|---|---|
| 1 | Missing validation feedback for empty sign-up fields | Registration | Low |
| 2 | Password change may not require current-password verification | Account Security | Pending verification |
| 3 | Existing article publication dates appear to change after creating a new article | Article Management | Medium |
| 4 | User-created articles disappear after logout | Article Persistence | High |
| 5 | Additional verified issue | To be completed | To be determined |

### QA Approach

Each issue is documented with:

- Title and summary
- Affected module
- Preconditions
- Steps to reproduce
- Expected result
- Actual result
- Severity
- Suspected cause
- Verification status

A root-cause analysis is also included to distinguish observed behaviour from possible underlying implementation issues.

**Deliverable:** `Task1_QA_Report_Janhavi_Rathod.pdf`

---

# Task 2 — n8n API Integration Workflow

### Objective

Build an automated GitHub monitoring workflow that retrieves popular machine learning repositories, enriches repository information, applies conditional filtering, and delivers notifications through Discord.

### Technologies Used

- n8n
- GitHub REST API
- JavaScript
- Discord Webhooks

### Workflow Architecture

```text
Schedule Trigger
       |
       v
GitHub HTTP Request
       |
       v
Code Node
(Filter and Sort Top 5)
       |
       v
README HTTP Request
       |
       v
Merge Node
       |
       v
IF Node
(Stars > 1000?)
       |
       v
Discord Notification
```

### Implementation Details

**1. Schedule Trigger**

Initiates the workflow periodically. The hourly schedule is intended for testing and automated execution.

**2. GitHub API Integration**

Uses the GitHub repository search endpoint to retrieve machine learning repositories sorted by star count.

**3. Data Transformation**

A JavaScript Code node:

- Extracts repository information.
- Sorts repositories by star count.
- Selects the top five results.
- Retains the repository name, owner, description, stars, language, and URL.

**4. API Enrichment**

Makes a second GitHub API request to retrieve README content for the selected repositories.

**5. Data Merging**

Uses an n8n Merge node in Combine by Position mode to combine repository information with the corresponding README responses.

**6. Conditional Routing