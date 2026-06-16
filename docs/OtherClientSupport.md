# Other client support (App registrations)

Use these steps to configure a 3rd-party client with Azure Resource Manager MCP server access.

## 1. Create an app registration

In **Microsoft Azure > App registrations**, create a new app registration for your client.

## 2. Update `manifest.requiredResourceAccess`

Manually add the following entries:

```json
[
  {
    "resourceAppId": "22bfbae3-f4e7-485f-be43-8cee15065084",
    "resourceAccess": [
      {
        "id": "601b3b64-a3c4-4faa-ab9c-8f97ba332aa3",
        "type": "Scope"
      }
    ]
  },
  {
    "resourceAppId": "1c167cbf-701e-4941-bf1e-98162a419003",
    "resourceAccess": [
      {
        "id": "31d0c4b9-dc46-49bc-a512-c307ba90248e",
        "type": "Scope"
      }
    ]
  }
]
```

After saving the manifest, the **API permissions** page should show both required delegated scopes.

## 3. Configure redirect URI

Set the required **Redirect URI** on the app registration for your client environment.

## 4. Create service principals

Create service principals for each app registration ID (use separate IDs for test and production):

```bash
az ad sp create --id <test-app-registration-id>
az ad sp create --id <prod-app-registration-id>
```

## 5. Create a client secret

Create a new client secret and copy the **secret value** (not the secret ID).

Use this value in your Claude Code custom connector definition.

## 6. Set in-tenant connector values

Configure the connector with your own in-tenant settings:

- Tenant ID
- Client ID
- Redirect URI
- Client secret value
