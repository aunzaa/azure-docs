---
title: 'Tutorial: Azure Active Directory integration with Voyance | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Voyance.
services: active-directory
author: jeevansd
manager: CelesteDG
ms.reviewer: celested
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.topic: tutorial
ms.date: 04/07/2019
ms.author: jeedes
---
# Tutorial: Azure Active Directory integration with Voyance

In this tutorial, you learn how to integrate Voyance with Azure Active Directory (Azure AD).
Integrating Voyance with Azure AD provides you with the following benefits:

* You can control in Azure AD who has access to Voyance.
* You can enable your users to be automatically signed-in to Voyance (Single Sign-On) with their Azure AD accounts.
* You can manage your accounts in one central location - the Azure portal.

If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).
If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.

## Prerequisites

To configure Azure AD integration with Voyance, you need the following items:

* An Azure AD subscription. If you don't have an Azure AD environment, you can get a [free account](https://azure.microsoft.com/free/)
* Voyance single sign-on enabled subscription

## Scenario description

In this tutorial, you configure and test Azure AD single sign-on in a test environment.

* Voyance supports **SP** and **IDP** initiated SSO

* Voyance supports **Just In Time** user provisioning

## Adding Voyance from the gallery

To configure the integration of Voyance into Azure AD, you need to add Voyance from the gallery to your list of managed SaaS apps.

**To add Voyance from the gallery, perform the following steps:**

1. In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.

	![The Azure Active Directory button](common/select-azuread.png)

2. Navigate to **Enterprise Applications** and then select the **All Applications** option.

	![The Enterprise applications blade](common/enterprise-applications.png)

3. To add new application, click **New application** button on the top of dialog.

	![The New application button](common/add-new-app.png)

4. In the search box, type **Voyance**, select **Voyance** from result panel then click **Add** button to add the application.

	 ![Voyance in the results list](common/search-new-app.png)

## Configure and test Azure AD single sign-on

In this section, you configure and test Azure AD single sign-on with Voyance based on a test user called **Britta Simon**.
For single sign-on to work, a link relationship between an Azure AD user and the related user in Voyance needs to be established.

To configure and test Azure AD single sign-on with Voyance, you need to complete the following building blocks:

