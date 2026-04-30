<div align="center">

# TaskFlow Cloud Pipeline

### CS437 Cloud Development - Programming Assignment 4

<img alt="Azure" src="https://img.shields.io/badge/Azure-App%20Service%20%7C%20Functions%20%7C%20AKS%20%7C%20ACI-7c3aed?style=for-the-badge">
<img alt="Submission" src="https://img.shields.io/badge/Submission-GitHub%20Only-10b981?style=for-the-badge">
<img alt="Status" src="https://img.shields.io/badge/Student%20Work-TODOs%20Required-f59e0b?style=for-the-badge">

</div>

**GitHub repository description:** Starter repository for CS487 PA4, an Azure TaskFlow pipeline using App Service, Durable Functions, AKS, ACI, Blob Storage, and ACR.

<div style="background:#f5f3ff;color:#111827;border-left:6px solid #7c3aed;padding:14px 18px;border-radius:10px;margin:18px 0;">
This repository is the required starter structure for PA4. Fork it, complete the TODOs, deploy the Azure resources, commit your screenshots and write-up, then submit only your GitHub repository URL to the LMS.
</div>

## Architecture

```text
User Browser
    |
    v
App Service Web App
    |
    v
Azure Durable Function Orchestrator
    |-- calls --> AKS validate-api service
    |
    |-- creates --> Azure Container Instance report-job
                         |
                         v
                    Blob Storage PDF

All container images are stored in Azure Container Registry.
```

## What You Must Complete

| Task | Points | Required repo evidence |
|---|---:|---|
| 1. App Service Web App | 15 | Web App screenshots and GitHub deployment evidence in `SUBMISSION.md` |
| 2. Azure Container Registry | 15 | Three pushed images: `validate-api`, `report-job`, `func-app` |
| 3. Durable Function Code | 12 | Completed `function-app/function_app.py` |
| 4. Function App Container Deployment | 8 | Function App screenshots and starter/status URL evidence |
| 5. AKS Validator | 15 | Updated Kubernetes YAML, AKS screenshots, validator curl tests |
| 6. ACI Report Job | 15 | Blob, ACI logs, Function identity, and app settings evidence |
| 7. End-to-End Pipeline | 15 | Happy path and reject path screenshots |
| 8. Write-up and Diagram | 5 | Architecture diagram and short answers in `SUBMISSION.md` |

## Project Structure

```text
pa4-starter/
|-- webapp/                # Node.js / Express dashboard and proxy
|   |-- server.js
|   |-- public/
|   |   |-- index.html
|   |   +-- Cloud fr.avif
|   +-- package.json
|-- function-app/          # Azure Durable Function container
|   |-- function_app.py    # TODO: complete orchestrator and activities
|   |-- Dockerfile
|   |-- host.json
|   |-- local.settings.json
|   +-- requirements.txt
|-- validate-api/          # FastAPI validator deployed to AKS
|   |-- app.py
|   |-- Dockerfile
|   |-- requirements.txt
|   +-- k8s/
|       |-- deployment.yaml
|       +-- service.yaml
|-- report-job/            # One-shot PDF generator for ACI
|   |-- generate.py
|   |-- Dockerfile
|   +-- requirements.txt
|-- docs/                  # Put all screenshots and architecture diagram here
|-- SUBMISSION_TEMPLATE.md
+-- README.md
```

## Student Workflow

1. Fork this repository to your own GitHub account.
2. Work only in your fork and keep this directory structure.
3. Use your assigned Azure resource group: `rg-sp26-<rollnum>`.
4. Use your assigned region:
   - Roll number starting with `2027-10`: `ukwest`
   - Roll number starting with `2024` or `2025` or `2026-10`: `uaenorth`
5. Build and push all three Docker images to your ACR.
6. Complete the TODOs in `function-app/function_app.py`.
7. Deploy the Web App, Function App, AKS validator, ACI report job path, and Blob Storage.
8. Copy `SUBMISSION_TEMPLATE.md` to `SUBMISSION.md`.
9. Put screenshots and your architecture diagram under `docs/`.
10. Embed every required screenshot in `SUBMISSION.md` with a short description below it.

## Local Web App Check

```bash
cd webapp
npm install
npm start
```

Open `http://localhost:8080`.

Without `FUNCTION_START_URL`, the UI should load but submitting an order should show a configuration error. That is expected until your Azure Function is deployed and wired.

## Submission Rule

<div style="background:#ecfdf5;color:#064e3b;border-left:6px solid #10b981;padding:14px 18px;border-radius:10px;margin:18px 0;">
Submit only your GitHub repository URL to the LMS. The grader must be able to verify the full assignment from your committed code, <code style="color:#111827;background:#d1fae5;padding:2px 4px;border-radius:4px;">SUBMISSION.md</code>, <code style="color:#111827;background:#d1fae5;padding:2px 4px;border-radius:4px;">docs/</code> screenshots, and architecture diagram.
</div>

Do not submit a separate PDF or ZIP unless the instructor explicitly changes the submission instructions.
