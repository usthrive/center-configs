# Center Configurations Repository

## Purpose
This repository serves as the central configuration store for the DEZ-CENTERS application. It contains configuration files for all centers managed by the platform, separating configuration data from application code to improve maintainability and security.

## Benefits of This Architecture
- **Separation of concerns** - Configuration data lives independently from application code
- **Security** - Limited access permissions for automated systems
- **Versioning** - Full history of configuration changes
- **Validation** - Automatic schema validation ensures data integrity
- **Automation** - Changes can be automated via Supabase edge functions

## Repository Structure

### `/configs/`
Individual JSON configuration files for each center, named using the center code:
```
configs/
  center1.json
  center2.json
  ...
```

### `/schema/`
JSON Schema definitions that describe the structure and validation rules for configuration files:
```
schema/
  center-schema.json
```

## Configuration Format
Each center configuration includes:

```json
{
  "code": "center1",
  "name": "Center Name",
  "domain": "center1.example.com",
  "features": {
    "keyTakeaways": true,
    "summaryVideo": true,
    "fullVideo": true,
    "detailedNotes": false,
    "activity": false
  },
  "admins": ["admin@example.com"],
  "sheetId": "spreadsheet-id-if-applicable",
  "theme": {
    "primary": "#0d6efd",
    "secondary": "#6c757d"
  },
  "status": "active",
  "timestamp": "2025-04-21T05:17:50-07:00"
}
```

## Integration with Supabase
This repository connects with Supabase edge functions to enable automated configuration updates:

1. Edge function authenticates with GitHub using personal access token
2. Updates or creates center configuration files when triggered
3. Commits changes back to this repository
4. DEZ-CENTERS application pulls the latest configurations when loaded

## Usage Instructions

### Adding/Updating a Center Configuration
1. Create a new JSON file in `/configs/` named after the center code
2. Ensure it follows the schema defined in `/schema/center-schema.json`
3. Commit and push your changes

### Automated Updates
Configuration files are automatically updated by the Supabase edge function when center data changes in the database.

### Manual Updates
For manual changes, update the configuration files directly in this repository.

## Security Notes
- Supabase edge functions use a GitHub personal access token with limited scope
- The token only has access to this specific repository
- All configuration changes are tracked with full commit history
Place where the config file will stay which will be updated based on supabase updates