1. **[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.
2. **[Configure Voyance Single Sign-On](#configure-voyance-single-sign-on)** - to configure the Single Sign-On settings on application side.
3. **[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.
4. **[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.
5. **[Create Voyance test user](#create-voyance-test-user)** - to have a counterpart of Britta Simon in Voyance that is linked to the Azure AD representation of user.
6. **[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.

### Configure Azure AD single sign-on

In this section, you enable Azure AD single sign-on in the Azure portal.

To configure Azure AD single sign-on with Voyance, perform the following steps:

1. In the [Azure portal](https://portal.azure.com/), on the **Voyance** application integration page, select **Single sign-on**.

    ![Configure single sign-on link](common/select-sso.png)

2. On the **Select a Single sign-on method** dialog, select **SAML/WS-Fed** mode to enable single sign-on.

    ![Single sign-on select mode](common/select-saml-option.png)

3. On the **Set up Single Sign-On with SAML** page, click **Edit** icon to open **Basic SAML Configuration** dialog.

	![Edit Basic SAML Configuration](common/edit-urls.png)

4. On the **Basic SAML Configuration** section, if you wish to configure the application in **IDP** initiated mode, perform the following steps:

    ![Screenshot shows the Basic SAML Configuration, where you can enter Identifier, Reply U R L, and select Save.](common/idp-intiated.png)

    a. In the **Identifier** text box, type a URL using the following pattern:
    `https://<companyname>.nyansa.com`

    b. In the **Reply URL** text box, type a URL using the following pattern:
    `https://<companyname>.nyansa.com/saml/create/`

5. Click **Set additional URLs** and perform the following step if you wish to configure the application in **SP** initiated mode:

    ![Screenshot shows Set additional U R Ls where you can enter a Sign on U R L.](common/metadata-upload-additional-signon.png)

    In the **Sign-on URL** text box, type a URL using the following pattern:
    `https://<companyname>.nyansa.com/`

	> [!NOTE]
	> These values are not real. Update these values with the actual Identifier, Reply URL and Sign-on URL. Contact [Voyance Client support team](mailto:support@nyansa.com) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section in the Azure portal.

6. On the **Set up Single Sign-On with SAML** page, in the **SAML Signing Certificate** section, click **Download** to download the **Certificate (Base64)** from the given options as per your requirement and save it on your computer.

	![The Certificate download link](common/certificatebase64.png)

7. On the **Set up Voyance** section, copy the appropriate URL(s) as per your requirement.

	![Copy configuration URLs](common/copy-configuration-urls.png)

	a. Login URL

	b. Azure AD Identifier

	c. Logout URL

### Configure Voyance Single Sign-On

1. In a different web browser window, sign-on to your Voyance tenant as an administrator.

2. Go to the top right corner of the navigation bar and click on **Profile**.
	
	![Configure Single Sign-On On App Side Acme University](./media/voyance-tutorial/tutorial_voyance_001.png) 

3. Click **Admin Settings**.

	![Configure Single Sign-On On App Side Admin Settings](./media/voyance-tutorial/tutorial_voyance_002.png)

4. Click **User Access** tab.

	![Configure Single Sign-On On App Side User Access](./media/voyance-tutorial/tutorial_voyance_003.png)

5. Click the **SSO is disabled** button to configure Azure AD as an IdP using SAML 2.0.

	![Configure Single Sign-On On App Side SSO is disabled button](./media/voyance-tutorial/tutorial_voyance_004.png)

6. Go to **SAML v2** section and perform below steps:

	![Configure Single Sign-On On App Side SAML v2](./media/voyance-tutorial/tutorial-voyance-005.png)
	
	a. Select **Enabled**.
	
	b. Paste **Login URL**, which you have copied from the Azure portal Into the **IdP Login URL** textbox.

	c. Open your downloaded Base64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **IdP Cert** textbox.
	
	d. Click **Save**.

### Create an Azure AD test user 

The objective of this section is to create a test user in the Azure portal called Britta Simon.

1. In the Azure portal, in the left pane, select **Azure Active Directory**, select **Users**, and then select **All users**.

    ![The "Users and groups" and "All users" links](common/users.png)

2. Select **New user** at the top of the screen.

    ![New user Button](common/new-user.png)

3. In the User properties, perform the following steps.

    ![The User dialog box](common/user-properties.png)

    a. In the **Name** field enter **BrittaSimon**.
  
    b. In the **User name** field type brittasimon@yourcompanydomain.extension. For example, BrittaSimon@contoso.com

    c. Select **Show password** check box, and then write down the value that's displayed in the Password box.

    d. Click **Create**.

### Assign the Azure AD test user

In this section, you enable Britta Simon to use Azure single sign-on by granting access to Voyance.

1. In the Azure portal, select **Enterprise Applications**, select **All applications**, then select **Voyance**.

	![Enterprise applications blade](common/enterprise-applications.png)

2. In the applications list, select **Voyance**.

	![The Voyance link in the Applications list](common/all-applications.png)

3. In the menu on the left, select **Users and groups**.

    ![The "Users and groups" link](common/users-groups-blade.png)

4. Click the **Add user** button, then select **Users and groups** in the **Add Assignment** dialog.

    ![The Add Assignment pane](common/add-assign-user.png)

5. In the **Users and groups** dialog select **Britta Simon** in the Users list, then click the **Select** button at the bottom of the screen.

6. If you are expecting any role value in the SAML assertion then in the **Select Role** dialog select the appropriate role for the user from the list, then click the **Select** button at the bottom of the screen.

7. In the **Add Assignment** dialog click the **Assign** button.

### Create Voyance test user

In this section, a user called Britta Simon is created in Voyance. Voyance supports just-in-time user provisioning, which is enabled by default. There is no action item for you in this section. If a user doesn't already exist in Voyance, a new one is created after authentication.

>[!NOTE]
>If you need to create a user manually, you need to contact [Voyance support team](maiLto:support@nyansa.com).

### Test single sign-on 

In this section, you test your Azure AD single sign-on configuration using the Access Panel.

When you click the Voyance tile in the Access Panel, you should be automatically signed in to the Voyance for which you set up SSO. For more information about the Access Panel, see [Introduction to the Access Panel](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).

## Additional Resources

- [List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory](./tutorial-list.md)

- [What is application access and single sign-on with Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)

- [What is Conditional Access in Azure Active Directory?](../conditional-access/overview.md)