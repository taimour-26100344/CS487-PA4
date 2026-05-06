<div align="center">

# PA4 Submission: TaskFlow Pipeline

<img alt="GitHub only" src="https://img.shields.io/badge/Submit-GitHub%20URL%20Only-10b981?style=for-the-badge">
<img alt="Total points" src="https://img.shields.io/badge/Total-100%20points-7c3aed?style=for-the-badge">

</div>

## Student Information

| Field | Value |
|---|---|
| Name | Taimour Rafique |
| Roll Number | 26100344 |
| GitHub Repository URL | https://github.com/taimour-26100344/CS487-PA4 |
| Resource Group | `rg-sp26-26100344` |
| Assigned Region | `swedencentral` |

## Evidence Rules

- Use relative image paths, for example: `![AKS nodes](docs/aks-nodes.png)`.
- Every image must have a 1-3 sentence description below it.
- Azure Portal screenshots must show the resource name and enough page context to identify the service.
- CLI screenshots must show the command and output.
- Mask secrets such as function keys, ACR passwords, and storage connection strings.


## Task 1: App Service Web App (15 points)

### Evidence 1.1: Forked Repository

![Forked Repo](docs/task1_1_fork.png)

Description: This is a screenshot of my forked GitHub repository showing the cloned starter code structure for the TaskFlow project.

### Evidence 1.2: App Service Overview

![Web App Overview](docs/task1_2_overview.png)

Description: The Azure App Service overview page for `pa4-26100344` showing a 'Running' status in the swedencentral region.

### Evidence 1.3: Deployment Center / GitHub Actions

![Deployment Center](docs/task1_3_deployment.png)

Description: Deployment Center view showing the successful GitHub Actions integration and a completed deployment run.

### Evidence 1.4: Live Web UI

![Live UI](docs/task1_4_live_ui.png)

Description: The TaskFlow frontend interface is live and accessible via the App Service URL, displaying the Submit Order form.

---

## Task 2: Azure Container Registry (15 points)

### Evidence 2.1: ACR Overview

![ACR Overview](docs/task2_1_acr_overview.png)

Description: Overview of the Azure Container Registry `pa426100344` using the Basic SKU in the assigned resource group.

### Evidence 2.2: Docker Builds

![Docker Builds](docs/task2_2_docker_builds.png)

Description: Successful local Docker build outputs for the `validate-api`, `report-job`, and `func-app` images.

### Evidence 2.3: ACR Repositories

![ACR Repositories](docs/task2_3_acr_repos.png)

Description: ACR repository list confirming that all three container images have been successfully tagged and pushed.

---

## Task 3: Durable Function Implementation (12 points)

### Evidence 3.1: Completed Function Code

[function_app.py](function-app/function_app.py)

Description: The completed orchestration logic in `function_app.py` chains the validation activity and the report generation activity.

### Evidence 3.2: Local Function Handler Listing

![Func Start](docs/task3_2_func_start.png)

Description: Output of `func start` showing the registration of the HTTP starter, orchestrator, and both activity functions.

---

## Task 4: Function App Container Deployment (8 points)

### Evidence 4.1: Function App Container Configuration

![Function Config](docs/task4_1_func_config.png)

Description: The Function App is configured to pull the `func-app:v1` image from my Azure Container Registry.

### Evidence 4.2: Orchestration Smoke Test

![Smoke Test](docs/task4_2_smoke_test.png)

Description: Result of the initial smoke test via `curl`, returning the instance ID and management URLs for the orchestration.

### Evidence 4.3: Expected Failed Status Before Downstream Wiring

![Failed Status](docs/task4_3_failed_status.png)

Description: The status query shows the orchestration reached a 'Failed' state as expected before Task 5 was completed.

---

## Task 5: AKS Validator (15 points)

### Evidence 5.1: AKS Cluster

![AKS Overview](docs/resource_group_overview.png)

Description: Resource group overview showing the AKS cluster `pa4-26100344` successfully provisioned.

### Evidence 5.2: Kubernetes Nodes and Pods

![AKS Nodes](docs/task5_2_nodes.png)
![AKS Pods](docs/task5_2_pods.png)

Description: Kubectl output showing the single worker node and the validator pod in a 'Running' state.

### Evidence 5.3: Kubernetes Service

![AKS Service](docs/task5_3_service.png)

Description: The `validate-service` LoadBalancer service is active with a Public External IP on port 8080.

### Evidence 5.4: Validator API Tests

![API Tests](docs/task5_4_api_tests.png)

Description: Successful test results for the validator API health check and validation logic (including rejection for high qty).

### Evidence 5.5: Function App `VALIDATE_URL`

![Validate URL](docs/task5_5_validate_url.png)

Description: The Function App settings now include the `VALIDATE_URL` pointing to the AKS LoadBalancer endpoint.

### Evidence 5.6: AKS Idle Behavior

![AKS Metrics](docs/task7_3_backend_participation.png)

Description: AKS pods remain running in the cluster even during idle periods, maintaining readiness for incoming requests at the cost of persistent resource reservation.

---

## Task 6: ACI Report Job (15 points)

### Evidence 6.1: Blob Container

![Blob Container](docs/task6_1_blob_container.png)

Description: The 'reports' container has been created in Azure Blob Storage to store the output PDFs.

### Evidence 6.2: Manual ACI Run

![Manual ACI](docs/task6_2_manual_aci.png)

