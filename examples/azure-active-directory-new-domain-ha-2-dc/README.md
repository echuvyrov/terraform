# Create 2 new Windows VMs, create a new AD Forest, Domain and 2 DCs in an availability set

This template will deploy 2 new VMs (along with a new VNet, Storage Account and Load Balancer) and create a new AD forest and domain. Each VM will be created as a DC for the new domain and will be placed in an availability set. Each VM will also have an RDP endpoint added with a public load balanced IP address.

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

## Further information

For more information on Azure Virtual Machines and Virtual Machine Extensions:

- [Virtual Machine Documentation](https://docs.microsoft.com/en-us/azure/virtual-machines/)
- [Virtual Machine REST API Reference](https://docs.microsoft.com/en-us/rest/api/compute/virtualmachines)
- [Virtual Machine Extension REST API Reference](https://docs.microsoft.com/en-us/rest/api/compute/extensions)

---

This is based on the [active-directory-new-domain-ha-2-dc](https://github.com/Azure/azure-quickstart-templates/tree/master/active-directory-new-domain-ha-2-dc) Azure Quick Start Template.
