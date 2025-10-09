<img width="1280" height="720" alt="image" src="https://github.com/user-attachments/assets/562ce889-b6f2-4782-bda1-07634592ade3" />


# Manual Deployment Guide - Buildpiper

##  Overview

This guide explains how to manually deploy applications using the Buildpiper deployment pipeline interface.

---

##  Prerequisites

* Access to the Buildpiper application portal
* Deploy permissions for target environment
* Successfully completed build with **"IN USE"** status
* Configured Kubernetes cluster and services
* Valid deployment configuration

---

##  Manual Deployment Steps

### Step 1: Navigate to Application

1. Click **Application** from the left sidebar
2. Click **Service Overview**
3. Select your application (e.g., `perfeasy-testing`)
4. Click on the service instance (e.g., `K-DEMO-SERVICE`)
---

<img width="1362" height="654" alt="image" src="https://github.com/user-attachments/assets/5502bc5f-5b91-4338-88e2-c19afb366ff5" />
<img width="1362" height="375" alt="image" src="https://github.com/user-attachments/assets/408ce077-a460-4f92-a858-46ffaaa6241e" />

---

### Step 2: Access Deploy Details

1. Click on the **ENV DEPLOY DETAILS** tab
2. Verify the environment is correct (e.g., `DEVCOMMUNITY`)
3. Confirm deployment configuration shows **"IN USE"** status
4. Review the stable configuration name
---
<img width="1363" height="651" alt="image" src="https://github.com/user-attachments/assets/3e2a71a3-2dbb-4878-bc91-ead416ed73d5" />

---

### Step 3: Trigger Deployment

1. Click the **Deploy** button (blue button with 📤 icon on the right side)
---
<img width="1362" height="248" alt="Screenshot from 2025-10-09 11-36-11" src="https://github.com/user-attachments/assets/a5374deb-b352-4b4b-b2a3-f065cd5998e1" />

2. The **"Trigger a new Deploy"** dialog will open

---
<img width="1363" height="651" alt="image" src="https://github.com/user-attachments/assets/1872d14e-6ad8-48e8-b8b6-b031b9db56e5" />

---

### Step 4: Configure Deployment Settings

#### Fetch tags from BP

**Purpose:** Automatically retrieve available build tags from Buildpiper

**Options:**

* **Yes (Recommended):** 
  - System fetches all available build tags into dropdown
  - Easier and faster selection
  - Shows only valid, built tags
  - Prevents typos and errors

* **No:** 
  - Manually type tag name
  - Use for custom or external tags
  - Requires exact tag name
  - Risk of typos

---

#### Tag (Required Field)

**Purpose:** Specify which build version to deploy

**Selection Methods:**

* **Dropdown:** Select from available build tags (when Fetch tags = Yes)
* **Manual Entry:** Click **"PROVIDE CUSTOM TAG"** to type tag name

**Requirements:**
- Must select or enter a tag to proceed
- Error message appears if left empty: **"This is required"**

**Examples:**
```
321           - Build number
v1.0.0        - Version tag
latest        - Latest build
hotfix-123    - Hotfix tag
```

---

#### Init Container Tag (Optional)

**Purpose:** Specify tag for init containers (containers that run before the main application)

**Question:** *"Do you want to deploy the same tag in the init container?"*

**Options:**

* **Yes (Default):** 
  - Init containers use same tag as main container
  - Simpler configuration
  - Ensures version consistency
  - Recommended for most cases

* **No:** 
  - Specify different tag for init containers
  - Use when init container needs different version
  - Allows independent versioning
  - Advanced use case

**Note:** This option only appears if init containers are configured for the service

---

### Step 5: Review Last Deploys Details By Clicking on History Icon

The dialog shows recent deployment history with the following information:

