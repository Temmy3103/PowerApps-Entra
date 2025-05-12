# PowerApps-Entra
#  Power Apps Mobile User Creator for Microsoft Entra ID (Azure AD)

A low-code mobile app built with Power Apps that allows you to **create users in Microsoft Entra ID (Azure AD)** on the go, using Power Automate and Microsoft Graph API.

##  Overview

This project enables IT admins, HR teams, or onboarding staff to create Entra ID users from their phone — no need to access the Azure portal. It's built using:

- **Power Apps** for the UI
- **Power Automate** for backend processing
- **Microsoft Graph API** to interact with Entra ID
- **Azure App Registration** for secure API access

---

## Tools & Technologies

| Tool              | Purpose                                 |
|-------------------|-----------------------------------------|
| Power Apps        | Front-end mobile app                    |
| Power Automate    | Flow that handles user creation logic   |
| Microsoft Graph   | API to create Entra ID users            |
| Azure AD App Reg  | Secure token-based authentication       |

---

##  Features

- Mobile-friendly form for user creation
- Automatically triggers Microsoft Graph API
- Uses secure OAuth 2.0 token for access
- Instant user provisioning in Microsoft Entra ID
- Toggle to enable/disable account creation

---
![My Logo](![image](https://github.com/user-attachments/assets/e6d80628-773a-43fd-a3aa-0595bb7695b3)

##  App Fields

The app form includes:

- `First Name`
- `Last Name`
- `User Principal Name (UPN)`
- `Mail Nickname`
- `Department`
- `Job Title`
- `Mobile Phone`
- `Business Phone`
- `Office Location`
- `Enable Account` toggle

---

##  Flow Logic (Power Automate)

1. Triggered from Power Apps with form data
2. Uses HTTP action to call Microsoft Graph
3. Authenticates using client credentials from Azure App Registration
4. Sends a POST request to `https://graph.microsoft.com/v1.0/users`

### Sample JSON Payload

```json
{
  "accountEnabled": true,
  "displayName": "John Doe",
  "mailNickname": "jdoe",
  "userPrincipalName": "jdoe@yourdomain.com",
  "passwordProfile": {
    "forceChangePasswordNextSignIn": true,
    "password": "P@ssword123"
  },
  "givenName": "John",
  "surname": "Doe",
  "department": "Sales",
  "jobTitle": "Manager",
  "mobilePhone": "+123456789",
  "officeLocation": "NYC",
  "businessPhones": [
    "+123456789"
  ]
}
 Azure App Registration Setup
Go to Azure Portal > App registrations

Create a new registration

Add API permissions:

User.ReadWrite.All

Directory.ReadWrite.All

Grant admin consent

Create a client secret

Use the client ID, tenant ID, and secret in Power Automate's HTTP action

Power Apps Code Snippet
powerapps
Copy
Edit
ClearCollect(
    businessPhoneCol,
    { Value: BusinessNumberTextInput2_1.Text }
);

MicrosoftEntraID.CreateUser(
    Enabletoggle.Value,
    DisplayNameTextInput2_3.Text,
    MailNickNameTextInput2_4.Text,
    {
        password: "P@ssword123",
        forceChangePasswordNextSignIn: true
    },
    UserPrincipalNameTextInput2_5.Text,
    {
        givenName: FirstNameTextInput1_2.Text,
        surname: SurnameTextInput2.Text,
        department: DepartmentTextInput2_4.Text,
        jobTitle: JobTitleTextInput2_2.Text,
        mobilePhone: MobileNumberTextInput1_1.Text,
        officeLocation: officeLocationTextInput2_3.Text,
        businessPhones: businessPhoneCol
    }
);

)



Final Output
Once submitted, a new user is created in Entra ID within seconds. Ideal for:

Field onboarding

Remote IT teams

Events or training sessions
