# Setup steps on Win11 Machine

[https://chocolatey.org/install](https://chocolatey.org/install#:~:text=Install%20Chocolatey%20for%20Individual%20Use)

choco install powershell-core -y  
choco install dotnet-6.0-sdk -y  
choco install dotnet-8.0-sdk -y  
choco install azure-cli azd git -y  
choco install vscode -y  
  
code --install-extension GitHub.copilot  
**Already installed**  code --install-extension GitHub.copilot-chat  
code --install-extension ms-azuretools.vscode-azure-github-copilot  
**(missing?)** code --install-extension **GitHub MCP Server**  
**Already installed**  code --install-extension ms-azuretools.vscode-azure-mcp-server  
code --install-extension ms-azuretools.vscode-bicep  
code --install-extension ms-azuretools.vscode-docker  

choco install docker-desktop -y  

## On a fresh Azure VM, Docker needs WSL Update  
  
wsl --update  

# Lab 02
## On 02_01
Would it be a good idea to Copy+Paste the content of the issue from the lab? Just in case the student does not change the model or for any reason the result is significantly different? And results in different outcomes.  
  
The Lab screenshot shows GPT-5 mini and my default on GH was GPT-4.1  

**For example** See the next 2 Markdown blocks, taht is the Issue description GHCP Chat generated for me on two different tests. Compare to the Markdownfrom the Lab (third block, below).
```markdown
## Overview
Provision an Azure infrastructure for the ZavaStorefront web application targeting a development environment. The setup should:

- Be deployed together in one resource group in the westus3 region.
- Use Bicep and AZD (Azure Developer CLI) for definition and deployment.

## Requirements
- **App Service (Linux):**
    - Should host the ZavaStorefront web application.
    - Use Docker for deployment — do not require Docker to be installed locally.
    - App Service should use Azure RBAC for image pulls instead of passwords.
- **Container Registry:**
    - For storing images deployed to the App Service via Docker.
- **Application Monitoring:**
    - Integrate Application Insights for monitoring.
- **AI Capabilities:**
    - Include Azure AI Foundry resources for leveraging GPT-4 and Phi capabilities.
    - Must use westus3 region (as required for GPT-4 and Phi access).
- **Deployment Strategy:**
    - Everything must be grouped in a single resource group per environment (e.g., `zavastorefront-dev-westus3`).
    - All resources are provisioned using Bicep templates and AZD workflows.

## Acceptance Criteria
- All infrastructure resources (App Service, Container Registry, Application Insights, AI Foundry) provisioned via Bicep with AZD.
- No need to install Docker locally for deployment — use Azure Dev resources.
- App Service pulls container images using RBAC, not passwords.
- Solution deploys fully to westus3; all necessary configuration in infrastructure-as-code.
- Monitoring enabled through Application Insights.
- AI Foundry deployed and configured for GPT-4 and Phi access in westus3.
- Documentation for any post-provision steps or environment configurations.

---
**Labels:** enhancement, documentation
**Repository:** `Zava-Labs-omarv74/TechWorkshop-L300-GitHub-Copilot-and-platform`
```
  
```markdown
## Objective
Provision Azure infrastructure for the ZavaStorefront web application in a development environment using the following resources and best practices:

### Requirements
- **Linux App Service**: Host the ZavaStorefront web application on a Linux-based Azure App Service.
- **Docker Deployment (No Local Docker)**: Use Azure Container Registry (ACR) for image storage and configure Azure App Service to pull images using Azure RBAC, not passwords.
- **Monitoring**: Set up Application Insights for runtime monitoring and diagnostics of the App Service.
- **Azure AI Foundry**: Provision and configure resources for Azure AI Foundry (GPT-4 & Phi models), ensuring they're available in West US 3 region.
- **Resource Group**: Deploy all resources (App Service, ACR, Application Insights, AI Foundry) in a single resource group located in `westus3` for unified management.
- **Dev Environment**: This infrastructure should be tailored for a development use case (cost optimization, naming conventions, general accessibility for a dev team).
- **Infrastructure as Code**: Use AZD (Azure Developer CLI) and define all resources in Bicep files for repeatable, declarative deployments.

### Acceptance Criteria
- All resources provisioned in the same resource group in `westus3`.
- App Service is Linux-based, uses a Docker image from ACR, and pulls using RBAC.
- No local Docker install required for CI/CD pipeline or developer setup.
- Application Insights monitoring configured and integrated with App Service.
- Azure AI Foundry resources (GPT-4 and Phi) are deployable and operational in West US 3.
- Deployment can be executed end-to-end with `azd` and Bicep scripts (no manual steps required).

### Tasks
- [ ] Design Bicep module for the entire resource group (App Service, ACR, Application Insights, AI Foundry).
- [ ] Implement RBAC setup for App Service to pull from ACR.
- [ ] Integrate Application Insights with App Service in Bicep definition.
- [ ] Define Azure AI Foundry (GPT-4, Phi) resources in Bicep, ensure use of correct region.
- [ ] Structure and test deployment flow using AZD.

---
If you need further breakdown, request sub-issues for individual resource setup or tasks.
```
  
**Issue text from Lab:**  

```markdown
## Summary
Provision all Azure resources as infrastructure for the ZavaStorefront web application (dev environment) into a single resource group in westus3. Use Bicep files and AZD to define and deploy all resources together. Application to be deployed as a Docker container to Linux App Service (Web App for Containers), without requiring local Docker. App Service will pull images from Azure Container Registry (ACR) using Azure RBAC and managed identity (no password secrets). The application will be monitored using Application Insights. Azure AI Foundry will also be provisioned for GPT-4 and Phi access in westus3 as these models are available there.

## Requirements
- All resources provisioned into a single resource group (e.g. `rg-zavastore-dev-westus3`) in westus3
- Azure Container Registry (ACR) for container images (SKU: Basic/Standard)
- Linux App Service (Web App for Containers) configured to pull images from ACR
- System-assigned managed identity for Web App, with AcrPull role assignment to ACR
- No password-based pulls from ACR
- Application Insights instance linked for monitoring
- Azure AI Foundry resource provisioned in westus3
- All resources defined in Bicep templates and provisioned with AZD
- No local Docker required: Image builds/pushes use az acr build or GitHub Actions (run in cloud)
- Minimal-cost SKUs appropriate for dev

## Implementation Guidance
- Use modular Bicep structure (`infra/` folder with modules for ACR, App Service Plan, Web App, App Insights, AI Foundry, and role assignments)
- Parameterize resource names, region, environment, SKUs in Bicep
- `azd.yaml` and README should document full deployment/dev workflow
- CI workflow examples for image build/push without local Docker (cloud builds)
- Role assignment in Bicep: Assign `AcrPull` on ACR to App Service managed identity
- Application Insights: Connect via instrumentation key/app settings
- AI Foundry: Use dev-appropriate SKUs; ensure region supports requested models

## Checklist
- [ ] Confirm region and subscription quotas for AI Foundry in westus3
- [ ] Bicep modules for ACR, App Service, App Insights, Role Assignment, AI Foundry
- [ ] Main Bicep template (calls modules)
- [ ] azd.yaml script (maps provision/deploy workflow)
- [ ] GitHub Actions workflow for ACR build (cloud-side or hosted runner)
- [ ] AcrPull role assignment (managed identity)
- [ ] App Insights wiring
- [ ] AI Foundry deployment and configuration
- [ ] README.md with workflow/cost notes
- [ ] Smoke test: app deploy/monitoring/AI access

---
If you need code/starter templates for Bicep or CI workflow, request below.
```

## On 02_02
After selecting the **src** context, my instance of Copilot Chat shows **Automatic** for the model, while the lab screenshot shows **GPT-4.1** (not GPT-5 mini like earlier).

**Under 02: Execute the Infrastructure scripts**
Lab instructions say to run **azd init** - My Laptop's GHCP (Claude Sonnet 4) prompted to run **azd init --no-prompt**, as part of the previous GHCP Chat instruction. It then failed to find an azd environment and prompted to create one: **azd ini --environment zavastorefront-dev**.  
  
Lab instructions also say to run **azd provision --preview**, but my GHCP prompted to run it for me. The result was an **ERROR: AADSTS700082: The refresh token has expired due to inactivity".  
  
The above command *created* all resources but the ACR listed in the Lab. Then prompted if I wanted it to proceed with **azd up*. I clicked **keep**. Empty RG **LEARN-TechExcel-GHCPandPlatform-dev** was created.

***azd up* failed for the AppInsights resource (BAD REQUEST), I told GHCP to add the SecurityControl tag to all resources in main.bicep, tried again and it woked.
  




