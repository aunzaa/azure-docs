---
title: Page layout versions
titleSuffix: Azure AD B2C
description: Page layout version history for UI customization in custom policies.
services: active-directory-b2c
author: kengaderdus
manager: CelesteDG

ms.service: active-directory
ms.workload: identity
ms.topic: reference
ms.date: 09/22/2021
ms.author: kengaderdus
ms.subservice: B2C
---

# Page layout versions

Page layout packages are periodically updated to include fixes and improvements in their page elements. The following change log specifies the changes introduced in each version.

> [!IMPORTANT]
> Azure Active Directory B2C releases improvements and fixes with each new page layout version. We highly recommend you keep your page layout versions up-to-date so that all page elements reflect the latest security enhancements, accessibility standards, and your feedback.
>

## jQuery and Handlebars versions

Azure AD B2C page layout uses the following versions of the [jQuery library](https://jquery.com/) and the [Handlebars templates](https://handlebarsjs.com/):

|Element |Page layout version range |jQuery version  |Handlebars Runtime version |Handlebars Compliler version |
|---------|---------|------|--------|----------|
|multifactor |>= 1.2.4 | 3.5.1 | 4.7.6 |4.7.7 |
|            |< 1.2.4 | 3.4.1 |4.0.12 |2.0.1 |
|            |< 1.2.0 | 1.12.4 |
|selfasserted |>= 2.1.4 | 3.5.1 |4.7.6 |4.7.7 |
|            |< 2.1.4 | 3.4.1 |4.0.12 |2.0.1 |
|            |< 1.2.0 | 1.12.4 |
|unifiedssp |>= 2.1.4 | 3.5.1 |4.7.6 |4.7.7 |
|            |< 2.1.4 | 3.4.1 |4.0.12 |2.0.1 |
|            |< 1.2.0 | 1.12.4 |
|globalexception |>= 1.2.1 | 3.5.1 |4.7.6 |4.7.7 |
|            |< 1.2.1 | 3.4.1 |4.0.12 |2.0.1 |
|            |< 1.2.0 | 1.12.4 |
|providerselection |>= 1.2.1 | 3.5.1 |4.7.6 |4.7.7 |
|            |< 1.2.1 | 3.4.1 |4.0.12 |2.0.1 |
|            |< 1.2.0 | 1.12.4 |
|claimsconsent |>= 1.2.1 | 3.5.1 |4.7.6 |4.7.7 |
|            |< 1.2.1 | 3.4.1 |4.0.12 |2.0.1 |
|            |< 1.2.0 | 1.12.4 |
|unifiedssd |>= 1.2.1 | 3.5.1 |4.7.6 |4.7.7 |
|            |< 1.2.1 | 3.4.1 |4.0.12 |2.0.1 |
|            |< 1.2.0 | 1.12.4 |

## Self-asserted page (selfasserted)

**2.1.8**

- The claim name is added to the `class` attribute of the `<li>` HTML element that surrounding the user's attribute input elements. The class name allows you to create a CSS selector to select the parent `<li>` for a certain user attribute input element. The following HTML markup shows the class attribute for the sign-up page:
  
  ```html
  <div id="attributeList" class="attr">
    <ul>
      <li class="EmailBox email_li">...</li>
      <li class="Password newPassword_li">...</li>
      <li class="Password reenterPassword_li">...</li>
      <li class="TextBox displayName_li">...</li>
      <li class="TextBox givenName_li">...</li>
      <li class="TextBox surname_li">...</li>
      <li class="TextBox extension_age_li">...</li>
    </ul>
  </div>
  ```
**2.1.7**
- Fixed a language encoding issue that is causing the request to fail.
- Fixed an accessibility bug to show inline error messages only on form submission.

**2.1.6**
- Fixed password error get cleared when typing too quickly on a different field.

**2.1.5**
- Fixed cursor jumps issue on iOS when editing in the middle of the text.

**2.1.4**
- Updated jQuery version to 3.5.1.
- Updated HandlebarJS version to 4.7.6.

**2.1.3**
- Security fixes.

**2.1.2**
- Fixed the localization encoding issue for languages such as Spanish and French.

**2.1.1**

- Added a UXString `heading` in addition to `intro` to display on the page as a title. This is hidden by default.
- Added support for saving passwords to iCloud Keychain.
- Added support for using policy or the QueryString parameter `pageFlavor` to select the layout (classic, oceanBlue, or slateGray).
- Added disclaimers on self-asserted page.
- Focus is now placed on the first editable field when the page loads.
- Focus is now placed on the first error field when multiple fields have errors.
- Focus is now placed on the 'change' button after the email verification code is verified.

**2.1.0**

- Localization and accessibility fixes.

**2.0.0**

- Added support for [display controls](display-controls.md) in custom policies.

**1.2.0**

- The username/email and password fields now use the `form` HTML element to allow Edge and Internet Explorer (IE) to properly save this information.
- Added a configurable user input validation delay for improved user experience.
- Accessibility fixes
- Fixed an accessibility issue so that error messages are now read by Narrator. 
- Focus is now placed on the password field after the email is verified.
- Removed `autofocus` from the checkbox control. 
- Added support for a display control for phone number verification.
- You can now add the `data-preload="true"` attribute [in your HTML tags](customize-ui-with-html.md#guidelines-for-using-custom-page-content)
  - Load linked CSS files at the same time as your HTML template so it doesn't 'flicker' between loading the files.
  - Control the order in which your `script` tags are fetched and executed before the page load.
- Email field is now `type=email` and mobile keyboards will provide the correct suggestions.
- Support for Chrome translate.
- Added support for company branding in user flow pages.

**1.1.0**

- Removed cancel alert
- CSS class for error elements
- Show/hide error logic improved
- Default CSS removed

**1.0.0**

- Initial release

## Unified sign-in sign-up page with password reset link (unifiedssp)

> [!TIP]
> If you localize your page to support multiple locales, or languages in a user flow. The [localization IDs](localization-string-ids.md) article provides the list of localization IDs that you can use for the page version you select.

**2.1.5**
- Fixed an issue on tab order when idp selector template is used on sign in page.
- Fixed an encoding issue on sign-in link text.

**2.1.4**
- Updated jQuery version to 3.5.1.
- Updated HandlebarJS version to 4.7.6.

**2.1.3**
- Security fixes.
- Minor bug fixes.

**2.1.2**
- Fixed the localization encoding issue for languages such as Spanish and French.
- Allowing the "forgot password" link to use as claims exchange. For more information, see [Self-service password reset](add-password-reset-policy.md#self-service-password-reset-recommended).

**2.1.1**
- Added a UXString `heading` in addition to `intro` to display on the page as a title. This is hidden by default.
- Added support for using policy or the QueryString parameter `pageFlavor` to select the layout (classic, oceanBlue, or slateGray).
- Added support for saving passwords to iCloud Keychain.
- Focus is now placed on the first error field when multiple fields have errors.
- Focus is now placed on the first editable field when the page loads.
- Added a new location for the claims provider selection link `bottomUnderFormClaimsProviderSelections`.
- Removed UXStrings that are no longer used.

**2.1.0**

- Added support for multiple sign-up links.
- Added support for user input validation according to the predicate rules defined in the policy.
- When the [sign-in option](sign-in-options.md) is set to Email, the sign-in header presents "Sign in with your sign in name". The username field presents "Sign in name". For more information, see [localization](localization-string-ids.md#sign-up-or-sign-in-page-elements).

**1.2.0**

- The username/email and password fields now use the `form` HTML element to allow Edge and Internet Explorer (IE) to properly save this information.
- Accessibility fixes
- You can now add the `data-preload="true"` attribute [in your HTML tags](customize-ui-with-html.md#guidelines-for-using-custom-page-content) to control the load order for CSS and JavaScript.
  - Load linked CSS files at the same time as your HTML template so it doesn't 'flicker' between loading the files.
  - Control the order in which your `script` tags are fetched and executed before the page load.
- Email field is now `type=email` and mobile keyboards will provide the correct suggestions.
- Support for Chrome translate.
- Added support for tenant branding in user flow pages.

**1.1.0**

- Added keep me signed in (KMSI) control

**1.0.0**

- Initial release

## MFA page (multifactor)

**1.2.5**
- Fixed a language encoding issue that is causing the request to fail.

**1.2.4**
- Updated jQuery version to 3.5.1.
- Updated HandlebarJS version to 4.7.6.

**1.2.3**
- Allowing tooltip string override via language localization.
- Security fixes.
- Minor bug fixes.

**1.2.2**
- Fixed an issue with auto-filling the verification code when using iOS.
- Fixed an issue with redirecting a token to the relying party from Android Webview. 
- Added a UXString `heading` in addition to `intro` to display on the page as a title. This is hidden by default.  
- Added support for using policy or the QueryString parameter `pageFlavor` to select the layout (classic, oceanBlue, or slateGray).

**1.2.1**

- Accessibility fixes on default templates

**1.2.0**

- Accessibility fixes
- You can now add the `data-preload="true"` attribute [in your HTML tags](customize-ui-with-html.md#guidelines-for-using-custom-page-content) to control the load order for CSS and JavaScript.
  - Load linked CSS files at the same time as your HTML template so it doesn't 'flicker' between loading the files.
  - Control the order in which your `script` tags are fetched and executed before the page load.
- Email field is now `type=email` and mobile keyboards will provide the correct suggestions
- Support for Chrome translate.
- Added support for tenant branding in user flow pages.

**1.1.0**

- 'Confirm Code' button removed
- The input field for the code now only takes input up to six (6) characters
- The page will automatically attempt to verify the code entered when a 6-digit code is entered, without any button having to be clicked
- If the code is wrong, the input field is automatically cleared
- After three (3) attempts with an incorrect code, B2C sends an error back to the relying party
- Accessibility fixes
- Default CSS removed

**1.0.0**

- Initial release

## Exception Page (globalexception)

**1.2.1**
- Updated jQuery version to 3.5.1.
- Updated HandlebarJS version to 4.7.6.

**1.2.0**

- Accessibility fixes
- You can now add the `data-preload="true"` attribute [in your HTML tags](customize-ui-with-html.md#guidelines-for-using-custom-page-content) to control the load order for CSS and JavaScript.
  - Load linked CSS files at the same time as your HTML template so it doesn't 'flicker' between loading the files.
  - Control the order in which your `script` tags are fetched and executed before the page load.
- Email field is now `type=email` and mobile keyboards will provide the correct suggestions
- Support for Chrome translate

**1.1.0**

- Accessibility fix
- Removed the default message when there is no contact from the policy
- Default CSS removed

**1.0.0**

- Initial release

## Other pages (ProviderSelection, ClaimsConsent, UnifiedSSD)

**1.2.1**
- Updated jQuery version to 3.5.1.
- Updated HandlebarJS version to 4.7.6.

**1.2.0**

- Accessibility fixes
- You can now add the `data-preload="true"` attribute [in your HTML tags](customize-ui-with-html.md#guidelines-for-using-custom-page-content) to control the load order for CSS and JavaScript.
  - Load linked CSS files at the same time as your HTML template so it doesn't 'flicker' between loading the files.
  - Control the order in which your `script` tags are fetched and executed before the page load.
- Email field is now `type=email` and mobile keyboards will provide the correct suggestions
- Support for Chrome translate

**1.0.0**

- Initial release

## Next steps

For details on how to customize the user interface of your applications in custom policies, see [Customize the user interface of your application using a custom policy](customize-ui-with-html.md).
