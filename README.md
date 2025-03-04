# jira-cloud-api
# **Jira Admin API and Organization Management**

## **1. Organization ID**
The Organization ID is a unique identifier used to manage organizations within the Jira Admin API. It is required for various API operations, such as managing users, roles, and permissions. To locate the Organization ID:
- Navigate to the **Atlassian Administration Console** at [admin.atlassian.com](https://admin.atlassian.com).
- Under **Settings**, go to **API Keys** and create or manage existing API keys.
- The Organization ID can also be obtained programmatically using the Organizations REST API endpoint:  
  `GET https://api.atlassian.com/admin/v1/orgs`  
  This will return a list of organizations associated with your account, including their IDs.  
  Sources: (https://developer.atlassian.com/cloud/admin/organization/rest/), (https://support.atlassian.com/organization-administration/docs/manage-an-organization-with-the-admin-apis/)

---

## **2. API Key**
The API Key acts as a secure token for authenticating requests to the Jira Admin API. To generate an API key:
1. Go to **API Keys** in the **Settings** menu of the Atlassian Administration Console.
2. Click **Create API Key**, provide a recognizable name, and copy the generated key securely.
3. Use the API key in your requests as a Bearer token in the Authorization header:  
   ```
   Authorization: Bearer <API_KEY>
   ```
   Ensure the key is kept confidential to prevent unauthorized access.  
   Sources: (https://support.atlassian.com/organization-administration/docs/manage-an-organization-with-the-admin-apis/)

---

## **3. Example API Usage**
Below is an example of how to use the Jira Admin API to search for users within an organization:

### **cURL Command**
```bash
curl --request POST \
  --url 'https://api.atlassian.com/admin/v1/orgs/<organization-id>/users/search' \
  --header 'Authorization: Bearer <API_KEY>' \
  --header 'Accept: application/json' \
  --header 'Content-Type: application/json' \
  --data '{
    "emailUsernames": {
      "eq": ["exampleuser@example.com"]
    }
  }'
```

### **Successful Response**
```json
{
  "data": [
    {
      "accountId": "12345:67890-abcde-fghij-klmno",
      "accountType": "atlassian",
      "accountStatus": "active",
      "statusInUserbase": true
    }
  ],
  "links": {}
}
```
This response includes details about the user, such as their account ID, type, and status.  
Sources: (https://developer.atlassian.com/cloud/admin/organization/rest/), (https://community.developer.atlassian.com/t/how-to-get-organization-id-in-codes-or-through-what-rest-api/81791)

---

## **4. Managing Roles and Permissions**
To manage roles and permissions, you can use the following API endpoint to view or modify project roles:
- **Endpoint:**  
  `GET https://api.atlassian.com/project/<project-key>/role/<role-id>`
- **Required Headers:**  
  - Authorization: Bearer `<API_KEY>`
  - Accept: application/json

### **Examples of Roles**
- **Administrator:** Full access to manage the project and its settings.
- **Viewer:** Read-only access to project data.
- **Member:** Access to collaborate within the project.  

For more details, refer to [Jira Platform REST API documentation](https://developer.atlassian.com/cloud/jira/platform/rest/v3/).  
Sources: (https://support.atlassian.com/organization-administration/docs/manage-an-organization-with-the-admin-apis/), (https://community.developer.atlassian.com/t/how-to-get-organization-id-in-codes-or-through-what-rest-api/81791)

---

## **5. Additional Resources**
- [Organizations REST API Documentation](https://developer.atlassian.com/cloud/admin/organization/rest/)  
- [Managing Organizations with Admin APIs](https://support.atlassian.com/organization-administration/docs/manage-an-organization-with-the-admin-apis/)  
- [Understanding Organization IDs](https://confluence.atlassian.com/jirakb/what-it-is-the-organization-id-and-where-to-find-it-1207189876.html)  

These resources provide comprehensive guides and examples for working with the Jira Admin API.

---
