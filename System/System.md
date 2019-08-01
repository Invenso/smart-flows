# System

#### POST /api/v1/system/backup
Create a backup of all objects in the project. Returns a zip file.

<table>
<tr><th>Query parameter</th><th>Description</th></tr>
<tr><td>includeHistory</td><td>Whether to include the complete history of templates</td></tr>
<tr><td>includeSensitiveData</td><td>Whether to include possible sensitive data (passwords from connectors e.a.)</td></tr>
</table>

#### POST /api/v1/system/backup/restore
Use the zip file as POST body from POST /api/v1/system/backup. This will not clear a project. All objects will be added, not
overwritten.

#### GET /api/v1/system/cleanup/run
Run one or all cleanup processes now.
<table>
<tr><th>Query parameter</th><th>Description</th></tr>
<tr><td>action</td><td>The cleanup action to run. When not specified, all actions are triggered</td></tr>
</table>

#### GET /api/v1/system/currencies
Returns all the currency symbols that are available on the system, this is [paged](/3.%20Smart%20Flows%20Entities/1.%20CRUD.md).

#### POST /api/v1/system/export
Create an export for the given objects.

<table>
<tr><th>Query parameter</th><th>Description</th></tr>
<tr><td>includeHistory</td><td>Whether to include the complete history of templates</td></tr>
<tr><td>includeSensitiveData</td><td>Whether to include possible sensitive data (passwords from connectors e.a.)</td></tr>
<tr><td>includeUserData</td><td>Whether to include data objects that are created by users (samples)</td></tr>
</table>

The body will have similar structure to:
```
{
  "items": [
    {
      "displayName": "flow 1",
      "id": "flow-1",
      "type": "flow"
    },
    {
      "displayName": "template 6",
      "id": "template-6",
      "type": "template"
    },
    ...
  ]
}
```

#### PUT /api/v1/system/expression
Parse the given expression

#### GET /api/v1/system/expression/functions
Gets all the supported template expression functions

#### GET /api/v1/system/features
To be implemented

#### GET /api/v1/system/format
To be implemented

#### POST /api/v1/system/import
Execute an import of flows/templates/data sets. The POST-body should contains all mappings so all objects are linked
to the right objects. Usually done after POST /api/v1/system/import/prepare. overwriteExisting is a setting which can be 
set on or off. It is highly recommended to us the project console for this.

#### POST /api/v1/system/import/prepare
Send an export of flows/templates/data sets. Returns import information on how mappings can be made. It is highly
recommended to us the project console for this.

#### GET /api/v1/system/info
Get system information like the projectId, project name, the version & esign provider.

#### GET /api/v1/system/languages
Returns all the languages that are available on the system, this is [paged](/3.%20Smart%20Flows%20Entities/1.%20CRUD.md).

#### GET /api/v1/system/languages/default
Returns the default language for the system

#### PUT /api/v1/system/languages/default
Updates the default system language for the system

#### GET /api/v1/system/languages/ui
Returns all the languages that are availabled for the user interface

#### GET /api/v1/system/license
Returns the current license

#### POST /api/v1/system/license
Installs a new license

#### GET /api/v1/system/notifications
Returns the current notifications. Could differ on user role.

#### GET /api/v1/system/printers
Returns a list of all available printers on the system

#### GET /api/v1/system/printers/{printer}
Returns a single printer

#### PUT /api/v1/system/pseudo/sort
Sorts the given list of pseudofields

#### GET /api/v1/system/timeZones
Returns all timezones available on the system.