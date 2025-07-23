# The Tenant Log-in Loop

If you run into MS authentication loop, the following steps may
troubleshoot the error

## Background

The loop is when you are requested to fill in more MFA information, but end up getting denied or it says all info is
filled in, but end up coming back to the same login prompt.  
![](img/TheLoop-More_information_required.png)  
![](img/TheLoop-No_method_available.png)

## First try

1. You get the request for more information, and if you select it you might get
2. Click on 'Use a different account'
3. In the list, pick the same account you used when getting the loop.
4. If you are lucky, you have now passed The Loop.

## Break-glass Account

1. Reset the Authentication Method for the User
    - Try removing all existing authentication methods for the user in Azure AD and then re-adding the preferred method.
    - Go to Azure Active Directory > Users > All Users, select the specific user, and under Authentication methods,
      remove any existing methods.
    - After that, reconfigure the authentication method from scratch to ensure it’s set as the default.
2. Use PowerShell to Reset Authentication Information
    - Using PowerShell can sometimes clear out any configurations causing the loop.
    - Install the AzureAD module with powershell:
      `Install-Module AzureAD`
    - Connect to your Azure account with powershell:
      `Connect-AzureAD`
    - Reset MFA or the default authentication method for the user with appropriate commands in powershell, such as:
      `Set-MsolUser -UserPrincipalName user@domain.com -StrongAuthenticationRequirements @()`
    - Try setting up the authentication method again after this reset.
3. Check for Security Defaults or Conditional Access Policies Conflicts
    - If Security Defaults are enabled in your Azure AD tenant, they can sometimes conflict with custom MFA or
      authentication configurations.
    - Go to `Azure Active Directory > Properties` and look under `Manage Security Defaults`. If Security Defaults are
      enabled, consider disabling them temporarily to see if that resolves the issue.
    - If you have Conditional Access policies enforcing specific authentication requirements, review them to ensure they
      aren’t forcing different settings than intended.
4. Temporary Workaround: Use a Different Authentication Method
    - Temporarily switch to a different authentication method (e.g., Authenticator App instead of Phone SMS or Email).
    - Go to Security info for the account (https://mysignins.microsoft.com/security-info) and add an alternate
      authentication method. Set it as the default to see if this resolves the loop.
    - If successful, reattempt setting up the original authentication method and default.
5. Clear User State and Re-Enable Authentication Settings
    - In the Azure AD > Users > Multi-Factor Authentication settings page, you can reset the user’s MFA state.
    - After resetting, try re-enabling and setting up the default authentication method.
6. Contact Microsoft Support
    - If the issue persists after all troubleshooting, it’s best to contact Microsoft Support. This issue might be due
      to a configuration on Microsoft’s end or an issue within your tenant, and they can provide further assistance or
      escalate as needed.

