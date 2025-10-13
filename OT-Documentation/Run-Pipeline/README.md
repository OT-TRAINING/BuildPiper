<img width="1280" height="720" alt="image" src="https://github.com/user-attachments/assets/2668b795-fc03-49d7-ab17-a53ba3b4e1eb" />

#  Buildpiper Pipeline Execution Guide

##  Overview

This document explains how to **create, configure, and execute** a pipeline in Buildpiper for automated CI/CD workflows.

---

## Prerequisites

* Access to Buildpiper application portal
* Permissions to create and execute pipelines
* Configured environments, services, and job templates
* Access to Git repository

---

##  Pipeline Workflow (End-to-End)

```
1. Add Pipeline  
2. Configure Basic Info  
3. Add Stages / Upload YAML  
4. Save Workflow  
5. Run with Parameters  
6. Monitor Execution  
7. Approve Stages (if required)  
8. Review Results
```

---

##  Step 1: Add New Pipeline

1. Navigate: **Application → Select Project → Pipeline Overview**
2. Click **+ ADD PIPELINE** → Opens “Setup Pipeline” page.
---
<img width="1366" height="658" alt="Screenshot from 2025-10-13 17-05-08" src="https://github.com/user-attachments/assets/7ab50992-9d04-448f-b978-73c1f03a157c" />


##  Step 2: Configure Basic Information

| **Field** | **Meaning** | **Description** | **Recommended** |
|------------|--------------|-----------------|-----------------|
| **Pipeline Name** | The unique identifier of your pipeline. | Used to distinguish between multiple pipelines (e.g., `demo-deploy`, `prod-pipeline`). Naming should reflect the environment or purpose. | Use clear, descriptive names (e.g., `app1-prod-deploy`). |
| **Version** | Defines the version of the pipeline configuration format or syntax. | Versioning ensures backward compatibility and helps maintain consistency with CI/CD platform updates. | Choose **Version 2** (latest stable format). |
| **Retention Count** | Determines how many past pipeline runs are stored in history. | Old runs are automatically deleted beyond this number, freeing up space and reducing clutter. | Keep **10–50 runs** based on frequency and audit needs. |
| **Pipeline Execution Via** | Specifies how the pipeline can be triggered. | Options include: `Run with Parameters`, `Run with Release Package`, or both. This defines whether manual input or predefined package triggers are allowed. | Select **Both** to support flexibility for both manual and automated runs. |
| **Trigger Type** | Defines what initiates the pipeline execution. | Common triggers include: **Manual** (human-triggered), **Schedule** (cron job), **SCM Poll** (source code change), or **Webhook** (external event). | Use **Manual** for controlled deployments (especially production). |
| **Production Hotfix** | Indicates whether this pipeline is used for urgent fixes in production. | Helps track and categorize high-priority emergency releases or patches. | Set to **No**, unless this is a designated hotfix pipeline. |
| **JIRA Reference Required** | Determines if the pipeline must be linked to a JIRA ticket. | Useful for organizations with strict change management and audit trails. | Set to **No** for non-audit or internal pipelines; **Yes** if under compliance control. |
| **Multi-Service Pipeline** | Enables deployment for multiple microservices in a single execution. | Allows bundling multiple related services or components together to deploy in one go. | Enable **Yes** if your application consists of multiple microservices. |
| **Select Tag During Execution** | Allows users to select an artifact or image tag at runtime. | Useful for controlled rollouts or choosing between versions without code changes. | Mark as **Optional** — use when manual tag control is required. |
| **Tags** | Metadata or keywords used for filtering and searching pipelines. | Helps organize and categorize pipelines in large environments (e.g., `production`, `testing`, `frontend`). | Add tags if needed for better discoverability. |
| **Pipeline Variables** | Dynamic key-value pairs used across pipeline steps. | Useful for managing environment details like namespaces, regions, image names, and configurations. | Define clearly: e.g., `ENV=dev`, `NAMESPACE=demo`, `REGION=us-east1`. |

<img width="1363" height="656" alt="image" src="https://github.com/user-attachments/assets/4563db67-8a30-4030-a93f-3883f1507f53" />
<img width="1363" height="656" alt="image" src="https://github.com/user-attachments/assets/3a4af927-5c76-4090-a641-4df9a9a723db" />

### - Once filled, it auto-saves and moves to Workflow Editor.
### - Click on the Pipeline name you created, It will open Workflow Editor


<img width="1357" height="627" alt="Screenshot from 2025-10-13 17-11-28" src="https://github.com/user-attachments/assets/0da73d9c-06a8-44e3-a4a6-8c9117fbb670" />

---

##  Step 3: Add Stages

In the **Workflow Editor**:

1. Click **ADD NEW STAGE**
2. Set:

   ### **Stage Name:** e.g., Build, Deploy, Test
   
   <img width="1363" height="656" alt="image" src="https://github.com/user-attachments/assets/4a526e49-6203-4b22-ba69-1dd30cd6347c" />
   
   ### **Approval Required:** Yes/No
   
   <img width="1363" height="656" alt="image" src="https://github.com/user-attachments/assets/5e854378-8ee6-4c04-8226-8e116314af70" />
   
4. Stage Approval Configurations


