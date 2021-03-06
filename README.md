# Move file attachments from Dynamics 365 to Azure Blob using Web API

Move Dynamics 365 Customer Engagement aka CRM Online attachments (Notes attachments / Email Activity Mime attachments) to Azure Blob storage using Azure Logic Apps.

These Logic Apps uses the below:

- Uses Application user to connect to Dynamics CRM via Web API (For more information, please visit <https://github.com/anilvem1/CrmWebApiOAuth>)
- Uses Azure Blob REST API to connect to Blob
- No dependency on Logic App API connections
- Applicable to Dynamics 365 CRM versions 8.2 and later

It would be ideal to test run the these Logic Apps in your pre - production environments before using in your production environment.

## Description

As a customer, I would like to move all my existing CRM attachments stored in Notes / Emails to an Azure Blob as a one time / continuous setup.
These Logic Apps can be used together with the Attachment Management solution available in <a href="https://appsource.microsoft.com/en-us/product/dynamics-365/microsoft_labs.96257e65-dbbe-43db-b775-77cf1609530c">AppSource</a>.

## Move CRM Note Attachments to Azure Blob

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fanilvem1%2FLAMoveCRMAttachmentsToBlob-API%2Fmaster%2FLA-API-MoveCRMNote-AttachmentsToBlob.json" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"/>
</a>

## Move CRM Email Attachments to Azure Blob

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fanilvem1%2FLAMoveCRMAttachmentsToBlob-API%2Fmaster%2FLA-API-MoveCRMEmail-AttachmentsToBlob.json" target="_blank">
<img src="http://azuredeploy.net/deploybutton.png"/>
</a>

## Pre requisites

1) Valid Dynamics 365 CRM instance
2) Valid Azure Subscription
3) Valid Azure Storage Account & Blob

## Deployment steps

You can click the "Deploy to Azure" button at the beginning of this document.

- Enter the parameters as required
  - Subscription Tenant Id: Specify a valid Office365 subscription Tenant ID. Ex: 72f988bf-86f1-41af-91ab-2d7cd0xxxxxx
  - Crm Client Id: Specify a valid Azure AD app client ID to access CRM resource.
  - Crm Client Secret: Specify a valid Azure AD app client secret to access CRM resource.
  - Crm Org Domain Name: Specify a valid Dynamics CRM Online Org Domain Name Ex: contoso
  - Crm Org Version: Specify a valid Dynamics CRM Online Org Version Ex: 8.2, 9.0
  - Azure Storage Blob Container Url: Specify a valid azureStorageBlobContainerUrl. Ex: <https://StorageAccountName.blob.core.windows.net/ContainerName/>
  - Azure Storage SAS Key: Specify a valid storage account SAS key. Ex: ?sv=yyyy-mm-dd&ss=.....

- Enter the parameter 'azureStorageBlobContainerUrl' with correct Blob name & container name
- Enter the Azure Storage account SAS key (Please make sure its a valid SAS key)
- Click 'I agree to the terms and conditions stated above'
- Click Purchase

## Usage

Once the Logic App deployment is completed, you can perform below steps to test your Logic App

- Open Logic App in Code View
- Recurrence: Change the recurrence schedule of Logic App as per your requirement to make it schedule job
- Note: By default, Logic App moves top 2 attachment records ("$top": 2) to Azure Blob. Please update the Logic App in code view with the number you wanted

## Important

If you have Attachment Management solution installed from AppSource, please disable the RetrieveMultiple / Update plugin steps on Note & ActivityMimeAttachment entities to avoid any performance issues.
