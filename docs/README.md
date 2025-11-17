# Setup steps on Win11 Machine

https://chocolatey.org/install

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

## On a frersh Azure VM, Docker needs WSL Update  
  
wsl --update  

# Lab 02
## On 02_01
Would it be a good idea to Copy+Paste the content of the issue from the lab? Just in case the student does not change the model or for any reason the result is significantly different? And results in different outcomes.  
  
The Lab screenshot shows GPT-5 mini and my default on GH was GPT-4.1  

# For example This is the Issue description GHCP Chat generated for me. Compare to the text from the Lab.

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
