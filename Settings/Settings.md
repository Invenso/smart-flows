#Settings

This API manages the settings for your project.
#### GET /api/v1/settings/public
The public settings of the project. These are publicly available properties like the url for the Flow Execution Panel,
the system language & the project id.

#### GET /api/v1/settings
Get all other settings. You need to be authenticated for this. It contains cleanup settings, the default project plugin,
fronted settings like themes & date display formats, default tag groups & user management.

#### GET /api/v1/settings/{settingsType}
Settings can be fetched per settingsType. settingsType are the first level properties retrieved from GET /api/v1/settings.

#### PUT /api/v1/settings/{settingsType}
Settings can be updated per settingsType.

#### DELETE /api/v1/settings/{settingsType}
Settings can be cleared per settingsType.
