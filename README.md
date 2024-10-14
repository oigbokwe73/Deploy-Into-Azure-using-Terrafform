# Deploy-Into-Azure-using-Terraform


Here's a detailed **Mermaid flowchart** diagram showing the process of using Azure DevOps with Terraform to deploy resources in Azure, including the use of **Azure Key Vault** for managing Service Principal Identities (SPI) and **Azure Blueprint** at the management group level.

```mermaid
graph TD
    A[Start: Developer Pushes Code to Azure DevOps] -->|Trigger| B[Azure DevOps Pipeline Initiated]
    
    B --> C[Fetch Terraform Scripts from Git Repository]
    
    C --> D[Azure Key Vault Authentication]
    D -->|Service Principal ID| E[Fetch Service Principal from Key Vault]
    
    E --> F[Azure DevOps Access Azure Resources]
    
    F --> G[Apply Azure Blueprint]
    G -->|Management Group Policy| H[Azure Blueprint Enforces Compliance]
    
    H --> I[Terraform Initializes Backend]
    I --> J[State Stored in Azure Storage]
    
    J --> K[Terraform Plan Execution]
    
    K --> L[Manual Approval Stage]
    L --> M[Terraform Apply]
    
    M --> N[Deploy Azure Resources]
    N --> O1[Deploy Azure SQL]
    N --> O2[Deploy Azure Logic App]
    
    O1 --> P[Terraform Updates State in Azure Storage]
    O2 --> P
    
    P --> Q[Monitor Deployment in Azure DevOps]
    
    Q --> R[End: Resources Successfully Deployed]
    
    subgraph Key Vault and Security
        D -->|Access Control| E
        E -->|Rotation Policy| E[Key Vault Manages Service Principal Certificates]
    end
    
    subgraph Blueprint Enforcement
        G -->|Management Group| H
    end
```

### Explanation:
- **Key Vault and Security**: Shows how Azure Key Vault is used to store and manage Service Principal credentials, including automated certificate rotation.
- **Blueprint Enforcement**: Demonstrates how Azure Blueprints are applied to ensure compliance at the management group level before any resources are deployed.
- **Terraform Steps**: Shows the flow from initializing Terraform, running a `plan`, manual approval (if necessary), and `apply` stages that deploy resources such as Azure SQL and Logic App.
- **State Management**: Terraform state is stored in Azure Storage, ensuring consistent state tracking across different runs.

This flow represents a complete lifecycle from code push to resource deployment, ensuring security and governance using Azure Key Vault and Blueprints.
