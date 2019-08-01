# Data

#### GET /api/v1/data/{dataId}
Return information about previously added data

#### HEAD /api/v1/data/{dataId}
Check if data with id = dataId exists

#### PUT /api/v1/data/{dataId}
Update data by dataId

#### DELETE /api/v1/data/{dataId}
Delete data by id

#### GET /api/v1/data/{dataId}/content
Get the actual data content. This can either be XML or json

#### GET /api/v1/data/{dataId}/preview
Get the data as sent to the document preview

#### GET /api/v1/data/meta
Get a sample for the metadata used when generating documents

<table>
<tr><th>Query parameter</th><th>Description</th></tr>
<tr><td>creator</td><td>The name of the creator to use</td></tr>
<tr><td>projectName</td><td>The name of the project to use</td></tr>
<tr><td>templateName</td><td>The name of the template to use</td></tr>
</table>

Creates an XML sample using the input data