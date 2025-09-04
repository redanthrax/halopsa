# Agent Dashboard

This Grafana dashboard provides comprehensive monitoring and analytics for agent performance, ticket management, and client metrics. The dashboard includes real-time visualizations for ticket volumes, resolution times, agent utilization, and client activity.

## Dashboard Components

### Panels Included
1. **Tickets Opened Today** - Gauge showing daily ticket volume
2. **Tickets Closed Today** - Gauge tracking closure rates
3. **Net Ticket Change** - Displays the difference between opened and closed tickets
4. **Stale Tickets** - Monitors tickets older than 7 days
5. **Average Resolution Time** - Shows resolution time in hours
6. **Agent Utilization** - Horizontal bar gauge showing daily utilization percentages
7. **Clients by Ticket Count** - Bar chart of top 5 clients by ticket volume

## Setup Instructions

### Prerequisites
- Grafana instance with admin access
- Infinity Data Source plugin installed
- API access to your ticketing system

### Step 1: Install Infinity Data Source Plugin

1. Navigate to **Configuration > Plugins** in your Grafana instance
2. Search for "Infinity" in the plugin catalog
3. Click **Install** on the "Infinity" data source by yesoreyeram
4. Wait for the installation to complete

### Step 2: Configure Data Source

1. Go to **Configuration > Data Sources**
2. Click **Add data source**
3. Select **Infinity** from the list
4. Configure the data source:
   - **Name**: Give it a meaningful name (e.g., "HaloPSA API")
   - **URL**: Your API base URL
   - **Auth**: Configure authentication as needed for your API
5. Click **Save & Test** to verify the connection
6. **Important**: Note the UID of this data source (visible in the URL or settings)

### Step 3: Import the Dashboard

#### Method 1: JSON Import (Recommended)

1. Copy the contents of `agentdashboard.json`
2. In Grafana, navigate to **+ > Import**
3. Paste the JSON content into the **Import via panel json** text area
4. Click **Load**
5. Configure the import settings:
   - **Name**: Agent Dashboard (or customize as needed)
   - **Folder**: Select appropriate folder
   - **UID**: Leave as default or customize
6. **Critical Step**: Update the data source UID
   - In the JSON, find all occurrences of `"uid": "example-datasource-uid"`
   - Replace `example-datasource-uid` with your actual Infinity data source UID
7. Click **Import**

#### Method 2: Manual Panel Creation

If you prefer to create panels manually:

1. Create a new dashboard: **+ > Dashboard**
2. For each panel in the JSON file, click **Add panel**
3. Configure each panel according to the specifications in `agentdashboard.json`

### Step 4: Configure API Endpoints

After importing, you'll need to update the API endpoints in each panel:

1. Edit each panel (click the panel title > Edit)
2. In the Query tab, update the **URL** field to match your API endpoints:
   - Replace `https://example.company.com/api/` with your actual API URL
   - Ensure endpoint paths match your API structure
3. Verify and adjust query parameters as needed for your API
4. Test each query to ensure data is returned correctly

### Step 5: Customize Thresholds and Styling

Adjust the visualization thresholds based on your organization's metrics:

1. **Tickets Opened Today**: Adjust max value and color thresholds
2. **Resolution Time**: Modify hour thresholds (currently 4h yellow, 8h red)
3. **Agent Utilization**: Update percentage thresholds as needed
4. **Stale Tickets**: Adjust the 7-day threshold if needed

### Step 6: Set Up Refresh and Time Range

The dashboard is configured with:
- **Refresh**: 30 seconds
- **Time Range**: Current day (now/d to now/d)
- **Timezone**: Browser timezone

Adjust these settings in **Dashboard Settings** if needed.

## API Requirements

This dashboard expects the following API endpoints to be available:

- **GET /api/Tickets** - Ticket data with filtering capabilities
- **GET /api/Agent** - Agent information
- **GET /api/TimesheetEvent** - Time tracking data
- **GET /api/Timesheet** - Timesheet configuration

### Required Query Parameters

The dashboard uses these common parameters:
- `datesearch` - Field to filter by date
- `startdate` / `enddate` - Date range filters
- `includeclosed` - Include/exclude closed tickets
- `tickettype_id` / `requesttype_id` - Filter by ticket types
- `count` - Limit number of results

## Troubleshooting

### Common Issues

1. **No Data Displayed**
   - Verify data source configuration and connectivity
   - Check API endpoint URLs and authentication
   - Ensure query parameters match your API requirements

2. **Panels Showing Errors**
   - Update the data source UID in all panel configurations
   - Verify JSON syntax if manually editing queries
   - Check API response format matches expected structure

3. **Incorrect Data**
   - Review root_selector JSONata expressions
   - Adjust date format parameters to match your API
   - Verify field names in transformations

### Performance Optimization

- Adjust refresh intervals based on your needs
- Implement API caching if possible
- Consider using smaller count limits for large datasets
- Monitor API rate limits and adjust refresh accordingly

## Customization

### Adding New Panels

1. Click **Add panel** in edit mode
2. Configure the Infinity data source
3. Set up your API query with appropriate parameters
4. Use JSONata expressions for data transformation
5. Configure visualization type and styling

### Modifying Existing Panels

1. Enter edit mode for the panel
2. Adjust queries, transformations, or visualizations as needed
3. Test changes before saving

## Support

For issues specific to:
- **Grafana Configuration**: Refer to Grafana documentation
- **Infinity Plugin**: Check the plugin documentation on GitHub
- **API Integration**: Consult your ticketing system's API documentation

---

**Note**: Remember to replace all placeholder URLs and UIDs with your actual configuration values before using the dashboard.
