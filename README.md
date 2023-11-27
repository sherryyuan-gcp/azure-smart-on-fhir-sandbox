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

[Deploy Proxy services](https://github.com/Azure-Samples/azure-health-data-and-ai-samples/blob/main/samples/smartonfhir/docs/deployment.md)

```sh
cd azure-health-data-and-ai-samples/samples/smartonfhir
azd init #env name = smartonfhir-dev

# List users
powershell ../../../Get-UserInfo.ps1

# add claim to user
powershell ./scripts/Add-FhirUserInfoToUser.ps1 -UserObjectId "b0c27481-a11d-4e01-8f3a-b4484b9755de" -FhirUserValue "Patient/PatientA"

# Resolve err Unable to resolve X for net6.0
dotnet nuget add source --name nuget.org https://api.nuget.org/v3/index.json
```

It configures allowed oauth scopes on Azure AD, the allowed scopes and roles can be found [here](https://github.com/Azure-Samples/azure-health-data-and-ai-samples/tree/main/samples/smartonfhir/scripts/manifest-json-contents).

Gaps:
1. Azure FHIR service allows configuring for [CORS policies](https://learn.microsoft.com/en-us/azure/healthcare-apis/fhir/configure-cross-origin-resource-sharing) without relying on proxy
2. Azure has IAM FHIR SMART user role, access granted to the users in this role will then be limited by the resources associated to their fhirUser compartment and the restrictions in the clinical scopes.
3. Each user is the service account / IAM account

Their gap: need to [add fhirUser claim to your test users](https://github.com/Azure-Samples/azure-health-data-and-ai-samples/blob/main/samples/smartonfhir/docs/ad-apps/set-fhir-user-mapping.md#add-fhiruser-claim-to-your-test-users).  each user have one scope per app.

Track