# Re-Security-Pro----Plan-implement-and-administer-Conditional-Access
Conditional Access gives a fine granularity of control over which users and identities can perform specific activities, access resources, and ensure data and systems are safe. With the introduction of Microsoft Entra Agent ID control, now extends to AI agents


### Introduction
Unit 1/12
Conditional Access gives a fine granularity of control over which users and identities can perform specific activities, access resources, and ensure data and systems are safe. With the introduction of Microsoft Entra Agent ID control, now extends to AI agents—you apply the same Zero Trust principles to agent identities that you apply to users and workload identities.

Learning objectives
In this module, you will:

Plan and implement security defaults.
Plan Conditional Access policies.
Implement Conditional Access policy controls and assignments (targeting, applications, and conditions).
Test and troubleshoot Conditional Access policies.
Implement application controls.
Implement session management.
Configure continuous access evaluation.
Identify how agent identities are protected using Conditional Access.


### Plan security defaults

Summarize

Turn into podcast
Unit 2/12
Managing security can be difficult with common identity-related attacks like password spray, replay, and phishing becoming more popular. Security defaults provide secure default settings that Microsoft manages on behalf of organizations to keep customers safe until organizations are ready to manage their own identity security story. Security defaults provide preconfigured security settings, such as:

Requiring all users to register for multifactor authentication.

Requiring administrators to perform multifactor authentication.

Blocking legacy authentication protocols.

Requiring users to perform multifactor authentication when necessary.

Protecting privileged activities like access to the Azure portal.

Screenshot of the Microsoft Entra admin center with the toggle to enable security defaults.

Availability
Microsoft security defaults are available to everyone. The goal is to ensure that all organizations have a basic level of security enabled at no extra cost. If your tenant was created on or after October 22, 2019, security defaults might already be enabled. To protect all users, security defaults are enabled on all new tenants at creation.

