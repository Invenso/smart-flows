# Data sources
Data sources are created automatically when certain elligible connectors are created (Dynamics & Sugar). 
CUD operations on data sources should be avoided to ensure stability of your environment. The layout endpoints
are commonly used to create data sets. 

For default create, read & update operations see [CRUD](/3.%20Smart%20Flows%20Entities/1.%20CRUD.md).
Delete is not supported

### Data Source Layout

#### GET /api/v1/datasources/{datasourceId}/layout
Gets all the fields and relations that are available in the datasource
<table>
<tr><th>Query parameter</th><th>Description</th></tr>
<tr><td>full</td><td>True to return all fields & relations together with all entities. False only returns the entities.</td></tr>
</table>

#### GET /api/v1/datasources/{datasourceId}/layout/{entityName}
Gets all the fields and relations for the entity.

### Data Source Types

#### GET /api/v1/datasources/types
Gets all datasources for this project. These are 1:1 related with connectors.

#### GET /api/v1/datasources/types/{datasourceTypeId}
Gets a single datasourceType object.