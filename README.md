# Final Project – Automated Jira Ticket Pipeline

## 📖 Project Description
This project implements an AI-driven pipeline that transforms project requirements (from `.docx` documents) into structured Jira tickets.  
The system leverages multiple LLM-powered agents to:
- Parse and review the document structure.
- Predict labels, priorities, and assignee groups.
- Optionally generate SQL subtasks (DDL + SELECT queries).
- Visualize the Jira ticket hierarchy in a tree view.

The final outcome is a set of Jira issues automatically created through the Jira REST API.

---

## ⚙️ Instructions
A .env file should be created in the same folder that the Final_Project.ipynb exists, with the following parameters.

--- Jira connection (required) ---
- JIRA_EMAIL=your_email@domain.com          # Your Jira account email
- JIRA_API_TOKEN=your_api_token             # API token from Atlassian account
- JIRA_BASE_URL=https://yourcompany.atlassian.net  # Jira base URL
- JIRA_PROJECT_KEY=ABC                      # Target Jira project key
- JIRA_FIELD_ASSIGNED_GROUP=customfield_10124  # Jira custom field for "Assigned Group". It is a custom field in Jira that should be created for all tickets (Epic, Task, Subtask) named "Assigned Group". By clicking on #inspect, you can find customfield_... of the field and add it to the .env file

--- OPEN AI API Key (required) ---
- OPENAI_API_KEY                            # Your OPEN AI API Key

--- Custom fields (optional) ---
- JIRA_EPIC_NAME_FIELD=customfield_10011       # Custom field for Epic Name (if required in your Jira)
- JIRA_EPIC_LINK_FIELD=customfield_10014       # Custom field for Epic Link (if required in your Jira)

--- Epic / Task handling options ---
- TEAM_MANAGED_EPIC_PARENT=false    # Set to true if using Team-managed project where Epics behave differently
