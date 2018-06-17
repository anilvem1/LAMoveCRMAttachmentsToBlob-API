# Move file attachments from Dynamics 365 to Azure Blob

Move Dynamics 365 Customer Engagement aka CRM Online attachments (Notes attachments / Email Activity Mime attachments) to Azure Blob storage using Azure Logic Apps.

These Logic Apps uses the below:

- Uses Application user to connect to Dynamics CRM via Web API (For more information, please visit <https://github.com/anilvem1/CrmWebApiOAuth>)
- Uses Azure Blob REST API to connect to Blob
- No dependency on API connections

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

#### Note: If CRM version is 9.0 and later, please do the below

- While deploying Logic App (LA-API-MoveCRMEmail-AttachmentsToBlob), enter the parameter 'crmOrgVersion' value as 8.2 instead of 9.0

## Pre requisites

1) Valid Azure Subscription
2) Valid Azure Storage Account & Blob

## Deployment steps

You can click the "Deploy to Azure" button at the beginning of this document.

- Enter the parameters as required
- Enter the parameter 'azureStorageBlobContainerUrl' with correct Blob name & container name
- Enter the Azure Storage account SAS key (Please make sure its a valid SAS key)
- Click 'I agree to the terms and conditions stated above'
- Click Purchase

## Usage

Once the Logic App deployment is completed, you can perform below steps to test your Logic App

- Open Logic App in Code View
- Make sure the the CRM org unique name is having correct extension based on region. (Ex: NA its crm , Australia its crm6 and so on)
- Recurrence: Change the recurrence schedule of Logic App as per your requirement to make it schedule job
- Note: By default, Logic App moves top 2 attachment records ("$top": 2) to Azure Blob. Please update the Logic App in code view with the number you wanted

## Important

If you have Attachment Management solution installed from AppSource, please disable the RetrieveMultiple / Update plugin steps on Note & ActivityMimeAttachment entities to avoid any performance issues.
