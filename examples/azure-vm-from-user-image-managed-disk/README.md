# Create a Virtual Machine from a User Image

> Prerequisite - The Storage Account with the User Image VHD should already exist

This template allows you to create a Virtual Machines from a User image. This template also deploys a Virtual Network, Public IP addresses and a Network Interface.

---

## Azure credentials for Terraform

To use this Azure Quickstart with Terraform, you will be required to set the following environment variables:
- ARM_SUBSCRIPTION_ID
- ARM_CLIENT_ID
- ARM_CLIENT_SECRET
- ARM_TENANT_ID

Read the README.md at the root of this repo for details on how to set up Azure Credentials for Terraform and how to get the values for each of the environment variables.

## Use Terraform

Once you have completed the pre-requisites and filled in all the variables in `terraform.tfvars`, then run the following command:

```
> terraform apply
```

## Pre-requisites

### Create a service principal

You will need a service principal credential that will be used by Kubernetes to interact with Azure APIs. To create a service principal in your tenant, use the [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) as follows:

```
# Ensure you use a long complex password
> az ad sp create-for-rbac --name "terraform-k8s-credentials" --role "Contributor" --password "${PASSWORD}"
```

Use the returned `appId` value for the `service_principal_client_id` variable in `terraform.tfvars`. Use the ${PASSWORD} value for the `service_principal_client_secret` variable in `terraform.tfvars`.

---

This is based on the [101-vm-from-user-image](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) Azure Quick Start Template.