Description: Overview of the manual ACI test run `ci-report-test` showing that it reached the 'Succeeded' state.

### Evidence 6.3: ACI Logs

![ACI Logs](docs/task6_3_aci_logs.png)

Description: Container logs from the ACI job confirming PDF generation and successful upload to the blob storage.

### Evidence 6.4: Generated PDF

![Generated PDF](docs/task6_4_generated_pdf.png)

Description: List of blobs in the 'reports' container showing the generated `TEST-001.pdf` from the manual run.

### Evidence 6.5: Function App Managed Identity and IAM

![Managed Identity](docs/task6_5_managed_identity.png)

Description: The User-Assigned Managed Identity is attached to the Function App to allow it to create ACIs on-demand.

### Evidence 6.6: Report App Settings

![Report Settings](docs/task6_6_report_settings.png)

Description: Environment variables configured on the Function App to provide ACI and Storage context to the activities.

---

## Task 7: End-to-End Pipeline (15 points)

### Evidence 7.1: Web App Wiring

![Web App Wiring](docs/task7_1_webapp_wiring.png)

Description: The Web App is now wired to the Function App via the `FUNCTION_START_URL` and `FUNCTION_STATUS_URL`.

### Evidence 7.2: Happy Path UI

![Form](docs/task7_2_form.png)
![Running Status](docs/task7_2_running.png)
![Completed Status](docs/task7_2_completed.png)
![PDF Result](docs/task7_2_pdf.png)

Description: The complete happy path: from form submission to polling status and finally viewing the generated PDF report.

### Evidence 7.3: Backend Participation

![Backend Evidence](docs/task7_3_backend_participation.png)

Description: Evidence of all services participating in the flow, showing logs and pods active during the orchestration.

### Evidence 7.4: Reject Path UI

![Reject Path](docs/task7_4_reject_path.png)

Description: UI showing a rejected order message when a quantity greater than 100 is submitted.

### Evidence 7.5: Resource Group Overview

![Resource Group Overview](docs/resource_group_overview.png)

Description: Overview of the resource group `rg-sp26-26100344` showing all deployed resources, including App Service, Function App, AKS, ACR, and Storage Account.

---

## Task 8: Write-up and Architecture Diagram (5 points)

### Evidence 8.1: Architecture Diagram

![Architecture Diagram](docs/architecture_diagram.png)

Description: The system architecture shows the end-to-end flow from the user's browser to the App Service, orchestrated by Durable Functions using AKS and ACI.

### Question 8.2: Service Selection

- **App Service:** Ideal for the frontend dashboard as it provides a fully managed platform for hosting the Node.js web UI with built-in CI/CD, allowing for high availability and easy scaling of the user-facing entry point.
- **Durable Functions:** Chosen as the orchestrator to manage the asynchronous, multi-step pipeline. It provides state persistence, automatic checkpoints, and retry logic which are critical for coordinating between independent microservices like the validator and report job.
- **Azure Kubernetes Service (AKS):** Used for the validator microservice because it requires a long-lived, high-availability endpoint. AKS provides the industry-standard platform for microservice orchestration, offering robust networking and declarative infrastructure.
- **Azure Container Instances (ACI):** Perfect for the report-generator job as it is a one-shot, short-lived task. ACI is cost-effective here because it only bills for the exact duration of the job execution, avoiding the costs of idle compute resources.

### Question 8.3: ACI vs AKS

- **Idle Behavior:** In our pipeline, the AKS node remains running and active even when no orders are being processed, maintaining a persistent footprint. In contrast, ACI only exists when spawned for a specific order and disappears immediately after completion.
- **Cost Behavior:** AKS incurs a steady hourly cost regardless of traffic, making it expensive for low-volume tasks but efficient for high-load services. ACI follows a consumption-based model where we only pay for the seconds the container is running, making it significantly cheaper for bursty or infrequent jobs.
- **Operational Model:** AKS requires managing clusters, namespaces, and services with Kubernetes manifests. ACI follows a serverless container model where we simply specify the image and resources without managing any underlying infrastructure.

### Question 8.4: Durable Functions vs Plain HTTP

Implementing this flow with two plain HTTP-triggered functions would be significantly harder because:
1. **Function Timeouts:** A report generation task that takes up to a minute could exceed standard HTTP request timeouts or lead to hanging client connections if chained synchronously.
2. **State & Reliability:** Durable Functions automatically persist state between steps. If the report job fails, the orchestrator can retry just that step without re-running the validator. With plain HTTP, we would need to manually implement state management (e.g., using a database) and custom retry logic to handle mid-workflow failures.

### Question 8.5: Cost Review

![Cost Analysis](docs/cost_analysis.png)

Description: The cost analysis for the resource group shows a total actual cost of approximately $0.18 for the current billing period. The primary cost driver is the Azure Container Registry ($0.16), while other services like Storage, App Service, and Container Instances have incurred negligible costs (<$0.01) due to their consumption-based or small-scale usage during the assignment.

### Question 8.6: Challenges Faced

1. **Managed Identity Propagation:** Initially, the Function App failed to create ACIs with a 403 error. This was debugged by verifying the role assignments in the Portal and realizing that Azure identity assignments can take several minutes to propagate across the tenant.
2. **ACR Pull Secret:** Setting up the AKS validator required careful configuration of the `acr-secret` in Kubernetes. I had to ensure the Docker registry credentials matched the ACR admin keys exactly for the pod to successfully pull the image from our private registry.

---
