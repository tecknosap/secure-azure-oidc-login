# Project 1: Secure Azure Login with OIDC

## 🔍 Overview

This project demonstrates how to securely connect GitHub Actions workflows to Azure using OpenID Connect (OIDC), eliminating the need to store long-lived client secrets in CI/CD pipelines. By leveraging federated identity, this approach reduces security risks and simplifies credential management in automated workflows.

---

## ❗ Problem Statement

Many organisations face challenges with secrets in CI/CD pipelines:

- Manual secret rotation increases operational overhead  
- Storing static secrets in repositories or environments can lead to leaks  
- Maintaining secret access for multiple pipelines slows down delivery velocity  

This project addresses these problems by using token-based authentication with OIDC, providing a secure, automated, and auditable method for Azure resource management from GitHub workflows.

---

## 🎯 Project Goals

- Enable secure authentication between GitHub Actions and Azure without storing secrets  
- Implement least-privilege access using Azure service principals  
- Demonstrate a zero-secret authentication flow  
- Validate connectivity via a GitHub Actions workflow with Azure CLI commands  

---

## 🧩 Key Components

1. **Azure AD App Registration**  
   - Configured with a federated credential that trusts GitHub repositories  

2. **Service Principal (SP)**  
   - Derived from the app registration and used for scoped access to Azure resources  
   - Authenticates via federated identity (not client secrets)  

3. **GitHub Actions Workflow**  
   - Uses `azure/login@v1` to authenticate to Azure using OIDC tokens  

4. **GitHub Secrets** *(optional)*  
   - Stores identifiers such as `AZURE_SUBSCRIPTION_ID`  
   - `AZURE_CLIENT_ID` and `AZURE_TENANT_ID` may be inferred from the federated setup  

---

## 💼 Business Impact

- Secures pipelines by removing embedded secrets  
- Enables auditable and automated deployments in Azure  
- Reduces operational overhead and improves developer productivity  
- Supports enterprise compliance requirements for identity management  

---

## ⚙️ Implementation Steps

1. **Register Azure AD Application**  
   - Create an Azure AD app registration  
   - Configure a federated credential for GitHub Actions  
   - Specify trusted repository and branch for token issuance  

2. **Create a Service Principal (SP)**  
   - The SP is automatically associated with the app registration  
   - No client secret is required  

3. **Assign Permissions**  
   - Apply least-privilege roles (e.g., Contributor or custom role scoped to resources)  

4. **Configure GitHub Repository Secrets**  
   - Store `AZURE_SUBSCRIPTION_ID`  
   - Ensure `id-token` permission is granted in the workflow  

5. **Create GitHub Actions Workflow**  
   - Place the YAML file under `.github/workflows/`  
   - Configure steps to:  
     - Checkout code  
     - Authenticate to Azure using OIDC  
     - Optionally verify access with Azure CLI  

6. **Test and Validate**  
   - Push workflow to GitHub and confirm it triggers  
   - Validate Azure CLI commands execute successfully without secrets  

---

## 🚀 Usage

Once configured:

1. Developers push changes to the target branch (e.g., `main`)  
2. GitHub Actions triggers the workflow  
3. The workflow authenticates to Azure using federated identity  
4. Azure resources are managed securely, with full auditability  

No manual secret management is required in the CI/CD pipeline.

---

## 📋 Prerequisites

- Azure subscription with administrative rights  
- GitHub repository with administrative access  
- Familiarity with GitHub Actions and Azure identity management  

---

## 🧭 Solution Architecture

![Architecture Diagram](https://github.com/tecknosap/secure-azure-oidc-login/blob/main/asset/oidc-architecture.gif)

---

## 🤝 Contributing

Contributions are welcome! Whether it’s bug fixes, workflow improvements, or documentation enhancements, feel free to submit a pull request. Please follow standard GitHub workflow practices:

- Fork the repository  
- Make your changes in a separate branch  
- Submit a pull request for review  

---

## 📄 Licence

This project is licensed under the MIT Licence. You are free to use, modify, and distribute this project in accordance with the licence.

---

## 📚 References

- [Azure AD Workload Identity Federation](https://learn.microsoft.com/en-us/azure/active-directory/develop/workload-identity-federation-create-trust)  
- [GitHub Actions: Azure Login](https://github.com/Azure/login)