To enable or disable security defaults, sign in to the Microsoft Entra admin center(https://entra.microsoft.com/) as at least a Conditional Access Administrator, then browse to Entra ID > Overview > Properties, and select Manage security defaults.

Who's it for?

**Who should use security defaults?**                                   **Who shouldn't use security defaults?**

**Organizations that want to increase their security posture but don't know how or where to start**------------**Organizations currently using Conditional Access policies to bring signals together, make decisions, and enforce organizational policies**
	
**Organizations utilizing the free tier of Microsoft Entra ID Licensing**----------------------	**Organization with Microsoft Entra ID Premium licenses**
-----------------------------------------------------------------------------**Organizations with complex security requirements that warrant using Conditional Access**






Policies enforced
Unified multifactor authentication registration
All users in your tenant must register for multifactor authentication (MFA) using the Microsoft Authenticator app. Registration is required immediately—there's no grace period. When users sign in after security defaults are enabled, they're prompted to register before they can access any resources. The MFA prompt uses number matching, where users enter a number displayed on screen into the Microsoft Authenticator app, which helps prevent MFA fatigue attacks.

Protecting administrators
Users with privileged access often increase access to your environment. Due to the power these accounts have, you should treat them with special care. One common method to improve the protection of privileged accounts is to require a stronger form of account verification for sign-in. In Microsoft Entra ID, you can get a stronger account verification by requiring multifactor authentication.

After registration with multifactor authentication is finished, the following Microsoft Entra administrator roles are required to perform other authentication every time they sign in:

Global Administrator
Application Administrator
Authentication Administrator
Authentication Policy Administrator
Billing Administrator
Cloud Application Administrator
Conditional Access Administrator
Exchange Administrator
Helpdesk Administrator
Identity Governance Administrator
Password Administrator
Privileged Authentication Administrator
Privileged Role Administrator
Security Administrator
SharePoint Administrator
User Administrator
Protecting all users
We tend to think that administrator accounts are the only accounts that need extra layers of authentication. Administrators have broad access to sensitive information and can make changes to subscription-wide settings. But attackers frequently target end users.

After these attackers gain access, they can request access to privileged information on behalf of the original account holder. They can even download the entire directory to perform a phishing attack on your whole organization.

One common method to improve protection for all users is to require a stronger form of account verification, such as multifactor authentication, for everyone. After users complete Multifactor Authentication registration, they'll be prompted for extra authentication whenever necessary. This functionality protects all applications registered with Microsoft Entra ID, including SaaS applications.

Blocking legacy authentication
To give your users easy access to your cloud apps, Microsoft Entra ID supports various authentication protocols, including legacy authentication. Legacy authentication is an authentication request made by:

Clients that don't use modern authentication (for example, an Office 2010 client). Modern authentication encompasses clients that implement protocols, such as OAuth 2.0, to support features like multifactor authentication and smart cards. Legacy authentication typically only supports less secure mechanisms like passwords.
Client that uses mail protocols such as IMAP, SMTP, or POP3.
Today, most compromising sign-in attempts come from legacy authentication. Legacy authentication doesn't support multifactor authentication. Even if you have a multifactor authentication policy enabled on your directory, an attacker can authenticate by using an older protocol and bypass multifactor authentication.

After security defaults are enabled in your tenant, all authentication requests made by an older protocol will be blocked. Security defaults blocks Exchange Active Sync basic authentication.





### Exercise - Work with security defaults
Unit 3/12
In this exercise, try enabling security defaults.

[!Note] Security Defaults are enabled on new subscriptions, so you can review the process of enabling and disabling.

To enable security defaults in your directory:

Browse to the Microsoft Entra admin center and sign in as a Security administrator, or a Conditional Access administrator.

Select the Show portal menu hamburger icon and then select Identity - Overview.

Screenshot of the Microsoft Entra admin center menu with Identity - Overview - Properties selected.

In the left navigation, in the Manage section, select Properties.

At the bottom of the Properties dialog, select Manage Security defaults.

Set the Enable Security defaults toggle to Yes.

Select Save.

Disabling security defaults
Organizations that choose to implement Conditional Access policies that replace security defaults must disable security defaults.

To disable security defaults in your directory:

Browse to the Azure portal and sign in using an Administrator account for the directory.

Select the Show portal menu hamburger icon and then select Microsoft Entra ID.

At the bottom of the Properties dialog, select Manage Security defaults.

Set the Enable security defaults toggle to No.

Screenshot of the security defaults being disabled and selection of the required reason for disabling.

Select Save.



### Plan Conditional Access policies

Summarize

Turn into podcast
Unit 4/12
Planning your Conditional Access deployment is critical to achieving your organization's access strategy for apps and resources.

In a mobile-first, cloud-first world, your users access your organization's resources from anywhere using various devices and apps. As a result, focusing on who can access a resource is no longer enough. You also need to consider where the user is, the device being used, the resource being accessed, and more.

Microsoft Entra Conditional Access (CA) analyzes signals, such as user, device, and location, to automate decisions and enforce organizational access policies for resource. You can use CA policies to apply access controls like multifactor authentication (MFA). CA policies allow you to prompt users for MFA when needed for security and to stay out of users’ way when not needed.

Diagram of how Conditional Access works. Centralize identity provider verifies rules before access is granted.

Although security defaults ensure a basic level of security, your organization needs more flexibility than security defaults offer. You can use CA to customize security defaults with more granularities and to configure new policies that meet your requirements.

Benefits
The benefits of deploying CA are:

Increase productivity - only interrupt users with a sign-in condition like MFA when one or more signals warrants it. CA policies allow you to control when users are prompted for MFA, when access is blocked, and when they must use a trusted device.
Manage risk - automating risk assessment with policy conditions means risky sign-ins are at once identified and remediated or blocked. Coupling Conditional Access with Identity Protection, which detects anomalies and suspicious events, allows you to target when access to resources is blocked or gated.
Address compliance and governance - Conditional access enables you to audit access to applications, present terms of use for consent, and restrict access based on compliance policies.
Manage cost - moving access policies to Microsoft Entra ID reduces the reliance on custom or on-premises solutions for CA and their infrastructure costs.
Zero Trust - Conditional Access helps you move toward a zero-trust environment.
Understand Conditional Access policy components
CA policies are if-then statements: If an assignment is met, then apply these access controls. When the admin configures CA policies, conditions are called assignments. CA policies allow you to enforce access controls on your organization’s apps based on certain assignments.

Screenshot of the conditional access dialog with the policy creation screen open for configuration.

Assignments define the users and groups to be affected by the policy, the cloud apps or actions to which the policy will apply, and the conditions under which the policy will apply. Access control settings grant or block access to different cloud apps and can enable limited experiences within specific cloud apps.

Some common questions about assignments, access controls, and session controls:

Users and Groups: Which users and groups will be included in or excluded from the policy? Does this policy include all users, specific group of users, directory roles, or external users?
Cloud apps or actions: What application(s) will the policy apply to? What user actions will be subject to this policy?
Conditions: Which device platforms will be included in or excluded from the policy? What are the organization’s trusted locations?
Access controls: Do you want to grant access to resources by implementing requirements such as MFA, devices marked as compliant, or Microsoft Entra hybrid joined devices?
Session controls: Do you want to control access to cloud apps by implementing requirements such as app enforced permissions or Conditional Access App Control?
With the introduction of Microsoft Entra Agent ID, agent identities are now first-class principals in Microsoft Entra ID. Like users or service principals, agents can be targeted by Conditional Access policies — allowing you to apply the same Zero Trust controls to AI agents that you apply to human identities. You treat agent identities similarly to how you treat workload identities: scope policies by identity type, enforce appropriate access controls, and exclude emergency or trusted agents where necessary.

Access token issuance
Access tokens enable clients to securely call protected web APIs, and they're used by web APIs to perform authentication and authorization. Per the OAuth specification, access tokens are opaque strings without a set format. Some identity providers (IDPs) use GUIDs; others use encrypted blobs. The Microsoft identity platform uses a variety of access token formats depending on the configuration of the API that accepts the token.

It’s important to understand how access tokens are issued.

Diagram of the flow of issues an access token for conditional access, and how it's used.

Note
If no assignment is required, and no CA policy is in effect, the default behavior is to issue an access token.

For example, consider a policy where:

IF user is in Group 1, THEN force MFA to access App 1.

IF a user not in Group 1 attempts to access the app, THEN the “if" condition is met, and a token is issued. Excluding users outside of Group 1 requires a separate policy to block all other users.

Follow best practices
The Conditional Access framework provides you with great configuration flexibility. However, great flexibility also means you should carefully review each configuration policy before releasing it to avoid undesirable results.

Set up emergency access accounts
If you misconfigure a policy, it can lock the organizations out of the Azure portal. Mitigate the accidental administrator lockout by creating two or more emergency access accounts in your organization. You'll learn more about emergency access accounts later in this course.

Set up report-only mode
It can be difficult to predict the number and names of users affected by common deployment initiatives such as:

Blocking legacy authentication.
Requiring MFA.
Implementing sign-in risk policies.
Report-only mode allows administrators to evaluate the CA policies before enabling them in their environment.

Exclude countries from which you never expect a sign-in
Microsoft Entra ID allows you to create named locations. Create a named location that includes all of the countries from which you would never expect a sign-in to occur. Then create a policy for all apps that blocks sign in from that named location. Be sure to exempt your administrators from this policy.

Common policies
When planning your CA policy solution, assess whether you need to create policies to achieve the following outcomes.

Require MFA. Common use cases include requiring MFA by admins, to specific apps, for all users, or from network locations you don't trust.

Respond to potentially compromised accounts. Three default policies can be enabled: require all users to register for MFA, require a password change for users who are high-risk, and require MFA for users with medium or high sign-in risk.

Require managed devices. The proliferation of supported devices to access your cloud resources helps to improve the productivity of your users. You probably don't want certain resources in your environment to be accessed by devices with an unknown protection level. For those resources, require that users can only access them using a managed device.

Require approved client applications. Employees use their mobile devices for both personal and work tasks. For BYOD scenarios, you must decide whether to manage the entire device or just the data on it. If managing only data and access, you can require approved cloud apps that can protect your corporate data.

Block access. Blocking access overrides all other assignments for a user and has the power to block your entire organization from signing on to your tenant. It can be used, for example, when you're migrating an app to Microsoft Entra ID, but you aren't ready for anyone to sign in to it yet. You can also block certain network locations from accessing your cloud apps or block apps using legacy authentication from accessing your tenant resources.

Important
If you create a policy to block access for all users, be sure to exclude emergency access accounts and consider excluding all administrators from the policy.

Build and test policies
At each stage of your deployment, ensure that you're evaluating that results are as expected.

When new policies are ready, deploy them in phases in the production environment:

Provide internal change communication to end users.
Start with a small set of users, and verify that the policy behaves as expected.
When you expand a policy to include more users, continue to exclude all administrators. Excluding administrators ensures that someone still has access to a policy if a change is required.
Apply a policy to all users only after it's thoroughly tested. Ensure you have at least one administrator account to which a policy doesn't apply.
Create test users
Create a set of test users that reflect the users in your production environment. Creating test users enables you to verify policies work as expected before you apply to real users and potentially disrupt their access to apps and resources.

Some organizations have test tenants for this purpose. However, it can be difficult to recreate all conditions and apps in a test tenant to fully test the outcome of a policy.

**Create a test plan**
The test plan is important to have a comparison between the expected results and the actual results. You should always have an expectation before testing something. The following table outlines example test cases. Adjust the scenarios and expected results based on how your CA policies are configured.


| Policy                          | Scenario                                  | Expected Result                      |
| ------------------------------- | ----------------------------------------- | ------------------------------------ |
| Require MFA when working        | User signs in from trusted location       | No MFA (or optional based on policy) |
| Require MFA when working        | User signs in from untrusted location     | MFA required                         |
| Require MFA for Admins          | Global Admin signs in                     | MFA required                         |
| Risky Sign-ins                  | User signs in from risky browser/location | MFA required                         |
| Device Management               | Authorized device                         | Access granted                       |
| Device Management               | Unauthorized device                       | Access blocked                       |
| Password Change for Risky Users | Compromised credentials detected          | Password change or block access      |


**License requirements**
Free Microsoft Entra ID - No Conditional Access
Free Office 365 subscription - No Conditional Access
Microsoft Entra ID Premium 1 (or Microsoft 365 E3 and up) - Conditional access work based on standard rules
Microsoft Entra ID Premium 2 - Conditional Access, and you get the ability to use Risky sign-in, Risky Users, and risk-based sign-in options as well (from Identity Protection)






### Implement Conditional Access policy controls and assignments

Summarize

Turn into podcast
Unit 5/12
Conditional Access is an advanced capability of Microsoft Entra ID that enables you to specify detailed policies that control who can access your resources. Using Conditional Access, you can protect your applications by limiting users' access based on signals like group membership, device compliance, network location, and sign-in risk.

Create a Conditional Access policy
This is an abbreviated guide to creating a Conditional Access policy. Full documentation is available at What is Conditional Access?.

To create a new policy:

Sign in to the Microsoft Entra admin center as at least a Conditional Access Administrator.
Browse to Protection > Conditional Access.
Select + New policy.
Give the policy a meaningful name.
Configure Assignments — select the users, groups, or roles the policy applies to.
Configure Target resources — select the cloud apps or user actions the policy covers.
Configure any additional Conditions such as sign-in risk, device platform, or location.
Under Access controls, configure the Grant or Session controls to apply.
Set Enable policy to Report-only to test impact before enabling, then select Create.
Microsoft recommends starting all new policies in report-only mode. Monitor sign-in logs to verify expected behavior before switching the policy to On.

Sign-in risk-based Conditional Access
Most users have a normal behavior that can be tracked. When they fall outside of this norm, it could be risky to allow them to just sign in. You want to block that user or ask them to perform multifactor authentication to prove that they are really who they say they are.

A sign-in risk represents the probability that a given authentication request isn't authorized by the identity owner. Organizations with Microsoft Entra ID Premium P2 licenses can create Conditional Access policies incorporating Microsoft Entra Identity Protection sign-in risk detections.

This policy can be assigned either through Conditional Access itself or through Microsoft Entra Identity Protection. Organizations should choose one of two options to enable a sign-in risk-based Conditional Access policy requiring a secure password change.

User risk-based Conditional Access
Microsoft works with researchers, law enforcement, various security teams at Microsoft, and other trusted sources to find leaked username and password pairs. Organizations with Microsoft Entra ID Premium P2 licenses can create Conditional Access policies incorporating Microsoft Entra Identity Protection user risk detections.

Like sign-in risk-based Conditional Access, this policy can be assigned either through Conditional Access itself or through Microsoft Entra Identity Protection.

Securing security info registration
Securing when and how users register for multifactor authentication and self-service password reset is now possible with user actions in Conditional Access policy. This preview feature is available to organizations that have enabled the combined registration preview. This functionality might be enabled in organizations where they want to use conditions like trusted network location to restrict access to register for multifactor authentication and self-service password reset (SSPR).

Create a policy to require registration from a trusted location
The following policy applies to all selected users who attempt to register using the combined registration experience, and it blocks access unless they are connecting from a location marked as a trusted network.

In the Microsoft Entra admin center, browse to Protection, then Conditional Access.

Select + Create new policy.

In Name, Enter a Name for this policy. For example, Combined Security Info Registration on Trusted Networks.

Under Assignments, select Users and groups, and select the users and groups you want this policy to apply to.

Under Exclude, select Users and groups and choose your organization's emergency access or break-glass accounts.
Select Done.
Note
If you were targeting AI agents instead of users, you would select Workload identities in the Assignments area and choose your agent identity from Microsoft Entra Agent ID at this step. The rest of the policy structure remains the same.

Under Cloud apps or actions, select User actions, check Register security information.

Under Conditions, select Locations.

Configure Yes.
Include Any location.
Exclude All trusted locations.
Select Done on the Locations screen.
Select Done on the Conditions screen.
Under Conditions, in Client apps (Preview), set Configure to Yes, and select Done.

Under Access controls, select Grant.

Select Block access.
Then use the Select option.
Set Enable policy to On.

Then select Save.

At step 6 in this policy, organizations have choices they can make. The policy above requires registration from a trusted network location. Organizations can choose to utilize any available conditions in place of Locations. Remember that this policy is a block policy, so anything included is blocked.

You can choose to use device state instead of location in step 6 above:

Under Conditions, select Device state (Preview).
Configure Yes.
Include All device state.
Exclude Device Hybrid Microsoft Entra joined and/or Device marked as compliant.
Select Done on the Locations screen.
Select Done on the Conditions screen.
Block access by location
With the location condition in Conditional Access, you can control access to your cloud apps based on the network location of a user. The location condition is commonly used to block access from countries/regions where your organization knows traffic should not come from.

Define locations
Sign in to the Microsoft Entra admin portal as a Security Administrator, or Conditional Access Administrator.

Browse to Protection, then Conditional Access, then Named locations.

Choose New location.

Give your location a name.

Choose IP ranges if you know the specific externally accessible IPv4 address ranges that make up that location or Countries/Regions.

Provide the IP ranges or select the Countries/Regions for the location you are specifying.
If you choose Countries/Regions, you can optionally choose to include unknown areas.
Choose Save.

Create a Conditional Access policy
Sign in to the Microsoft Entra admin center as a Security Administrator, or Conditional Access Administrator.

Browse to Protection, then Conditional Access.

Select + Create new policy.

Give your policy a name. We recommend that organizations create a meaningful standard for the names of their policies.

Under Assignments, select Users and groups.

Under Include, select All users.
Under Exclude, select Users and groups and choose your organization's emergency access or break-glass accounts.
Select Done.
Under Cloud apps or actions, then Include, and select All cloud apps.

Under Conditions, then Location.

Set Configure to Yes.
Under Include, select Selected locations.
Select the blocked location you created for your organization.
Choose Select.
Under Access controls, then select Block Access, and select Select.

Confirm your settings and set Enable policy to On.

Select Create to create Conditional Access Policy.

Require compliant devices
Organizations that have deployed Microsoft Intune can use the information returned from their devices to identify devices that meet compliance requirements, such as:

Requiring a PIN to unlock.
Requiring device encryption.
Requiring a minimum or maximum operating system version.
Requiring a device is not jailbroken or rooted.
This policy compliance information is forwarded to Microsoft Entra ID where Conditional Access can make decisions to grant or block access to resources.

Create a Conditional Access policy
The following steps will help create a Conditional Access policy to require devices accessing resources be marked as compliant with your organization's Intune compliance policies.

Sign in to the Microsoft Entra admin center as a Security Administrator, or Conditional Access Administrator.

Browse to Protection, then Conditional Access.

Select + Create new policy.

Give your policy a name. We recommend that organizations create a meaningful standard for the names of their policies.

Under Assignments, select Users and groups.

Under Include, select All users.
Under Exclude, select Users and groups and choose your organization's emergency access or break-glass accounts.
Select Done.
Under Cloud apps or actions, then Include, and select All cloud apps.

If you must exclude specific applications from your policy, you can choose them from the Exclude tab under Select excluded cloud apps and choose Select.
Select Done.
Under Conditions, then Client apps (Preview), then Select the client apps this policy will apply to, leave all defaults selected and select Done.

Under Access controls, then Grant, select Require device to be marked as compliant.

Select Select.

Confirm your settings and set Enable policy to On.

Select Create to create to enable your policy.

Note
You can enroll your new devices to Intune even if you select Require device to be marked as compliant for All users and All cloud apps using the steps above. Require device to be marked as compliant control does not block Intune enrollment.

Known behavior
On Windows 7, iOS, Android, macOS, and some third-party web browsers, Microsoft Entra ID identifies the device using a client certificate that is provisioned when the device is registered with Microsoft Entra ID. When a user first signs in through the browser, the user is prompted to select the certificate. The end user must select this certificate before they can continue to use the browser.

Block access
For organizations with a conservative cloud migration approach, the block all policy is an option that can be used.

Warning
Misconfiguration of a block policy can lead to organizations being locked out of the Azure portal.

Policies like these can have unintended side effects. Proper testing and validation are vital before enabling. Administrators should utilize tools such as Conditional Access report-only mode and the What If tool in Conditional Access.

User exclusions
Conditional Access policies are powerful tools. We recommend excluding the following accounts from your policy:

Emergency access or break-glass accounts to prevent tenant-wide account lockout. In the unlikely scenario that all administrators are locked out of your tenant, your emergency-access administrative account can be used to sign into the tenant and take steps to recover access.

Service accounts and service principals, such as the Microsoft Entra Connect Sync Account. Service accounts are non-interactive accounts that are not tied to any particular user. They are normally used by back-end services allowing programmatic access to applications, but they are also used to sign in to systems for administrative purposes. Service accounts like these should be excluded since MFA can't be completed programmatically. Calls made by service principals are not blocked by Conditional Access.

If your organization has these accounts in use in scripts or code, consider replacing them with managed identities. As a temporary workaround, you can exclude these specific accounts from the baseline policy.
Agent identities: AI agents registered in Microsoft Entra Agent ID can be targeted by or excluded from Conditional Access policies just like service principals. Ensure any trusted agents that require uninterrupted access are explicitly excluded, and review agent-targeted policies alongside your workload identity policies.

Conditional Access Terms of Use (TOU)
Screenshot of the Identity Governance dialog to create new Terms of Use for your cloud solutions.

You can create Terms of Use (TOU) for your site in the Identity Governance tools. Launch the identity governance app, and choose Terms of use from the menu. You have to supply a PDF file with the terms for the user. You can set up several rules like when the terms will expire, or whether the user has to open them before accepting. Once created, you can build a custom conditional rule right in identity governance. Or you can save the terms and use Conditional Access in Microsoft Entra ID. To create new Terms of use you fill in the above dialog.

Screenshot of the Microsoft Entra conditional access setup page that shows adding Terms-of-Use rules for being able to access resources.

The linking of consent (accept terms before access) and conditional access is getting more and more traction. Organizations get the ability to enforce a user to consent to the terms of use. Additionally, organizations can expire the consent given or change the terms of use, and request the user attests again.

Before accessing certain cloud apps in your environment, you might want to get consent from users in form of accepting your terms of use (ToU). Microsoft Entra Conditional Access provides you with:

A simple method to configure ToU
The option to require accepting your terms of use through a Conditional Access policy


### Exercise - Implement Conditional Access policies roles and assignments
Unit 6/12
In this exercise, create a conditional access policy.

Microsoft Entra Conditional Access is an advanced feature of Microsoft Entra ID that allows you to specify detailed policies that control who can access your resources. Using Conditional Access, you can protect your applications by limiting users' access based on things like groups, device type, location, and role.

Sign in to the Microsoft Entra admin center using a Global administrator account.

Open the portal menu and then select Identity.

Then select Protection.

On the Security blade, in the left navigation, select Conditional access.

On the top menu, select + Create new policy.

Screenshot of the Conditional Access blade with New policy highlighted.

In the Name box, enter Test app conditional access. This is the name being using for this exercise, you can choose another name if you wish.

Under Assignments, select Users and groups.

On the Include tab, select the Users and groups check box.

In the Select pane, select your administrator account and then select Select.

Select Cloud apps or actions.

Verify Cloud apps is selected and then select Select apps.

In the Select pane, select My apps and then select Select.

Select Conditions and then select Locations.

Under Configure, select Yes and then select Any location.

Under Access controls, select Grant.

In the Grant pane, select Block access and then select Select.

Important
This policy is being configured for the exercise only and is being used to quickly demonstrate a conditional access policy.

Under Enable policy, select On, and then select Create.
Screenshot of a new conditional access policy with enable and create highlighted.

Test the conditional access policy
You should test your conditional access policies to ensure they working as expected.

Open a new browser tab and then browse to https://myapps.microsoft.com.

Your credentials should be passed through.

Verify you are prevented from successfully accessing your My Apps page.

Screenshot of the blocked resource access due to an enabled conditional access policy.

Note
If you are signed in, close the tab, wait 1-2 minutes, and then retry.

Close the tab and return to the Conditional Access blade.

Select the Test app conditional access policy.

Under Enable policy, select Off and then select Save.


### Test and troubleshoot Conditional Access policies

Summarize

Turn into podcast
Unit 7/12
The Conditional Access framework provides you with great configuration flexibility. However, great flexibility also means that you should carefully review each configuration policy before releasing it to avoid undesirable results. In this context, you should pay special attention to assignments affecting complete sets such as all users / groups / cloud apps.

Organizations should avoid the following configurations:

For all users, all cloud apps:

Block access - This configuration blocks your entire organization.
Require Hybrid Microsoft Entra domain joined device - This access-blocking policy also has the potential to block access for all users in your organization if they don't have a hybrid Microsoft Entra joined device.
Require app protection policy - This access-blocking policy also has the potential to block access for all users in your organization if you don't have an Intune policy. If you're an administrator without a client application that has an Intune app protection policy, this policy blocks you from getting back into portals such as Intune and Azure.
For all users, all cloud apps, all device platforms:

Block access - This configuration blocks your entire organization.
Conditional Access sign-in interrupt
The first way is to review the error message that appears. For problems signing in when using a web browser, the error page itself has detailed information. This information alone describes what the problem is and suggests a solution.

Screenshot of the Sign-in error - compliant device required. With a button to cancel or get more information.

In the above error, the message states that the application can only be accessed from devices or client applications that meet the company's mobile device management policy. In this case, the application and device don't meet that policy.

Microsoft Entra sign-in events
The second method to get detailed information about the sign-in interruption is to review the Microsoft Entra sign-in events to see which Conditional Access policy or policies were applied and why.

Find more information about the problem by clicking More Details in the initial error page. Clicking More Details will reveal troubleshooting information that's helpful when searching the Microsoft Entra sign-in events for the specific failure event the user saw or when opening a support incident with Microsoft.

Screenshot of the More details from a Conditional Access interrupted web browser sign-in.

To find out which Conditional Access policy or policies applied and why, do the following steps:

Sign into the Microsoft Entra admin center as a Security Administrator, or Global Reader.

Browse to Identity - Monitoring and Health, then Sign-ins.

Find the event for the sign-in to review. Add or remove filters and columns to filter out unnecessary information.

Add filters to narrow the scope:

Correlation ID when you have a specific event to investigate.

Conditional access to see policy failure and success. Scope your filter to show only failures to limit results.

Username to see information related to specific users.

Date scoped to the time frame in question.

Screenshot of the error message screen. User is selecting the Conditional access filter in the sign-ins log.

Once the sign-in event that corresponds to the user's sign-in failure has been found select the Conditional Access tab, the tab will show the specific policy or policies that resulted in the sign-in interruption.

Information in the Troubleshooting and support tab provides a clear reason as to why a sign-in failed, such as a device that didn't meet compliance requirements.
To investigate further, drill down into the configuration of the policies by clicking on the Policy Name. Clicking the Policy Name will show the policy configuration user interface for the selected policy for review and editing.
The client user and device details that were used for the Conditional Access policy assessment are also available in the Basic Info, Location, Device Info, Authentication Details, and Additional Details tabs of the sign-in event.
Policy details
Selecting the ellipsis on the right side of the policy in a sign-in event brings up policy details. This gives administrators additional information about why a policy was successfully applied or not.

Screenshot of the Sign-in event Conditional Access tab. Waiting for user input.

Screenshot of the Policy details (preview) screen in Microsoft Entra conditional access.

The left side provides details collected at sign-in, and the right side provides details of whether those details satisfy the requirements of the applied Conditional Access policies. Conditional Access policies only apply when all conditions are satisfied or not configured.

If the information in the event isn't enough to understand the sign-in results or adjust the policy to get desired results, then a support incident can be opened. Navigate to that sign-in event's Troubleshooting and support tab and select Create a new support request.

Screenshot of The Troubleshooting and support tab of the Sign-in event. Wizard helps fix issues.

When submitting the incident, provide the request ID and time and date from the sign-in event in the incident submission details. This information will allow Microsoft support to find the event you're concerned about.


### Implement application controls

Summarize

Turn into podcast
Unit 8/12
Conditional Access App Control enables user app access and sessions to be monitored and controlled in real time based on access and session policies. Access and session policies are used within the Microsoft Defender for Cloud Apps portal to further refine filters and set actions to be taken on a user.

Conditional Access App Control
Screenshot of the Conditional Access App Control selected in the conditional access wizard.

Conditional Access App Control uses a reverse proxy architecture and is uniquely integrated with Microsoft Entra Conditional Access. Microsoft Entra Conditional Access allows you to enforce access controls on your organization’s apps based on certain conditions. The conditions define who (user or group of users) and what (which cloud apps) and where (which locations and networks) a Conditional Access policy is applied to. After you’ve determined the conditions, you can route users to Microsoft Defender for Cloud Apps where you can protect data with Conditional Access App Control by applying access and session controls.

With the access and session policies, you can:

Prevent data exfiltration: You can block the download, cut, copy, and print of sensitive documents on, for example, unmanaged devices.
Protect on download: Instead of blocking the download of sensitive documents, you can require documents to be labeled and protected with Azure Information Protection. This action ensures the document is protected and user access is restricted in a potentially risky session.
Prevent upload of unlabeled files: Before a sensitive file is uploaded, distributed, and used by others, it’s important to make sure that the file has the right label and protection. You can ensure that unlabeled files with sensitive content are blocked from being uploaded until the user classifies the content.
Monitor user sessions for compliance: Risky users are monitored when they sign into apps and their actions are logged from within the session. You can investigate and analyze user behavior to understand where, and under what conditions, session policies should be applied in the future.
Block access: You can granularly block access for specific apps and users depending on several risk factors. For example, you can block them if they're using client certificates as a form of device management.
Block custom activities: Some apps have unique scenarios that carry risk, for example, sending messages with sensitive content in apps like Microsoft Teams or Slack. In these kinds of scenarios, you can scan messages for sensitive content and block them in real time.
How to: Require app protection policy and an approved client app for cloud app access with Conditional Access
People regularly use their mobile devices for both personal and work tasks. While making sure staff can be productive, organizations also want to prevent data loss from potentially unsecure applications. With Conditional Access, organizations can restrict access to approved (modern authentication-capable) client apps.

This section presents two scenarios to configure Conditional Access policies for resources like Microsoft 365, Exchange Online, and SharePoint Online.

Note
In order to require approved client apps for iOS and Android devices, these devices must first register in Microsoft Entra ID.

Scenario 1: Microsoft 365 apps require an approved client app
In this scenario, Contoso has decided that users using mobile devices can access all Microsoft 365 services as long as they use approved client apps, like Outlook mobile, OneDrive, and Microsoft Teams. All of their users already sign in with Microsoft Entra credentials and have licenses assigned to them that include Microsoft Entra ID Premium P1 or P2 and Microsoft Intune.

Organizations must complete the following three steps in order to require the use of an approved client app on mobile devices.

Step 1: Policy for Android and iOS based modern authentication clients requiring the use of an approved client application when accessing Exchange Online.

Sign in to the Microsoft Entra admin center as a Security Administrator, or Conditional Access Administrator.

Browse to Identity, then Protection, and then Conditional Access.

Select +Create new policy.

Give your policy a name. We recommend that organizations create a meaningful standard for the names of their policies.

Under Assignments, select Users and groups.

Under Include, select All users or the specific Users and groups you wish to apply this policy to.
Select Done.
Under Cloud apps or actions, then Include, select Office 365.

Under Conditions, select Device platforms.

Set Configure to Yes.
Include Android and iOS.
Under Conditions, select Client apps (preview).

Set Configure to Yes.

Select Mobile apps and desktop clients and Modern authentication clients.

Under Access controls, then Grant, select Grant access, Require approved client app, and select Select.

Confirm your settings and set Enable policy to On.

Select Create to create and enable your policy.

Step 2: Configure an Microsoft Entra Conditional Access policy for Exchange Online with ActiveSync (EAS).

Browse to Identity, then Protection, and then Conditional Access.

Select +Create new policy.

Give your policy a name. We recommend that organizations create a meaningful standard for the names of their policies.

Under Assignments, select Users and groups.

Under Include, select All users or the specific Users and groups you wish to apply this policy to.
Select Done.
Under Cloud apps or actions, then Include, select Office 365 Exchange Online.

Under Conditions:

Client apps (preview):

Set Configure to Yes.
Select Mobile apps and desktop clients and Exchange ActiveSync clients.
Under Access controls, then Grant, select Grant access, Require approved client app, and select Select.

Confirm your settings and set Enable policy to On.

Select Create to create and enable your policy.

Step 3: Configure Intune app protection policy for iOS and Android client applications.

Review the article How to create and assign app protection policies for steps to create app protection policies for Android and iOS.

Scenario 2: Exchange Online and SharePoint Online require an approved client app
In this scenario, Contoso has decided that users can only access email and SharePoint data on mobile devices as long as they use an approved client app like Outlook mobile. All of their users already sign in with Microsoft Entra credentials and have licenses assigned to them that include Microsoft Entra ID Premium P1 or P2 and Microsoft Intune.

Organizations must complete the following three steps in order to require the use of an approved client app on mobile devices and Exchange ActiveSync clients.

Step 1: Policy for Android and iOS based modern authentication clients requiring the use of an approved client application when accessing Exchange Online and SharePoint Online.

Sign in to the Microsoft Entra admin center as a Security Administrator, or Conditional Access Administrator.

Browse to Identity, then Protection, and then Conditional Access.

Select New policy.

Give your policy a name. We recommend that organizations create a meaningful standard for the names of their policies.

Under Assignments, select Users and groups.

Under Include, select All users or the specific Users and groups you wish to apply this policy to.
Select Done.
Under Cloud apps or actions, then Include, select Office 365 Exchange Online and Office 365 SharePoint Online.

Under Conditions, select Device platforms.

Set Configure to Yes.
Include Android and iOS.
Under Conditions, select Client apps (preview).

Set Configure to Yes.
Select Mobile apps and desktop clients and Modern authentication clients.
Under Access controls, then Grant, select Grant access, Require approved client app, and select Select.

Confirm your settings and set Enable policy to On.

Select Create to create and enable your policy.

Step 2: Policy for Exchange ActiveSync clients requiring the use of an approved client app.

Browse to Identity, then Protection, and then Conditional Access.

Select New policy.

Give your policy a name. We recommend that organizations create a meaningful standard for the names of their policies.

Under Assignments, select Users and groups.

Under Include, select All users or the specific Users and groups you wish to apply this policy to.
Select Done.
Under Cloud apps or actions, then Include, select Office 365 Exchange Online.

Under Conditions:

Client apps (preview):

Set Configure to Yes.
Select Mobile apps and desktop clients and Exchange ActiveSync clients.
Under Access controls, then Grant, select Grant access, Require approved client app, and select Select.

Confirm your settings and set Enable policy to On.

Select Create to create and enable your policy.

Step 3: Configure Intune app protection policy for iOS and Android client applications.

Review the article How to create and assign app protection policies for steps to create app protection policies for Android and iOS.

App protection policies overview
App protection policies (APP) are rules that ensure an organization's data remains safe or contained in a managed app. A policy can be a rule that is enforced when the user attempts to access or move "corporate" data, or a set of actions that are prohibited or monitored when the user is inside the app. A managed app has app protection policies applied to it, and it can be managed by Intune.

Mobile Application Management (MAM) app protection policies allow you to manage and protect your organization's data within an application. With MAM without enrollment (MAM-WE), a work or school-related app that contains sensitive data can be managed on almost any device, including personal devices in bring-your-own-device (BYOD) scenarios. Many productivity apps, such as the Microsoft Office apps, can be managed by Intune MAM.

How you can protect app data
Your employees use mobile devices for both personal and work tasks. While making sure your employees can be productive, you want to prevent data loss—intentional and unintentional. You'll also want to protect company data that is accessed from devices that you don't manage.

You can use Intune app protection policies independent of any mobile-device management (MDM) solution. This independence helps you protect your company's data with or without enrolling devices in a device management solution. By implementing app-level policies, you can restrict access to company resources and keep data within the purview of your IT department.

App protection policies on devices
App protection policies can be configured for apps that run on devices that are:

Enrolled in Microsoft Intune: These devices are typically corporate owned.

Enrolled in a third-party MDM solution: These devices are typically corporate owned.

Note
Mobile app management policies should not be used with third-party mobile app management or secure container solutions.

Not enrolled in any mobile device management solution: These devices are typically employee-owned devices that aren't managed or enrolled in Intune or other MDM solutions.

Important
You can create mobile app management policies for Office mobile apps that connect to Microsoft 365 services. You can also protect access to Exchange on-premises mailboxes by creating Intune app protection policies for Outlook for iOS/iPadOS and Android enabled with hybrid Modern Authentication. Before using this feature, make sure you meet the Outlook for iOS/iPadOS and Android requirements. App protection policies are not supported for other apps that connect to on-premises Exchange or SharePoint services.

Benefits of using app protection policies
The important benefits of using app protection policies are the following:

Protecting your company data at the app level. Because mobile app management doesn't require device management, you can protect company data on both managed and unmanaged devices. The management is centered on the user identity, which removes the requirement for device management.

End-user productivity isn't affected and policies don't apply when using the app in a personal context. The policies are applied only in a work context, which gives you the ability to protect company data without touching personal data.

App protection policies ensure that the app-layer protections are in place. For example, you can:

Require a PIN to open an app in a work context.
Control the sharing of data between apps.
Prevent the saving of company app data to a personal storage location.
MDM, in addition to MAM, ensures that the device is protected. For example, you can require a PIN to access the device, or you can deploy managed apps to the device. You can also deploy apps to devices through your MDM solution to give you more control over app management.

There are additional benefits to using MDM with app protection policies, and companies can use app protection policies with and without MDM at the same time. For example, consider an employee who uses a phone issued by the company, as well as their personal tablet. The company phone is enrolled in MDM and protected by app protection policies, while the personal device is protected by app protection policies only.

If you apply a MAM policy to the user without setting the device state, the user will get the MAM policy on both the BYOD device and the Intune-managed device. You can also apply a MAM policy based on the managed state. So when you create an app protection policy, next to Target to all app types, you'd select No. Then do any of the following:

Apply a less strict MAM policy to Intune managed devices, and apply a more restrictive MAM policy to non MDM-enrolled devices.
Apply a MAM policy to unenrolled devices only.



### Implement session management and continuous access evaluation

Summarize

Turn into podcast
Unit 9/12
In complex deployments, organizations might have a need to restrict authentication sessions. Some scenarios might include:

Resource access from an unmanaged or shared device.
Access to sensitive information from an external network.
High priority or executive users.
Critical business applications.
Conditional Access controls allow you to create policies that target specific use cases within your organization without affecting all users.

Before diving into details on how to configure the policy, let’s examine the default configuration.

User sign-in frequency
Sign-in frequency defines the time period before a user is asked to sign in again when attempting to access a resource.

The Microsoft Entra ID default configuration for user sign-in frequency is a rolling window of 90 days. Asking users for credentials often seems like a sensible thing to do, but it can backfire: Users who are trained to enter their credentials without thinking can unintentionally supply them to a malicious credential prompt.

It might sound alarming to not ask for a user to sign back in; in reality any violation of IT policies will revoke the session. Some examples include a password change, an incompliant device, or an account disable. You can also explicitly revoke users’ sessions using PowerShell. The Microsoft Entra ID default configuration comes down to 'don’t ask users to provide their credentials if the security posture of their sessions hasn't changed.'

The sign-in frequency setting works with apps that have implemented OAUTH2 or OIDC protocols according to the standards. Most apps for Windows, Mac, and mobile, including the following web applications, comply with the setting.

Word, Excel, PowerPoint Online
OneNote Online
Office.com
Microsoft 365 Admin portal
Exchange Online
SharePoint and OneDrive
Teams web client
Dynamics CRM Online
Azure portal
The sign-in frequency setting works with SAML applications as well, as long as they don't drop their own cookies and are redirected back to Microsoft Entra ID for authentication on a regular basis.

User sign-in frequency and multifactor authentication
Sign-in frequency previously applied only to the first factor authentication on devices that were Microsoft Entra joined, Hybrid Microsoft Entra joined, and Microsoft Entra registered. There was no easy way for our customers to re-enforce multifactor authentication (MFA) on those devices. Based on customer feedback, sign-in frequency will apply for MFA as well.

Diagram of multifactor authentication sign-in process with sign-in frequency.

User sign-in frequency and device identities
If you have Microsoft Entra joined, hybrid Microsoft Entra joined, or Microsoft Entra registered devices, when a user unlocks their device or signs in interactively, this event will satisfy the sign-in frequency policy as well. In the following two examples user sign-in frequency is set to one hour:

Example 1:

At 00:00, a user signs in to their Windows 10 Microsoft Entra joined device and starts work on a document stored on SharePoint Online.
The user continues working on the same document on their device for an hour.
At 01:00, the user is prompted to sign in again based on the sign-in frequency requirement in the Conditional Access policy configured by their administrator.
Example 2:

At 00:00, a user signs in to their Windows 10 Microsoft Entra joined device and starts work on a document stored on SharePoint Online.
At 00:30, the user gets up and takes a break, locking their device.
At 00:45, the user returns from their break and unlocks the device.
At 01:45, the user is prompted to sign in again based on the sign-in frequency requirement in the Conditional Access policy configured by their administrator since the last sign-in happened at 00:45.
Persistence of browsing sessions
A persistent browser session allows users to remain signed in after closing and reopening their browser window. The Microsoft Entra ID default for browser session persistence allows users on personal devices to choose whether to persist the session by showing a 'Stay signed in?' prompt after successful authentication.

Validation
Use the What-If tool to simulate a sign-in from the user to the target application and other conditions based on how you configured your policy. The authentication session management controls show up in the result of the tool.

Screenshot of the Conditional Access What If tool results.

Policy deployment
To make sure that your policy works as expected, the recommended best practice is to test it before rolling it out into production. Ideally, use a test tenant to verify whether your new policy works as intended.

Continuous Access Evaluation (CAE)
Token expiration and refresh are a standard mechanism in the industry. When a client application like Outlook connects to a service like Exchange Online, the API requests are authorized using OAuth 2.0 access tokens. By default, access tokens are valid for one hour, when they expire the client is redirected to Microsoft Entra ID to refresh them. That refresh period provides an opportunity to reevaluate policies for user access. For example: we might choose not to refresh the token because of a Conditional Access policy, or because the user has been disabled in the directory.

However, there is lag between when conditions change for a user, and when policy changes are enforced. Timely response to policy violations or security issues really requires a "conversation" between the token issuer, and the relying party (enlightened app). This two-way conversation gives us two important capabilities. The relying party can see when properties change, like network location, and tell the token issuer. It also gives the token issuer a way to tell the relying party to stop respecting tokens for a given user because of account compromise, disablement, or other concerns. The mechanism for this conversation is continuous access evaluation (CAE).

Benefits
There are several key benefits to continuous access evaluation.

User termination or password change/reset: User session revocation will be enforced in near real time.
Network location change: Conditional Access location policies will be enforced in near real time.
Token export to a machine outside of a trusted network can be prevented with Conditional Access location policies.
Evaluation and revocation process flow
Diagram of the process flow when an access token is revoked and a client has to reverify access.

A continuous access evaluation (CAE)-capable client presents credentials or a refresh token to Microsoft Entra ID asking for an access token for some resource.
An access token is returned along with other artifacts to the client.
An Administrator explicitly revokes all refresh tokens for the user. A revocation event will be sent to the resource provider from Microsoft Entra ID.
An access token is presented to the resource provider. The resource provider evaluates the validity of the token and checks whether there's any revocation event for the user. The resource provider uses this information to decide to grant access to the resource or not.
In the case of the diagram, the resource provider denies access, and sends a 401+ claim challenge back to the client.
The CAE-capable client understands the 401+ claim challenge. It bypasses the caches and goes back to step 1, sending its refresh token along with the claim challenge back to Microsoft Entra ID. Microsoft Entra ID will then reevaluate all the conditions and prompt the user to reauthenticate in this case.
\

### Exercise - Configure authentication session controls
Unit 10/12
In this exercise you will configure sign in frequency controls using a conditional access policy.

Sign in to the Microsoft Entra admin center using an Administrator account.
Open the portal menu and then select Identity.
On the Identity menu, then select Protection.
On the Protection menu, select Conditional access.
On the top menu, select New policy.
Screenshot of the Conditional Access blade with New policy highlighted.

In the Name box, enter Sign in frequency.
Under Assignments, select Users and groups.
On the Include tab, select the Users and groups check box.
In the Select pane, select your administrator account and then select Select.
Select Cloud apps or actions.
Verify Cloud apps is selected and then select Select apps.
In the Select pane, select Office 365 and then select Select.
Under Access controls, select Session.
In the Session pane, select Sign-in frequency.
In the value box, enter 30.
Select the units menu, select Days, and then select Select.
Under Enable policy, select Report-only, and then select Create.



### Microsoft Entra Conditional Access Optimization agent

Summarize

Turn into podcast
Unit 11/12
The Conditional Access optimization agent helps you ensure all users are protected by policy. It recommends policies and changes based on best practices aligned with Zero Trust and Microsoft learning.

The Conditional Access optimization agent evaluates policies such as requiring multifactor authentication (MFA). The agent enforces device based controls (device compliance, app protection policies, and domain-joined devices). Finally, the agent can help block legacy authentication and device code flow.

The agent also evaluates all existing enabled policies to propose potential consolidation of similar policies.

Requirement to use the Conditional Access optimization agent
You must have at least the Microsoft Entra ID P1 license.
You must have available Security Compute Units (SCU).
To activate the agent the first time, you need the Security Administrator or higher role.
You can assign Conditional Access Administrators with Security Copilot access.
For more information, see Assign Security Copilot access
Device-based controls require Microsoft Intune licenses.


# Conditional Access optimization agent key features
The Conditional Access optimization agent scans your tenant for new users and applications and determines if Conditional Access policies are applicable. The key features include:

This table describes the capabilities of the **Conditional Access Optimization Agent** (an AI-powered agent that reviews and improves Conditional Access policies).

For exam purposes, focus on **Feature → What it does**.

| Feature                           | What the Agent Does                                                                          |
| --------------------------------- | -------------------------------------------------------------------------------------------- |
| **Require MFA**                   | Finds users not protected by MFA policies and updates policies to require MFA.               |
| **Require device-based controls** | Enforces device compliance, app protection, or domain-joined device requirements.            |
| **Block legacy authentication**   | Prevents old authentication methods (POP3, IMAP, SMTP Basic Auth, etc.) from being used.     |
| **Policy consolidation**          | Detects duplicate/overlapping Conditional Access policies and recommends combining them.     |
| **Block device code flow**        | Checks whether device code flow authentication is blocked and recommends blocking it if not. |
| **One-click remediation**         | Automatically applies the recommended fix when you click **Apply suggestion**.               |

---

# Memory Trick

Think of the agent as a **Conditional Access Doctor**.

### 1. Protect Users

```text
Require MFA
Require Device Controls
```

### 2. Block Weak Access

```text
Block Legacy Authentication
Block Device Code Flow
```

### 3. Clean Up Policies

```text
Policy Consolidation
```

### 4. Fix Everything Quickly

```text
One-Click Remediation
```

---

# High-Probability Exam Questions

### Which feature identifies users not protected by MFA?

✅ **Require MFA**

---

### Which feature blocks old protocols such as IMAP, POP3, and SMTP Basic Auth?

✅ **Block Legacy Authentication**

---

### Which feature enforces compliant or domain-joined devices?

✅ **Require Device-Based Controls**

---

### Which feature finds duplicate Conditional Access policies?

✅ **Policy Consolidation**

---

### Which feature checks for device code flow authentication blocking?

✅ **Block Device Code Flow**

---

### Which feature automatically applies a recommended fix?

✅ **One-Click Remediation**

---

# Ultra-Short Cheat Sheet

```text
Require MFA
→ Protect users

Require Device Controls
→ Protect devices

Block Legacy Auth
→ Block old protocols

Policy Consolidation
→ Merge duplicate policies

Block Device Code Flow
→ Block device-code sign-ins

One-Click Remediation
→ Auto-fix policies
```

A common Microsoft exam pattern is:

> "The agent detects overlapping Conditional Access policies. What feature provides a recommendation?"

✅ **Policy Consolidation**

or

> "You want the agent to automatically update the policy after a recommendation is identified."

✅ **One-Click Remediation**.






### https://microsoftlearning.github.io/click-throughs/docs/IG/interactive_guide_explore_conditional_access_optimization_agent_web/story.html







### Summary and resources
Unit 12/12
After completing this module, you are able to:

Plan and implement security defaults.
Plan your Conditional Access policies.
Implement Conditional Access policy controls and assignments (targeting, applications, and conditions).
Test and troubleshoot Conditional Access policies.
Implement application controls.
Implement session management.
Configure continuous access evaluation.
Resources
To learn more about the technology in this module, check out the following links to documentation:

What is Conditional Access?- https://youtu.be/ffMAw2IVO7A
How to deploy Conditional Access?- https://youtu.be/c_izIRNJNuk
How to roll out CA policies to end users?- https://youtu.be/0_Fze7Zpyvc
Conditional Access with device controls- https://youtu.be/NcONUf-jeS4
Conditional Access with Microsoft Entra MFA- https://youtu.be/Tbc-SU97G-w
Conditional Access in Enterprise Mobility + Security- https://youtu.be/A7IrxAH87wc
Using the location condition in a Conditional Access policy- https://learn.microsoft.com/en-us/entra/identity/conditional-access/howto-conditional-access-policy-location
Use compliance policies to set rules for devices you manage with Intune- https://learn.microsoft.com/en-us/mem/intune/fundamentals/deployment-plan-compliance-policies
Introducing security defaults- https://techcommunity.microsoft.com/t5/azure-active-directory-identity/introducing-security-defaults/ba-p/1061414
Plan a Conditional Access deployment- https://learn.microsoft.com/en-us/entra/identity/conditional-access/plan-conditional-access
Continuous Access Evaluation (CAE)- https://learn.microsoft.com/en-us/entra/identity/conditional-access/concept-continuous-access-evaluation
Conditional Access for agent identities (Microsoft Entra Agent ID)- https://learn.microsoft.com/en-us/entra/identity/conditional-access/concept-conditional-access-policy-common































































































































































































































