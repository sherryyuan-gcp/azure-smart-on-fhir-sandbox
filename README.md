# Azure SMART-on-FHIR Sandbox

This setup a sample app that interacts with [Azure Smart-on-FHIR](https://learn.microsoft.com/en-us/azure/healthcare-apis/fhir/smart-on-fhir).

# Setup

[Create](https://azure.microsoft.com/en-ca/free/cloud-services/search/) Azure cloud account.

(Only needed if default subscription does not suite your need) [Create Azure Subscription](https://learn.microsoft.com/en-us/azure/cost-management-billing/manage/create-subscription), view list of subscriptions [here](https://portal.azure.com/#view/Microsoft_Azure_Billing/SubscriptionsBladeV2).

Create [resource group](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/manage-resource-groups-portal) (`fhir-smart-on-fhir`), view list of resource groups [here](https://portal.azure.com/#view/HubsExtension/BrowseResourceGroups).

[Deploy](https://learn.microsoft.com/en-us/azure/healthcare-apis/healthcare-apis-quickstart) Azure Health Data Services workspace using Azure portal (workspace name = `azuresmartonfhir`, region = `northcentralus`, using the resource group that is just created).

[Deply FHIR service](https://learn.microsoft.com/en-us/azure/healthcare-apis/fhir/fhir-portal-quickstart) (service name = `test-store`, version = `R4`).

Enable [SMART-on-FHIR](https://learn.microsoft.com/en-us/azure/healthcare-apis/fhir/smart-on-fhir) for the deployed FHIR store.

[Register](https://learn.microsoft.com/en-us/azure/healthcare-apis/azure-api-for-fhir/register-public-azure-ad-client-app) FHIR service via App Registration on Azure Active Directory (renamed to Microsoft Entra ID). Application name = `azure-smart-on-fhir`. Other relevant [doc](https://learn.microsoft.com/en-gb/azure/healthcare-apis/azure-api-for-fhir/register-resource-azure-ad-client-app?WT.mc_id=Portal-Microsoft_Healthcare_APIs)

[Configure RBAC](https://learn.microsoft.com/en-us/azure/healthcare-apis/azure-api-for-fhir/configure-azure-rbac) for FHIR store.

Gaps:
1. Azure FHIR service allows configuring for [CORS policies](https://learn.microsoft.com/en-us/azure/healthcare-apis/fhir/configure-cross-origin-resource-sharing) without relying on proxy