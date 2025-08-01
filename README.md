# Project 1: Secure Azure Login with OIDC

## Overview

This project replicates a real-world enterprise security engagement where client secrets in CI/CD pipelines posed a significant risk. By adopting OpenID Connect (OIDC) for Azure authentication in GitHub Actions, the solution eliminates secret sprawl and improves pipeline security posture.

## Business Problem Solved

Manual secret rotation and leakage risks increase attack surfaces and slow delivery velocity. Enterprises require scalable, secure CI/CD authentication without managing static credentials.

## What You Will Build

- Azure AD app registration configured for federated identity with GitHub.
- Least-privilege service principal for scoped Azure access.
- GitHub Actions workflow leveraging `azure/login@v1` to authenticate using OIDC.
- Verified zero-secret Azure authentication flow.

## Enterprise Impact

- Secures CI/CD pipelines by removing embedded secrets.
- Enables automated, auditable Azure resource deployments.
- Accelerates pipeline maintenance with identity federation.

## Step-by-Step

1. Register Azure AD App with OIDC trust to GitHub repo.
2. Assign minimal permissions via service principal.
3. Store client ID, tenant ID, subscription ID in GitHub Secrets.
4. Configure and test GitHub Actions with `azure/login@v1`.
5. Validate token-based Azure CLI access in workflow.

## Prerequisites

- Azure subscription and admin rights
- GitHub repository admin access

## References

- [Azure AD OIDC Integration](https://learn.microsoft.com/en-us/azure/active-directory/develop/workload-identity-federation)
- [GitHub Azure Login Action](https://github.com/Azure/login)
