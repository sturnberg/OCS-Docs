---
uid: identityConsent
---

# AAD Consent to OSIsoft Applications

You have chosen to use your organization’s existing Azure Active Directory (AAD) to sign in to your
OSIsoft Cloud Services (OCS) account. In order to proceed, you must complete the consent process to allow your OCS tenant to access your AAD tenant and directory information for authentication. This consent process involves your AAD administrator granting permissions for OCS Identity to sign in and read user profile basic information (delegated permission).

Completing the neccesary consent process involves these steps:

1. For a new tenant, an email will be sent to your AAD administrator who has the privileges to grant OCS access to your AAD. For an existing tenant with access to your AAD tenant, skip to step 6. Note that if your administrator agrees with only one of the two consent emails required, your account will remain in a partially-consented state.
2. Your AAD administrator will click on the link provided in the email which will bring them to a login page. Your administrator will need to log in as a user with the Global Administrator role on your AAD.
3. Upon successful login, your administrator will be prompted to grant consent for a single application: OCS Identity.
4. Your administrator should select the box "Consent on behalf of the organization" before clicking the consent button.
5. OSIsoft will get a confirmation that the consent process has been completed.
6. Your administrator will get an email about consent to advanced integration with your OCS tenant and your AAD information. 
7. Your administrator should agree to the advanced integration by clicking the consent button.
8. A final email will be sent to the initial user who signed up for the account, informing them that they can sign in with their AAD account.
7. At that point, this initial user will be able to use the link provided to activate his profile and sign in your OCS account.
