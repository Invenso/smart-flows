# Templates

For default create, read, update & delete operations see [CRUD](/3.%20Smart%20Flows%20Entities/1.%20CRUD.md).

#### GET /api/v1/templates/{templateId}/content
Gets the content of the template for the given language.

<table>
<tr><th>Query parameter</th><th>Description</th></tr>
<tr><td>includeMeta</td><td>Whether template meta information should already be included in the template 
document itself. Default value: false</td></tr>
<tr><td>lang</td><td>The id of the language that is supported by the project, default when none specified.</td></tr>
<tr><td>version</td><td>The version ID or the revision number of the template to retrieve. Latest version 
if not specified.</td></tr>
</table>


#### PUT /api/v1/templates/{templateId}/content
Updates the content of the template for the given language.

#### DELETE /api/v1/templates/{templateId}/content
Deletes the content of the template for the given language.

<table>
<tr><th>Query parameter</th><th>Description</th></tr>
<tr><td>lang</td><td>The id of the language that is supported by the project, default when none specified.</td></tr>
<tr><td>deleteInbound</td><td>When true, later versions of this template will also be deleted. When 
false, an error is returned when there is some link to this standard template. Default value: false</td></tr>
</table>


#### GET /api/v1/templates/{templateId}/history
This is a [paged entity](/3.%20Smart%20Flows%20Entities/1.%20CRUD.md). Only GET is supported.

<table>
<tr><th>Query parameter</th><th>Description</th></tr>
<tr><td>lang</td><td>The id of the language that is supported by the project, default when none specified.</td></tr>
</table>

#### GET /api/v1/templates/{templateId}/lang/{langId}
Gets info about the template for the given language.

#### GET /api/v1/templates/{templateId}/schema
Get the schema of the fields that are usable in the template.
