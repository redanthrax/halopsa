# Grafana

Ensure you meet prerequisites before setting up any dashboards or gauges.

## Dashboards

[Agent Dashboard](./dashboards/Agent%20Dashboard/README.md)

## Prerequisites

This guide assumes you already have an instance of grafana setup and will not
include details for setup.

### Setup Infinity Plugin
1. Install the Plugin
    - Navigate to the side menu: Administration > Plugins and Data > Plugins.
    - Search for "Infinity" in the search bar.
    - Click the Infinity tile, then click Install. Installation may take a minute.
2. Setup HaloPSA Credentials
    1. Log into HaloPSA
        - Navigate to Configuration > Integrations > HaloPSA API with an admin account.
    2. Retrieve API Details
        - Note the Resource Server URL, Authorization Server URL, and Tenant Name from the API Details section.
        - Create an Application:In the View Applications section, click New.
        - Enter an Application Name (e.g., "Grafana Infinity").
        - Select Client ID and Secret (Services) as the Authentication Method.
        - Copy the Client ID and Client Secret (the secret is shown only once; save it securely).
    3. Set Permissions
        - On the application’s Permissions tab, click Edit.
        - Grant at least read:tickets, read:assets, read:customers, and read:contracts permissions (add others like edit:tickets if needed for future functionality).
        - Save the permissions.
3. Configure the Infinity Data Source
    1. Add Data Source
        - In Grafana, go to Connections > Add new connection (or Configuration > Data Sources in older versions).
        - Search for "Infinity" and select it.
        - Click Create an Infinity data source.
    2. Data Source Settings
        - Name: Set a name (e.g., "HaloPSA Infinity").
        - URL: Enter the HaloPSA Resource Server URL (e.g., https://your-tenant.halopsa.com/api).
    3. Authentication
        - Select OAuth 2.0 for HaloPSA’s API.
        - Set Token URL to the Authorization Server URL from HaloPSA.
        - Enter the Client ID and Client Secret from Step 2.
        - Set Scopes to include required permissions (e.g., read:tickets read:assets read:customers read:contracts).
        - HTTP Method: Use GET for most HaloPSA API queries (POST may be needed for specific endpoints).
        - TLS Settings: If you encounter certificate errors, enable Skip TLS Verification (not recommended for production) or configure proper certificates.
        - Health Check: Enable and test with a simple GET request to an endpoint like /tickets to verify connectivity (expects HTTP 200).
    4. Save and Test
        - Click Save & Test. A "Connection Successful" message confirms the setup. If you get errors, verify the URLs, Client ID, Client Secret, or permissions.

