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

