# Prerequisites

### Terraform code 

Complete terraform files to create EKS in AWS VPC is available in the `eks-install` folder of this repo. This includes remote backend and statelocking implementation as well.

- `eks-install`: Folder that holds the complete terraform hcl files.
- `backend`: Folder that holds hcl files for s3 bucket and dynamodb creation.
- `modules`: Terraform Modules for VPC and EKS.
- `main.tf`: Main file that invokes the modules to create EKS in VPC.
- `variables.tf`: Variables for main.tf
- `outputs.tf`: Output values you wish to see post terraform execution, For example - `VPC ID`.

### Useful plugins to write HCL files

- `Terraform`
- `YAML`
- `GitHub Copilot`

### Documentation

- For any additional help,Took help from Terrafor Documentation.


### Reason to use Remote Backend

By default, Terraform stores its statefile (terraform.tfstate) locally on the machine where Terraform is executed. This approach has several issues:

1. Risk of Data Loss: If the local machine crashes or the file is accidentally deleted, the statefile is lost.
2. Collaboration Challenges: When multiple users work on the same Terraform project, local statefiles can lead to inconsistencies and conflicts.
3. Concurrency Issues: If two users apply changes simultaneously, the statefile may become corrupted.
4. Security Risks: Local statefiles may contain sensitive data (e.g., resource IDs, credentials) that could be exposed.

### How S3 Bucket Solves These Problems

1. Centralized Storage: The statefile is stored in a remote S3 bucket, making it accessible to all team members.
2. Versioning Support: S3 enables versioning, allowing rollback to previous state versions if needed.
3. State Consistency: When used with DynamoDB for state locking, S3 prevents simultaneous modifications, avoiding corruption.
4.Security & Backup: S3 supports encryption and automated backups, reducing security risks and ensuring recovery options.
5. Scalability: S3 can handle large statefiles efficiently without performance issues.

# Dynamodb for state locking

## **Problem with No State Locking**
When multiple users or processes run Terraform at the same time, several issues can arise:
1. **Concurrency Conflicts**: If two users apply changes simultaneously, they might overwrite each other's changes, leading to inconsistencies.
2. **State Corruption**: Without locking, partial updates can occur, resulting in a corrupted statefile.
3. **Unreliable Infrastructure Changes**: Race conditions can cause Terraform to misinterpret infrastructure state, leading to unintended modifications.

## **How DynamoDB Solves These Problems**
1. **State Locking**: DynamoDB creates a lock entry when Terraform applies changes, preventing concurrent modifications.
2. **Ensures Consistency**: Only one process can modify the statefile at a time, ensuring consistency and preventing corruption.
3. **Automatic Lock Release**: When Terraform execution completes, the lock entry is removed, allowing the next process to proceed.
4. **High Availability**: As a managed AWS service, DynamoDB provides reliable and scalable state locking.
5. **Cost Efficiency**: With `PAY_PER_REQUEST` billing, DynamoDB incurs minimal cost for Terraform state locking.

# Terraform Modular approach benifits

## **What is Terraform Modular Approach?**
Terraform's modular approach allows infrastructure to be broken down into reusable and maintainable components called **modules**. Instead of writing everything in a single configuration file, modules help in structuring code for better scalability and reusability.