#### Deployment Entry Information:
- **Deploy Number:** Clickable deployment ID (e.g., Deploy #19)
- **Status Badge:** Current status (RUNNING, SUCCESS, FAILED, REVOKED)
- **Duration:** Total deployment time (e.g., 24 h 46 m 59 s)
- **User:** Username who triggered deployment (e.g., Super Admin)
- **Timestamp:** When deployment occurred (e.g., 2 days ago)
- **Artifact:** Tag/version deployed (e.g., 321) with copy icon

---
<img width="1083" height="224" alt="Screenshot from 2025-10-09 11-51-56" src="https://github.com/user-attachments/assets/99e15c81-3e23-4f0e-b13f-bcb82fdad31a" />

<img width="1362" height="566" alt="image" src="https://github.com/user-attachments/assets/3521d773-cf1a-400f-b283-67a33b367621" />

---

### Step 6: Execute Deployment

Choose one of the following options:

* **Trigger Deploy:** Starts the deployment process
* **Cancel:** Closes the dialog without any action
---

<img width="1022" height="244" alt="image" src="https://github.com/user-attachments/assets/6ac9f836-8a22-44ab-bc4e-3d92177f2423" />

---

### Step 7: Monitor Deployment

After triggering deployment:

1. **Status Updates:** Real-time deployment status changes
2. **Activity Steps:** Track each deployment phase
3. **View Logs:** Click **"VIEW LOGS"** to see detailed activity logs
4. **Check Progress:** Monitor completion of each step
---
<img width="1015" height="299" alt="image" src="https://github.com/user-attachments/assets/511dde73-1664-408f-9e77-70b543c25366" />

<img width="1358" height="507" alt="image" src="https://github.com/user-attachments/assets/4ef6f270-0d29-4d4e-a0ce-b74610659fb6" />

---

##  Deployment Status Types

| Status | Description |
|--------|-------------|
| **RUNNING**| Deployment currently in progress<br>- Pods being created or updated<br>- Health checks being performed<br>- Normal active deployment state |
| **SUCCESS**| Deployment completed successfully<br>- All pods are running<br>- Health checks passing<br>- Application is live and ready |
| **FAILED** | Deployment encountered errors<br>- Pod creation failed<br>- Health checks failed<br>- Resource or configuration issues |
| **REVOKED**| Deployment manually stopped<br>- User cancelled deployment<br>- Rollback initiated |
| **QUEUED** | Deployment queued<br>- Waiting for resources<br>- In queue behind other deployments |

---

##  Action Buttons

### Top Action Bar Icons

| Icon | Button | Description |
|------|--------|-------------|
| ⚡ | **Build** | Quick build trigger |
| 📤 | **Deploy** | Open deployment dialog (blue when active) |
| 🔄 | **Promote** | Promote build to another environment |
| ☰ | **History** | View deployment history |

---

### Deploy Entry Action Buttons

####  Parameters Button

**Purpose:** View detailed build and deployment configuration

**Opens:** Two-tab view with BUILD PARAMETERS and DEPLOY PARAMETERS

**Use Cases:**
- Verify deployment configuration
- Troubleshoot deployment issues
- Compare configurations between deployments
- Copy commit information for reference

**When to Use:**
- Before deployment to verify settings
- After deployment for documentation
- During troubleshooting to identify issues

---
##  Build Parameters

Shows information about the build that was created:

| Parameter | Description |
|-----------|-------------|
| **tag** | Docker image tag/version identifier (e.g., "321", "v1.0.0")<br>- Used to identify which build version to deploy |
| **no_cache** | Cache usage during build (true/false)<br>- `true`: Build without cached layers (clean build)<br>- `false`: Build using cached layers (faster) |
| **custom_tag** | Custom tag if manually specified<br>- Shows custom tag name if provided<br>- `null`: Auto-generated tag was used |
| **trigger_by** | Username who initiated the build<br>- Shows who created this build (e.g., "Super Admin") |
| **branch_name** | Git branch used for build<br>- Source code branch (e.g., "main", "develop", "feature/new-api") |
| **job_template_name** | Build template used<br>- Job template that defined build steps (e.g., "MI-TEMPLATE") |
| **activity_master_code** | Build activity type<br>- Internal code for build type (e.g., "ENVIRONMENT_BUILD") |
| **shallow_cloning_depth** | Git clone depth<br>- Number of commits cloned (`null` = full history)<br>- Used to speed up clone for large repositories |
| **Commit Id** | Full Git commit SHA hash<br>- Unique identifier for exact code version<br>- Click copy icon to copy hash |
| **Commit Msg** | Git commit message<br>- Description of what changed in this commit<br>- Click copy icon to copy message |

---

##  Deploy Parameters

Shows configuration used for deployment:

| Parameter | Description |
|-----------|-------------|
| **Environment Variables** | Custom environment-specific settings and configurations |
| **Resource Limits** | CPU, memory, and storage allocations for containers |
| **Replicas** | Number of pod instances to run |
| **Port Configurations** | Service and container port mappings |
| **Health Checks** | Liveness and readiness probe settings |
| **Secrets and ConfigMaps** | Referenced configuration objects and secrets |
| **Volume Mounts** | Persistent storage configurations and paths |
| **Service Account** | On which services deployment is Performed |
| **Namespace** | Kubernetes namespace for deployment |

---
<img width="1035" height="452" alt="image" src="https://github.com/user-attachments/assets/f4f74e98-ead7-4a68-b4f7-9c1b6f21e35f" />

---

####  View Activity Details

**Purpose:** Shows step-by-step deployment activity timeline

**Displays:** 
- Detailed timeline of deployment execution
- Individual step progress and status
- Time taken for each activity
- Success/failure indicators

**Use Cases:**
- Monitor deployment progress in detail
- Track which step is currently executing
- View time taken for each step
- Identify which step failed
- Debug deployment issues

<img width="1366" height="648" alt="image" src="https://github.com/user-attachments/assets/3d4845de-0449-4b49-a989-706f66323de3" />

---

#### 📤 Redeploy

**Purpose:** Deploy again using the exact same configuration

**Action:** Auto-fills all previous deployment settings

**Use Cases:**
- Retry failed deployment
- Restart application with same version
- Test deployment reliability
- Apply infrastructure fixes without code changes

**When to Use:**
- Deployment failed due to temporary issue
- Need to restart pods without changes
- Testing deployment process
- Quick redeployment needed

---
<img width="1358" height="658" alt="image" src="https://github.com/user-attachments/assets/ca4e94a0-2f45-4e0a-81cd-d10719ef1d75" />

---

####  Workspace

**Purpose:** Opens detailed workspace view with complete deployment context

**Displays:**
- Service name and environment details
- Action status and triggering user
- Container registry image path
- Full deployment logs and output
- Complete activity timeline
- Resource status and metrics

**Use Cases:**
- Deep troubleshooting and debugging
- Review complete deployment context
- Access detailed logs and metrics
- Monitor real-time deployment progress
- Debug complex deployment issues

**When to Use:**
- Need complete deployment context
- Debugging complex issues
- Reviewing detailed deployment history
- Accessing container registry details
- Performance analysis
---

<img width="1358" height="658" alt="image" src="https://github.com/user-attachments/assets/4db6b005-fc7b-40ba-8f68-40c2762b0aa9" />

---

##  Deployment Tabs

### 1. DEPLOY DETAILS

**Purpose:** Main deployment configuration and execution tab

**Features:**
- Shows deployment configuration summary
- Displays stable configuration status (IN USE)
- Lists last deployment history
- Primary tab for triggering new deployments

**Use When:**
- Starting new deployment
- Reviewing deployment status
- Checking last deployment details

---
<img width="1092" height="328" alt="image" src="https://github.com/user-attachments/assets/3f4e9c73-07c5-4ba6-a5c8-7bd568475156" />

---

### 2. INTEGRATION TESTING

**Purpose:** Configure automated tests to run after deployment

**Configuration Options:**

#### Integrations URL (Required)
- API endpoint to test after deployment
- Format: `https://your-api.com/health` or `/api/status`

#### Select Credentials
- Authentication credentials for API calls
- Choose from pre-configured credentials
- Click **"ADD CREDENTIAL"** to add new credentials

#### Method
- HTTP method for API call
- Options: GET, POST, PUT, DELETE, PATCH
- Default: GET

#### Timeout
- Maximum wait time for test response
- Specified in seconds (e.g., 30, 60, 120)
- Default: 30 seconds

#### Pause Pipeline on Failure
- **Question:** *"Do you want to pause the pipeline execution once the integration URL is hit successfully?"*
- **False (Default):** Continue deployment regardless of test result
- **True:** Stop deployment if integration test fails

#### JSON Header
- Custom HTTP headers in JSON format
- Example: `{"Content-Type": "application/json", "Authorization": "Bearer token"}`
- Optional field

**Note:** Click **"Documentation"** link for detailed integration testing guide

---
<img width="1099" height="474" alt="image" src="https://github.com/user-attachments/assets/e9c6362e-1192-4b95-9814-ae0127fcce84" />

<img width="1099" height="474" alt="image" src="https://github.com/user-attachments/assets/ce638b32-682b-416b-a2c9-3f93ab3b9c46" />

---

### 3. OTHER DEPLOYMENT INFO

**Purpose:** Configure additional deployment features and optimizations

#### Auto Scaling

**What it does:**
- Automatically adjusts pod count based on load
- Scales up when demand increases
- Scales down when demand decreases

**Configuration Options:**
- **Min Replicas:** Minimum number of pods (e.g., 1)
- **Max Replicas:** Maximum number of pods (e.g., 10)
- **CPU Threshold:** CPU usage percentage to trigger scaling (e.g., 70%)
- **Memory Threshold:** Memory usage percentage to trigger scaling (e.g., 80%)

**Benefits:**
- Optimize resource usage and costs
- Handle traffic spikes automatically
- Maintain performance under load
- Reduce infrastructure costs during low traffic

**Note:** Click **"Documentation"** link for access levels and detailed configuration
---
<img width="1099" height="474" alt="image" src="https://github.com/user-attachments/assets/0fb72bac-59ec-45c1-acde-ead1f8dde0ec" />

---

### 4. GENERATED MANIFEST

**Purpose:** View Kubernetes deployment manifests generated by the system

**Displays:**
- Complete YAML configuration files
- All Kubernetes resources created (Deployment, Service, Ingress, etc.)
- Resource definitions and specifications
- Applied configurations and settings
- Environment variables and secrets
- Volume mounts and storage
- Service and networking configuration

**Use Cases:**
- Review complete deployment configuration
- Troubleshoot deployment issues
- Verify resource settings and limits
- Copy manifest for external use
- Understand what gets deployed
- Debug configuration problems

**Note:** 
- Shows **"No Manifest File has been generated"** if no deployment has run yet
- Manifest is generated after first successful deployment
- Updates after each new deployment

---
<img width="1099" height="474" alt="image" src="https://github.com/user-attachments/assets/61671173-07e7-402c-9076-8364d951a399" />

---

## 🔄 Activity Steps

Understanding the three-phase deployment workflow:

### Phase 1: Pre Hooks Executing

**Purpose:** Runs scripts and validations before deployment starts

**Activities:**
- Pre-deployment validation checks
- Database backup operations
- Notification triggers (Slack, Email, etc.)
- Custom pre-deployment scripts
- Environment preparation

**Typical Duration:** 0-30 seconds

**Success Criteria:** All pre-hooks complete without errors

---

### Phase 2: Deployment Manifest Creation

**Purpose:** Generates Kubernetes deployment manifests

**Activities:**
- Creates YAML configuration files
- Applies environment variables and secrets
- Sets resource limits and requests
- Configures services and ingress rules
- Applies ConfigMaps and secrets
- Validates manifest syntax

**Typical Duration:** 2-10 seconds

**Output:** Kubernetes manifest files ready for deployment

---

### Phase 3: Pod Shift

**Purpose:** Deploy and start application pods

**Activities:**
- Creates new pods with updated version
- Waits for pods to start successfully
- Performs health checks (liveness probes)
- Performs readiness checks
- Routes traffic to new pods
- Terminates old pods (rolling update)
- Verifies deployment stability

**Typical Duration:** 30 seconds to several minutes
*(Depends on application startup time and health check configuration)*

**Success Criteria:** All pods running and passing health checks

<img width="1032" height="318" alt="image" src="https://github.com/user-attachments/assets/466a6a70-f49e-4597-be22-b0e7684fdd43" />

---

### Status Indicators:

| Status | Description |
|--------|-------------|
| **Completed** | Step finished successfully |
| **In Progress** | Step currently executing |
| **Failed** | Step encountered errors |
| **Paused/Revoked** | Step paused or cancelled |

### Duration Display:

Each step shows execution time (e.g., "0m 4s", "2m 30s")
- Helps identify slow or stuck steps
- Useful for performance optimization
- Indicates if step is taking longer than expected

---


##  Troubleshooting

### Common Issues and Solutions

| Issue | Possible Cause | Fix |
|-------|---------------|-----|
| **Deploy button not visible** | - Permissions issue<br>- Build not ready | - Check deploy permissions<br>- Verify build shows "IN USE" status<br>- Refresh page (F5) |
| **No tags available in dropdown** | - No builds completed<br>- Fetch tags disabled | - Ensure build completed successfully<br>- Enable "Fetch tags from BP"<br>- Check build status in ENV BUILD DETAILS |
| **"This is required" error** | - Tag not selected | - Select tag from dropdown<br>- Or enter custom tag using "PROVIDE CUSTOM TAG" |
| **Deployment fails immediately** | - Configuration error<br>- Resource limits<br>- Image pull error | - Check deployment logs<br>- Review configuration in DEPLOY DETAILS<br>- Verify container image exists<br>- Check resource quotas |
| **Deployment stuck in PENDING** | - Resource constraints<br>- Queue backlog | - Check cluster resources (CPU, memory)<br>- Wait for other deployments to complete<br>- Review resource requests |
| **Long deployment times** | - Large container image<br>- Slow health checks<br>- Resource constraints | - Optimize container image size<br>- Adjust health check intervals<br>- Review pod logs for startup issues<br>- Check cluster performance |
| **Deployment stuck in Pod Shift** | - Health checks failing<br>- Pod crash loops<br>- Resource issues | - Check pod logs in Workspace<br>- Review health check configuration<br>- Verify environment variables<br>- Check resource limits |
| **Parameters not showing** | - UI issue<br>- No deployment selected | - Click Parameters button<br>- Ensure deployment entry is visible<br>- Refresh page |
| **Redeploy not working** | - Previous deployment incomplete<br>- Permission issue | - Verify previous deployment status<br>- Check deploy permissions<br>- Try manual deployment |
| **Workspace not opening** | - Popup blocker<br>- Browser settings | - Allow popups for this site<br>- Try different browser<br>- Check browser console for errors |
| **Integration testing fails** | - Wrong URL<br>- Credentials issue<br>- Timeout too short | - Verify integration URL is correct<br>- Check credentials are valid<br>- Increase timeout value<br>- Review API logs |
| **Manifest not generated** | - No deployment run yet<br>- Deployment failed | - Run successful deployment first<br>- Check deployment status<br>- Review error logs |

---

##  Best Practices

### Before Deployment

-  **Verify Environment:** Always confirm you're deploying to the correct environment
-  **Check Build Status:** Ensure build shows "IN USE" status before deploying
-  **Review Last Deployment:** Check previous deployment status and duration
-  **Use Fetch Tags:** Enable "Fetch tags from BP" to avoid tag errors
-  **Verify Tag:** Double-check you're deploying the correct version
-  **Check Resources:** Ensure cluster has sufficient resources

### During Deployment

-  **Monitor Progress:** Watch Activity Steps for real-time status
-  **Check Logs:** Review logs immediately if issues occur
-  **Track Duration:** Compare with previous deployment times
-  **Watch for Errors:** Address failures promptly

### After Deployment

-  **Verify Success:** Confirm all pods are running and healthy
-  **Test Application:** Perform basic functionality tests
-  **Document Changes:** Record deployment details for reference
-  **Notify Team:** Inform team of deployment completion
-  **Monitor Metrics:** Check application metrics and logs

### General Guidelines

-  **Test in DEV First:** Always deploy to DEV before higher environments
-  **Progressive Rollout:** Follow DEV → QA → UAT → PROD progression
-  **Use Integration Testing:** Configure automated tests for critical services
-  **Enable Auto Scaling:** Use for production environments with variable load
-  **Review Manifests:** Check generated manifests periodically
-  **Use Redeploy:** For quick retries of failed deployments
-  **Set Up Notifications:** Configure alerts for deployment status

---

##  Quick Reference

### Deployment Workflow

```
┌─────────────────────────────────────────────────────────┐
│  1. Application → Service Overview → Select Service     │
│  2. ENV DEPLOY DETAILS → Review Configuration          │
│  3. Click Deploy → Configure Settings                   │
│  4. Select Tag → Trigger Deploy                        │
│  5. Monitor Progress → Verify Success                   │
└─────────────────────────────────────────────────────────┘
```

### Key Buttons Quick Reference

| Button | Action | Location |
|--------|--------|----------|
| **Deploy** | Open deployment dialog | Top right (blue button) |
| **Trigger Deploy** | Start deployment | Deploy dialog (blue button) |
| **Parameters** | View build/deploy parameters | Deploy entry |
| **Redeploy** | Redeploy with same config | Deploy entry |
| ** Workspace** | Open workspace view | Deploy entry |
| **VIEW LOGS** | View activity logs | Activity steps |
| **Cancel** | Close dialog | Deploy dialog |



---

## 🆘 Support

### Getting Help

* **Deployment Issues:** 
  - Check activity logs and error messages
  - Review deployment configuration
  - Use Workspace for detailed troubleshooting

* **Tag Issues:** 
  - Verify build completed successfully
  - Check ENV BUILD DETAILS tab
  - Ensure tag exists in registry

* **Permission Issues:** 
  - Contact system administrator
  - Verify user has deploy permissions
  - Check environment access rights

* **Configuration Issues:** 
  - Review DEPLOY DETAILS tab
  - Check GENERATED MANIFEST
  - Verify environment variables and secrets

* **Integration Testing Issues:**
  - Verify integration URL is accessible
  - Check credentials configuration
  - Review API logs and responses
  - Adjust timeout settings

---

## Additional Resources

- **Documentation Link:** Available in INTEGRATION TESTING and OTHER DEPLOYMENT INFO tabs
- **Job Templates:** Configure in Job Templates section
- **Environment Overview:** Review environment configurations
- **Pipeline Overview:** Understand complete deployment pipeline

---


**Document Version:** 1.0  
**Last Updated:** October 2025  
**Platform:** Buildpiper Deployment
