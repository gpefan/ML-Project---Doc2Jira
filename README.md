# Final Project – Automated Jira Ticket Pipeline

## 📖 Project Description
This project implements an AI-driven pipeline that transforms project requirements (from `.docx` documents) into structured Jira tickets.  
The system leverages multiple LLM-powered agents to:
- Parse and review the document structure.
- Predict labels, priorities, and assignee groups.
- Optionally generate SQL subtasks (DDL + SELECT queries) and Assignee Groups.
- Visualize the Jira ticket hierarchy in a tree view.

The final outcome is a set of Jira issues automatically created through the Jira REST API.

---

## ⚙️ Instructions


### .env File

A .env file should be created in the same folder that the Final_Project.ipynb exists, with the following parameters.

Jira connection (required)
- JIRA_EMAIL=your_email@domain.com          # Your Jira account email
- JIRA_API_TOKEN=your_api_token             # API token from Atlassian account
- JIRA_BASE_URL=https://yourcompany.atlassian.net  # Jira base URL
- JIRA_PROJECT_KEY=ABC                      # Target Jira project key

OPEN AI API Key (required)
- OPENAI_API_KEY                            # Your OPEN AI API Key

Custom fields (optional)
- JIRA_FIELD_ASSIGNED_GROUP=customfield_10124  # Jira custom field for "Assigned Group". It is a custom field in Jira that should be created for all tickets (Epic, Task, Subtask) named "Assigned Group". By clicking on inspect, you can find customfield_... of the field and add it to the .env file

An example of the .env file is given in the "env parameters.txt" file.

---

### Input Files

Document (.docx):
Provide your requirements document in Word format. Example: "Technical_Document_01.docx".

Database Schema (.txt):
Provide the database schema in plain text. Example: "Database_Schema.txt".
This is only required if you want to generate SQL subtasks (include_sql=True).

---

### Jira Setup

1. Create an API Token for Atlassian Cloud (Jira Cloud) - https://id.atlassian.com/manage-profile/security/api-tokens
2. Create a Jira workspace (free plan) - https://www.atlassian.com/try/cloud/signup (keep your url in order to add it to corresponding .env parameter)
3. Create a Project (recommended: Kanban) and keep the Project Key in order to add it to the corresponding .env parameter)
4. When creating your Project, Epic, Task and Subtask should included in the Work Types
5. Click on Project Settings and then on Work Types. For all work types, Epic, Task and Subtask, add the field Priority from the right side (System fields) to the left side (Description fields)

(Optional) Addition of "Assigned Group" field
1. In Jira Admin Settings, move to Fields area on the left
2. Click on the Create new field at the top right corner
3. Select Field type = "Group Picker (signle groups)" and Name = "Assigned Group"
4. Then click on Actions and select "Add field to screen"
5. Select all Screens, except the Workflow Screens, and click on Update
6. Move to Project Settings and click on Field at the left side
7. Click on "Add field" at the top right corner and add the "Assigned Group" field
8. For every Work Type, Epic, Task and Subtask, add the field "Assigned Group" from the right side (People and groups fields) to the left bottom side (Context fields)
9. Click on the Project, the move to the "List". Find the "Assigned Group" field, right click on the field, select inspect and search for "customfield_...". Add this text to the corresponding .env parameter
10. Click on Settings and select User Management. Then click on Groups and create the following groups

        - Business Analysis Team
        - Business Intelligence Team
        - Configuration Engineer Team
        - Data Warehouse Team
        - Project Management Office (PMO)
        - Quality Assurance Team

If you don't want to create these groups and you want others, you should also change the parameter "groups_list" in the Final_Project.ipynb in order to include them there also.

---

### Running the pipeline

Near the end of the Final_Project.ipynb, there are two parameters, "doc_path" that should contain your docx path and "schema_text" that should contain you database schema (txt file).

The final Pipeline (run_pipeline), contains four parameter:
- doc_path
- schema_text (None if you do not want to include SQL and Database read)
- include_sql (True or False)
- include_assignee_group (True or False)

---

After successfully installing the required libraries from requirements.txt, setting up your Jira account and project, and creating a .env file with the necessary parameters, you can run the run_pipeline function in Final_Project.ipynb.

You may use the provided example files:
- Technical_Document_01.docx (sample technical document)
- Database_Schema.txt (sample database schema)

Alternatively, you can create and use your own documents and schema.
