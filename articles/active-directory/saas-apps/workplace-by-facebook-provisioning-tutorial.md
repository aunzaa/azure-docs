---
title: 'Tutorial: Configure Workplace by Facebook for automatic user provisioning with Azure Active Directory | Microsoft Docs'
description: Learn the steps you need to do in both Workplace by Facebook and Azure Active Directory (Azure AD) to configure automatic user provisioning.
services: active-directory
author: twimmers
manager: CelesteDG
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.topic: tutorial
ms.date: 07/22/2021
ms.author: thwimmer
---

# Tutorial: Configure Workplace by Facebook for automatic user provisioning

This tutorial describes the steps you need to do in both Workplace by Facebook and Azure Active Directory (Azure AD) to configure automatic user provisioning. When configured, Azure AD automatically provisions and de-provisions users to [Workplace by Facebook](https://work.workplace.com/) using the Azure AD Provisioning service. For important details on what this service does, how it works, and frequently asked questions, see [Automate user provisioning and deprovisioning to SaaS applications with Azure Active Directory](../app-provisioning/user-provisioning.md).

## Capabilities supported
> [!div class="checklist"]
> * Create users in Workplace by Facebook
> * Remove users in Workplace by Facebook when they do not require access anymore
> * Keep user attributes synchronized between Azure AD and Workplace by Facebook
> * [Single sign-on](./workplacebyfacebook-tutorial.md) to Workplace by Facebook (recommended)

>[!VIDEO https://www.youtube.com/embed/oF7I0jjCfrY]

## Prerequisites

The scenario outlined in this tutorial assumes that you already have the following prerequisites:

* [An Azure AD tenant](../develop/quickstart-create-new-tenant.md) 
* A user account in Azure AD with [permission](../roles/permissions-reference.md) to configure provisioning (for example, Application Administrator, Cloud Application administrator, Application Owner, or Global Administrator)
* A Workplace by Facebook single-sign on enabled subscription

> [!NOTE]
> To test the steps in this tutorial, we do not recommend using a production environment.

> [!NOTE]
> This integration is also available to use from Azure AD US Government Cloud environment. You can find this application in the Azure AD US Government Cloud Application Gallery and configure it in the same way as you do from public cloud.

To test the steps in this tutorial, you should follow these recommendations:

- Don't use your production environment, unless it is necessary.
- If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).

## Step 1. Plan your provisioning deployment
1. Learn about [how the provisioning service works](../app-provisioning/user-provisioning.md).
2. Determine who will be in [scope for provisioning](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts.md).
3. Determine what data to [map between Azure AD and Workplace by Facebook](../app-provisioning/customize-application-attributes.md).

## Step 2. Configure Workplace by Facebook to support provisioning with Azure AD

Before configuring and enabling the provisioning service, you need to decide what users in Azure AD represent the users who need access to your Workplace by Facebook app. Once decided, you can assign these users to your Workplace by Facebook app by following the instructions here:

*   It's recommended that a single Azure AD user is assigned to Workplace by Facebook to test the provisioning configuration. More users may be assigned later.

*   When assigning a user to Workplace by Facebook, you must select a valid user role. The "Default Access" role doesn't work for provisioning.

## Step 3. Add Workplace by Facebook from the Azure AD application gallery

Add Workplace by Facebook from the Azure AD application gallery to start managing provisioning to Workplace by Facebook. If you have previously setup Workplace by Facebook for SSO, you can use the same application. However it's recommended that you create a separate app when testing out the integration initially. Learn more about adding an application from the gallery [here](../manage-apps/add-application-portal.md).

## Step 4. Define who will be in scope for provisioning 

The Azure AD provisioning service allows you to scope who will be provisioned based on assignment to the application and or based on attributes of the user / group. If you choose to scope who will be provisioned to your app based on assignment, you can use the following [steps](../manage-apps/assign-user-or-group-access-portal.md) to assign users to the application. If you choose to scope who will be provisioned based solely on attributes of the user or group, you can use a scoping filter as described [here](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts.md). 

* When assigning users to Workplace by Facebook, you must select a role other than **Default Access**. Users with the Default Access role are excluded from provisioning and will be marked as not effectively entitled in the provisioning logs. If the only role available on the application is the default access role, you can [update the application manifest](../develop/howto-add-app-roles-in-azure-ad-apps.md) to add more roles. 

* Start small. Test with a small set of users before rolling out to everyone. When scope for provisioning is set to assigned users, you can control this by assigning one or two users to the app. When scope is set to all users and groups, you can specify an [attribute based scoping filter](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts.md). 

## Step 5. Configure automatic user provisioning to Workplace by Facebook
This section guides you through the steps to configure the Azure AD provisioning service to create, update, and disable users in Workplace by Facebook App based on user assignments in Azure AD.

1. Sign in to the [Azure portal](https://portal.azure.com). Select **Enterprise Applications**, then select **All applications**.

	![Enterprise applications blade](common/enterprise-applications.png)

2. In the applications list, select **Workplace by Facebook**.

	![The Workplace by Facebook link in the Applications list](common/all-applications.png)

3. Select the **Provisioning** tab.

	![Screenshot of the Manage options with the Provisioning option called out.](common/provisioning.png)

4. Set the **Provisioning Mode** to **Automatic**.

	![Screenshot of the Provisioning Mode dropdown list with the Automatic option called out.](common/provisioning-automatic.png)

5. Under the **Admin Credentials** section, click on **Authorize**. You'll be redirected to Workplace by Facebook's authorization page. Input your Workplace by Facebook username and click on the **Continue** button. Click **Test Connection** to ensure Azure AD can connect to Workplace by Facebook. If the connection fails, ensure your Workplace by Facebook account has Admin permissions and try again.

 	![Screenshot shows Admin Credentials dialog box with an Authorize option.](./media/workplace-by-facebook-provisioning-tutorial/provisioning.png)

 	![authorize](./media/workplace-by-facebook-provisioning-tutorial/workplace-login.png)

6. In the **Notification Email** field, enter the email address of a person or group who should receive the provisioning error notifications and select the **Send an email notification when a failure occurs** check box.

	![Notification Email](common/provisioning-notification-email.png)

7. Select **Save**.

8. Under the **Mappings** section, select **Synchronize Azure Active Directory Users to Workplace by Facebook**.

9. Review the user attributes that are synchronized from Azure AD to Workplace by Facebook in the **Attribute-Mapping** section. The attributes selected as **Matching** properties are used to match the user accounts in Workplace by Facebook for update operations. If you choose to change the [matching target attribute](../app-provisioning/customize-application-attributes.md), you will need to ensure that the Workplace by Facebook API supports filtering users based on that attribute. Select the **Save** button to commit any changes.

   |Attribute|Type|
   |---|---|
   |userName|String|
   |displayName|String|
   |active|Boolean|
   |title|Boolean|
   |emails[type eq "work"].value|String|
   |name.givenName|String|
   |name.familyName|String|
   |name.formatted|String|
   |addresses[type eq "work"].formatted|String|
   |addresses[type eq "work"].streetAddress|String|
   |addresses[type eq "work"].locality|String|
   |addresses[type eq "work"].region|String|
   |addresses[type eq "work"].country|String|
   |addresses[type eq "work"].postalCode|String|
   |addresses[type eq "other"].formatted|String|
   |phoneNumbers[type eq "work"].value|String|
   |phoneNumbers[type eq "mobile"].value|String|
   |phoneNumbers[type eq "fax"].value|String|
   |externalId|String|
   |preferredLanguage|String|
   |urn:scim:schemas:extension:enterprise:1.0.manager|String|
   |urn:scim:schemas:extension:enterprise:1.0.department|String|
   |urn:scim:schemas:extension:enterprise:1.0.division|String|
   |urn:scim:schemas:extension:enterprise:1.0.organization|String|
   |urn:scim:schemas:extension:enterprise:1.0.costCenter|String|
   |urn:scim:schemas:extension:enterprise:1.0.employeeNumber|String|
   |urn:scim:schemas:extension:facebook:auth_method:1.0:auth_method|String|
   |urn:scim:schemas:extension:facebook:frontline:1.0.is_frontline|Boolean|
   |urn:scim:schemas:extension:facebook:starttermdates:1.0.startDate|Integer|


10. To configure scoping filters, refer to the following instructions provided in the [Scoping filter tutorial](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts.md).

11. To enable the Azure AD provisioning service for Workplace by Facebook, change the **Provisioning Status** to **On** in the **Settings** section.

	![Provisioning Status Toggled On](common/provisioning-toggle-on.png)

12. Define the users that you would like to provision to Workplace by Facebook by choosing the appropriate values in **Scope** in the **Settings** section.

	![Provisioning Scope](common/provisioning-scope.png)

13. When you're ready to provision, click **Save**.

	![Saving Provisioning Configuration](common/provisioning-configuration-save.png)

This operation starts the initial synchronization cycle of all users defined in **Scope** in the **Settings** section. The initial cycle takes longer to perform than subsequent cycles, which occur approximately every 40 minutes as long as the Azure AD provisioning service is running. 

## Step 6. Monitor your deployment
Once you've configured provisioning, use the following resources to monitor your deployment:

1. Use the [provisioning logs](../reports-monitoring/concept-provisioning-logs.md) to determine which users have been provisioned successfully or unsuccessfully
2. Check the [progress bar](../app-provisioning/application-provisioning-when-will-provisioning-finish-specific-user.md) to see the status of the provisioning cycle and how close it is to completion
3. If the provisioning configuration seems to be in an unhealthy state, the application will go into quarantine. Learn more about quarantine states [here](../app-provisioning/application-provisioning-quarantine-status.md).

## Troubleshooting tips
*  If you see a user unsuccessfully created and there is an audit log event with the code "1789003" it means that the user is from an unverified domain.
*  There are cases where users get an error 'ERROR: Missing Email field: You must provide an email Error returned from Facebook: Processing of the HTTP request resulted in an exception. See the HTTP response returned by the 'Response' property of this exception for details. This operation was retried zero times. It will be retried again after this date'. This error is due to customers mapping mail, rather than userPrincipalName, to Facebook email, yet some users don't have a mail attribute. 
To avoid the errors and successfully provision the failed users to Workplace from Facebook, modify the attribute mapping to the Workplace from Facebook email attribute to Coalesce([mail],[userPrincipalName]) or unassign the user from Workplace from Facebook, or provision an email address for the user.  
*  There is an option in Workplace, which allows the existence of [users without email addresses.](https://www.workplace.com/resources/tech/account-management/email-less#enable) If this setting is toggled on the Workplace side, provisioning on the Azure side must be restarted in order for users without emails to successfully be created in Workplace.  

## Update existing Workplace by Facebook application to use the Workplace by Facebook SCIM 2.0 endpoint
Prior to December 2021, all Workplace by Facebook applications created were configured to utilize the Workplace by Facebook SCIM 1.0 endpoint. Starting December 2021, all newly created Workplace by Facebook applications are configured to utilize the Workplace by Facebook SCIM 2.0 endpoint. Completing the steps below will update applications configured to use the SCIM 1.0 endpoint to the use the SCIM 2.0 endpoint. These steps will remove any customizations previously made to the Workplace by Facebook application, including:
* Authentication details
* Scoping filters
* Custom attribute mappings

Be sure to note any changes that have been made to the settings listed above before completing the steps below. Failure to do so will result in the loss of customized settings. 

1. Sign into the Azure portal at https://portal.azure.com 
2. Navigate to your current Workplace by Facebook app under Azure Active Directory > Enterprise Applications
3. In the Properties section of your new custom app, copy the Object ID.

	![Screenshot of Workplace by Facebook app in the Azure portal](./media/workplace-by-facebook-provisioning-tutorial/app-properties.png)

4. In a new web browser window, go to https://developer.microsoft.com/graph/graph-explorer and sign in as the administrator for the Azure AD tenant where your app is added. 

	![Screenshot of Microsoft Graph explorer sign in page](./media/workplace-by-facebook-provisioning-tutorial/permissions.png)

5. Check to make sure the account being used has the correct permissions. The permission “Directory.ReadWrite.All” is required to make this change.                              

	![Screenshot of Microsoft Graph settings option](./media/workplace-by-facebook-provisioning-tutorial/permissions-2.png)                          

	![Screenshot of Microsoft Graph permissions](./media/workplace-by-facebook-provisioning-tutorial/permissions-3.png)
	
6. Run the command below to delete the provisioning job:

DELETE https://graph.microsoft.com/beta/servicePrincipals/[object-id]/synchronization/jobs/[job-id]

7. In the Graph Explorer, run the command below. Replace "[object-id]" with the service principal ID (object ID) copied from the third step.             
_POST https://graph.microsoft.com/beta/servicePrincipals/[object-id]/synchronization/jobs { "templateId": "FacebookWorkplace" }_           

	![Screenshot of Microsoft Graph request](./media/workplace-by-facebook-provisioning-tutorial/graph-request.png)

8. Return to the first web browser window and select the Provisioning tab for your application. Your configuration will have been reset. You can confirm the upgrade has taken place by confirming the Job ID starts with “FacebookWorkplace”. 

9. Update the tenant URL in the Admin Credentials section to the following: https://scim.workplace.com/  
![Screenshot of Admin Credentials in the Workplace by Facebook app in the Azure portalt](./media/workplace-by-facebook-provisioning-tutorial/credentials.png)

10. Restore any previous changes you made to the application (Authentication details, Scoping filters, Custom attribute mappings) and re-enable provisioning. 

## Change log

* 09/10/2020 - Added support for enterprise attributes "division", "organization", "costCenter" and "employeeNumber". Added support for custom attributes "startDate", "auth_method" and "frontline"
* 07/22/2021 - Updated the troubleshooting tips for customers with a mapping of mail to Facebook mail yet some users don't have a mail attribute

## More resources

* [Managing user account provisioning for Enterprise Apps](../app-provisioning/configure-automatic-user-provisioning-portal.md)
* [What is application access and single sign-on with Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)

## Next steps

* [Learn how to review logs and get reports on provisioning activity](../app-provisioning/check-status-user-account-provisioning.md)