| **Field**                                            | **Meaning**                                                  | **Purpose / Description**                                                                                                                                                     | **Recommended Action**                                                                            |
| ---------------------------------------------------- | ------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------- |
| **Any questions before approval?**                   | Optional prompt for additional clarification from approvers. | Allows you to set a question or note that approvers must review before granting approval. Example: “Has QA testing been validated?” or “Is rollback plan documented?”         | Keep **No** if unnecessary, or enable **Yes** with clear, short questions to avoid confusion.     |
| **Do you want to push approver name to JIRA?**       | Sync approval data with JIRA ticketing system.               | When enabled, the name of the person who approved the stage is automatically updated in the linked JIRA ticket, ensuring traceability for change management and audit.        | Enable **Yes** for production or audit-heavy environments where approvals must be logged in JIRA. |
| **Do you want to push approver name to ServiceNow?** | Sync approval data with ServiceNow change records.           | Similar to JIRA integration — when turned on, the approver’s name is pushed to ServiceNow change request, ensuring compliance and visibility for CAB (Change Advisory Board). | Enable **Yes** for enterprises using **ServiceNow** for ITSM/change management; otherwise **No**. |


---

##  Step 4: YAML Configuration (Optional)

You can define the pipeline using YAML instead of the visual editor.

**Example:**

```yaml
stages:
  - stage1:
      name: "Build Stage"
      jobs:
        - job_1: { type: Build, environment: dev, template: build-template }
        - job_2: { type: Deploy, environment: dev, template: deploy-template }
  - stage2:
      name: "Promote Stage"
      jobs:
        - job_1: { type: Promote, from_env: dev, to_env: qa }
```

Upload via **YAML tab → Upload YAML → Save Workflow.**

---

## Step 5: Save Workflow

Click **Save Workflow** (top-right).
Confirmation: “ Pipeline created successfully.”
Pipeline now visible under **Pipeline Overview**.

---

##  Step 6: Run Pipeline with Parameters

1. Go to **Pipeline Overview → RUN WITH PARAMETERS**
2. Fill required details:

| Field              | Purpose                                               |
| ------------------ | ----------------------------------------------------- |
| **Services**       | Select one/multiple services                          |
| **Branch**         | e.g., `main`, `develop`, `feature/...`                |
| **Artifact Tag**   | Unique build identifier (`v1.0.0`, `release-2025-10`) |
| **Deploy Version** | Deployment label (optional)                           |

**Optional Toggles:**

* **UAT Required:** Pause for approval
* **Link JIRA Issues:** Attach tickets
* **Advanced Config:** Override variables or parameters

Click **Run Pipeline** to execute.
<img width="1366" height="653" alt="Screenshot from 2025-10-13 16-31-50" src="https://github.com/user-attachments/assets/a85139fd-7f78-44d5-9679-e1dce6d04699" />

---
## Step 7 : Pending for Approval 

* It will show the Pending for Approval , When we click on the pipeline we created ( e.g Demo 1 , k-demo etc ) there will be one window that will open. Then you have to click on Thumbs up icon for Approval. Then add Comment for same 
---
### 1. <img width="1366" height="652" alt="Screenshot from 2025-10-13 16-33-31" src="https://github.com/user-attachments/assets/ce7ea813-4f2a-441e-9aae-961b7233614c" />
---
### 2. <img width="1366" height="648" alt="Screenshot from 2025-10-13 16-33-52" src="https://github.com/user-attachments/assets/4bac1a7e-b5e9-4be8-9d9d-87b0769fb6c5" />
---
### 3. <img width="1359" height="653" alt="Screenshot from 2025-10-13 16-34-07" src="https://github.com/user-attachments/assets/53f5c182-56d3-40a8-aa4b-31475684a747" />


##  Step 8: Monitor Execution

* View live status: **Running, Success, Failed, Pending**
* Each stage shows job count, duration, and logs.
* Click **VIEW LOGS** to inspect build or deploy details.

---
<img width="1359" height="653" alt="Screenshot from 2025-10-13 16-34-32" src="https://github.com/user-attachments/assets/44ca7a44-5da4-4e16-9360-2d8ff23e8776" />
---

**Indicators:**

| Color/Icon | Status  |
| ---------- | ------- |
| 🟢 Green   | Success |
| 🔴 Red     | Failed  |
| 🟡 Yellow  | Running |
| ⚪ Gray     | Pending |

---

##  Best Practices

### Configuration

* Use clear names and tags
* Define key variables early
* Keep retention balanced (10–50)
* Use approvals only for production

### Execution

* Always use unique artifact tags
* Monitor logs actively
* Test in non-prod first
* Add meaningful approval comments

### YAML

* Validate syntax before upload
* Keep YAML files in Git
* Reuse job templates

---

##  Troubleshooting (Quick Fixes)

| Issue               | Solution                     |
| ------------------- | ---------------------------- |
| YAML errors         | Fix indentation / syntax     |
| Tag already used    | Choose a new unique tag      |
| Stage not running   | Approvals pending            |
| Service not visible | Check Service configuration  |
| Pipeline missing    | Re-save and refresh overview |

---

**Document Version:** 1.0
**Last Updated:** 13 October 2025
**Platform:** Buildpiper


